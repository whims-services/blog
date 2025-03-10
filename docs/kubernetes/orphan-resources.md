---
icon: https://raw.githubusercontent.com/kubernetes/community/refs/heads/master/icons/svg/resources/unlabeled/ns.svg
tags:
  - kubernetes
  - namespace
---
# Detecting Orphaned Resources in Kubernetes

The efficient management of resources in Kubernetes is essential to maintain a clean and performant cluster. 
However, it may happen that resources become orphaned, meaning they are no longer associated with an existing namespace.

## Context

When deleting a namespace in Kubernetes, it may happen that the process blocks due to remaining resources or unresolved finalizers.
Forcing the finalization of a namespace can lead to orphaned resources, complicating the cluster management.

## Problem

Orphaned resources can cause various problems:
- **Unused resource consumption:** They allocate space and system resources.
- **Increased complexity:** They make debugging and maintenance more difficult.
- **Conflicts risks:** They can conflict with new resources created later.

## Solution

To avoid these problems, it is crucial to diagnose and resolve the underlying causes of a namespace blocking.
Here is a script that allows you to detect orphaned resources in a Kubernetes cluster:

```bash
#!/bin/bash

# Get the list of current namespaces in the cluster
current_namespaces=(\$(kubectl get ns --no-headers | awk '{print \$1}'))

# Get the list of API resources that are namespaced (associated with a namespace)
api_resources=(\$(kubectl api-resources --verbs=list --namespaced -o name))

# Iterate over each API resource
for api_resource in \${api_resources[@]}; do
    # Read each line of the output of the kubectl get command for the current API resource
    while IFS= read -r line; do
        # Extract the namespace from the resource from the line
        resource_namespace=\$(echo \$line | awk '{print \$1}')
        # Extract the name of the resource from the line
        resource_name=\$(echo \$line | awk '{print \$2}')

        # Check if the resource namespace does not exist in the list of current namespaces
        if [[ ! " \${current_namespaces[@]} " =~ " \$resource_namespace " ]]; then
            # If the namespace does not exist, display the API resource, the namespace and the resource name
            echo "api-resource: \${api_resource} - namespace: ${resource_namespace} - resource name: ${resource_name}"
        fi
        # Read the resources for the current API resource in all namespaces, ignoring errors if the namespace does not exist
    done < <(kubectl get \$api_resource -A --ignore-not-found --no-headers -o custom-columns="NAMESPACE:.metadata.namespace,NAME:.metadata.name")
done
```

## Usage

To use the script, save it to a file and make it executable:

```bash
chmod +x detect-orphan-resources.sh
./detect-orphan-resources.sh
```
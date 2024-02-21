## AWS EKS (using the eksctl tool)

This page provides instructions on how to manually create an EKS cluster using the `eksctl` tool with the minimum requirements to run the Agility application in High Availability mode.

To properly run the application, the cluster must include the following:


### Prerequisites
- eksctl
- helm

### Create Cluster
<details>

<summary>To create a cluster:</summary>

1- Run the following to generate the cluster definition (adjust the zone if needed)

```bash
export CLUSTER_NAME="demo-cluster"
export AWS_REGION="us-west-2"

export ACCOUNT_ID=$(aws sts get-caller-identity --output text --query Account)

cat <<EOF | tee ${CLUSTER_NAME}.yaml
---
apiVersion: eksctl.io/v1alpha5
kind: ClusterConfig

metadata:
  name: ${CLUSTER_NAME}
  region: us-west-2
  version: "1.24"

availabilityZones: ["us-west-2a", "us-west-2b", "us-west-2c"]

managedNodeGroups:
- name: nodegroup
  minSize: 4
  maxSize: 6
  desiredCapacity: 4
  instanceType: t3.2xlarge
  ssh:
    enableSsm: true

# To enable all of the control plane logs, uncomment below:
# cloudWatch:
#  clusterLogging:
#    enableTypes: ["*"]
EOF
```

2- Execute eksctl

```bash
eksctl create cluster -f ${CLUSTER_NAME}.yaml
```

Wait ~10 mins to have the cluster ready.

</details>



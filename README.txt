This directory contains the files needed to deploy a Ceph cluster with a 
host network configuration using Rook.

If running on AWS, the security groups need to be modified to allow traffic
from the Ceph ports to travel on the host network. 
From the AWS console, modify the worker-sg to allow TCP traffic from ports:
Ceph mon v1: 6789
Ceph mon v2: 3300
Ceph osd: 6800-7300

# Deploys everything needed for the Rook operator to run properly.
oc create -f common.yaml -f crds.yaml -f operator.yaml 

# Defines the Ceph cluster with host networking enabled,
# and the configmap that defines the network configuration.
oc create -f configmap-cluster.yaml

Notes:
Rook seems to have some silent errors, check the canary pods.

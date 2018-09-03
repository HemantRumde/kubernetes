# Create new Kubernetes cluster 
## S3 bucket to maintain k8s configuration files
* <code>hemantrumde.com</code> is a hosting zone in AWS Route53
* Create AWS bucket ```s3://kops.hemantrumde.com``` 

## AWS VPC 
* Create new **VPC** 
* Get id of this new VPC for kops --vpc option

## build k8s cluster with three nodes and one master 
```
kops create cluster --name=explore.hemantrumde.com \
     --yes \
     --cloud aws \
     --state=s3://kops.hemantrumde.com \
     --zones=us-west-2a,us-west-2b,us-west-2c\
     --master-size=t2.micro\
     --master-count=1\
     --node-size=t2.small\
     --node-count=3 \
     --dns-zone=hemantrumde.com\
     --vpc vpc-a51feedd\
     --ssh-public-key=~/.ssh/id_rsa.pub
```
## List of all clusters
```
kops get clusters 
```
Above command in yaml output provides more information about specified cluster
```
kops get clusters --name explore.hemantrumde.com -o yaml
kops get clusters -o json | jq -r '.metadata.name'
```

## Validate cluster 
```
kops validate cluster --name=explore.hemantrumde.com
Validating cluster explore.hemantrumde.com

INSTANCE GROUPS
NAME                    ROLE    MACHINETYPE     MIN     MAX     SUBNETS
master-us-west-2a       Master  t2.micro        1       1       us-west-2a
nodes                   Node    t2.small        3       3       us-west-2a,us-west-2b,us-west-2c

NODE STATUS
NAME                                            ROLE    READY
ip-30-30-102-21.us-west-2.compute.internal      node    True
ip-30-30-37-50.us-west-2.compute.internal       master  True
ip-30-30-49-222.us-west-2.compute.internal      node    True
ip-30-30-68-89.us-west-2.compute.internal       node    True

Your cluster explore.hemantrumde.com is ready
```

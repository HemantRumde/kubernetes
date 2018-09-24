# Add more nodes to existing cluster 
Use following command to change <code>maxSize</code> and <code>minSize</code> parameters. 
```
kops edit id --name explore.hemantrumde.com nodes
```
Upgrade the cluster to add additional nodes 
```
kops update cluster --name explore.hemantrumde.com --yes
```
# Rolling update 
```
kops rolling-update --name explore.hemantrumde.com --yes
```

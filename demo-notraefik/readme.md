# Simple Example

This example will deploy the [rancher-demo](https://hub.docker.com/r/monachus/rancher-demo) application into `default` namespace.
This app will cycle between all active pods within the same service on every cluster that the service enabled*.

*Note[Bug]: Somehow the connection only round robin to 1 cluster (eg. if there's 6 service split between 2 clusters, it'll only show 3 node on a cluster, but it does failover to another cluster if the first cluster is down. And if accessed with another browser/computer, chances are it will show the other 3 nodes). 

## Prerequisite
MetalLB is required to be installed and configured on all clusters before deploying these.

## Usage
1. Add the label `cluster: one` or `cluster: two` to each clusters
2. Create cluster group in `Continuous Delivery -> Cluster Groups` and add the clusters into the group
3. Create a new repo in `Continuous Delivery -> Git Repos`
4. Create an external load balancer pointing to external IPs of the traefik services in each clusters
5. Set a local DNS entry of hostname `primary.rancher.demo.test` and `secondary.rancher.demo.test`, both pointing to the external load balancer
6. Acces both hostnames, and verify that the deployment is working

## Cleanup
Just delete the repo in `Continuous Delivery -> Git Repos`
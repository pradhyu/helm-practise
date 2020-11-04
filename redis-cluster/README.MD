# installing bitnami chart for redis in microk8s
## github url
https://github.com/helm/charts/tree/master/stable/redis

## uninstall
helm uninstall my-release

## disabling persistence to start the service as had issues start it with persistence
helm install my-release   --set password=secretpassword   --set master.persistence.enabled=false --set slave.persistence.enabled=false  bitnami/redis

## installing with persistence for sentinel deployment
microk8s enable storage
helm install my-release   --set password=secretpassword --set sentinel.enabled bitnami/redis 

```
Single node - The basic solution where you run single process running Redis. It is not scalable and not highly available.
Redis Sentinel - Deployment that consist of multiple nodes where one is elected as master and the rest are slaves. It adds high availability since in case of master failure one of the slaves will be automatically promoted to master. It is not scalable since the master node is the only node that can write data. You can configure the clients to direct read requests to the slaves, which will take some of the load from the master. However, in this case slaves might return stale data since they replicate the master asynchronously.
Redis Cluster - Deployment that consist of at least 6 nodes (3 masters and 3 slaves). where data is sharded between the masters. It is highly available since in case of master failure, one of his slaves will automatically be promoted to master. It is scalable since you can add more nodes and reshard the data so that the new nodes will take some of the load.
```


#
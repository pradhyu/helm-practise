# installing bitnami chart for redis in microk8s
## github url
https://github.com/bitnami/charts/tree/master/bitnami/redis

## uninstall
helm uninstall rds

## installing with persistence for cluster mode
microk8s enable storage
helm uninstall rds
helm install rds --set password=secretpassword --set cluster.enabled=true bitnami/redis 

# issue with slave master host value 
## REDIS_MASTER_HOST is set to something that's not master hmm. 
### the stateful set is not making sense 
https://github.com/bitnami/charts/blob/master/bitnami/redis/templates/redis-slave-statefulset.yaml
```
[centos@centos8 helm-practise]$ kubectl exec -it rds-redis-slave-0 -- /bin/bash
I have no name!@rds-redis-slave-0:/$ redis-cli  -h localhost -a secretpassword ping
Warning: Using a password with '-a' or '-u' option on the command line interface may not be safe.
PONG
```

Single node - The basic solution where you run single process running Redis. It is not scalable and not highly available.
Redis Sentinel - Deployment that consist of multiple nodes where one is elected as master and the rest are slaves. It adds high availability since in case of master failure one of the slaves will be automatically promoted to master. It is not scalable since the master node is the only node that can write data. You can configure the clients to direct read requests to the slaves, which will take some of the load from the master. However, in this case slaves might return stale data since they replicate the master asynchronously.

Redis Cluster - Deployment that consist of at least 6 nodes (3 masters and 3 slaves). where data is sharded between the masters. It is highly available since in case of master failure, one of his slaves will automatically be promoted to master. It is scalable since you can add more nodes and reshard the data so that the new nodes will take some of the load.
```


#

# some details from the artifact hub 
https://artifacthub.io/packages/helm/bitnami/redis
Choose between Redis Helm Chart and Redis Cluster Helm Chart
You can choose any of the two Redis Helm charts for deploying a Redis cluster. While  will deploy a master-slave cluster using Redis Sentinel, the  will deploy a Redis Cluster topology with sharding. The main features of each chart are the following:

Redis Cluster
Supports multiple databases	Supports only one database. Better if you have a big dataset
Redis	
Single write point (single master)	Multiple write points (multiple masters)

# installing bitnami chart 
helm uninstall my-release

## disabling persistence to start the service as had issues start it with persistence
helm install my-release   --set password=secretpassword   --set master.persistence.enabled=false --set slave.persistence.enabled=false  bitnami/redis

## installing with persistence
helm install my-release   --set password=secretpassword bitnami/redis

#
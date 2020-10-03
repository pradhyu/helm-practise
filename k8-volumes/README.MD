# doco : https://www.alibabacloud.com/blog/kubernetes-volume-basics-emptydir-and-persistentvolume_594834

# notes
## create pod
kubectl create -f myVolumes-Pod.yaml

## exec in pod and do stuff
kubectl exec myvolumes-pod -i -t -- /bin/sh
echo test > demo/textfile
cat demo/textfile
exit

## delete pod forcefully
kubectl delete -f myVolumes-Pod.yaml --force --grace-period=0



# myVolumes-3Pods.yaml
kubectl create -f myVolumes-3Pods.yaml

kubectl exec myvolumes-pod -c myvolumes-container-1 -i -t -- /bin/sh
echo test1 > demo1/textfile1
exit
kubectl exec myvolumes-pod -c myvolumes-container-1 -i -t -- cat demo1/textfile1
kubectl exec myvolumes-pod -c myvolumes-container-1 -i -t -- ls -l /
kubectl exec myvolumes-pod -c myvolumes-container-1 -i -t -- ls -l /demo1

kubectl exec myvolumes-pod -c myvolumes-container-2 -i -t -- /bin/sh
echo test2 > demo2/textfile2
exit

kubectl exec myvolumes-pod -c myvolumes-container-2 -i -t -- cat demo1/textfile1
kubectl exec myvolumes-pod -c myvolumes-container-2 -i -t -- cat demo2/textfile2
kubectl exec myvolumes-pod -c myvolumes-container-2 -i -t -- ls -l /


## volume 3 has all  it's jst the different name
kubectl exec myvolumes-pod -c myvolumes-container-3 -i -t -- ls -l /demo3

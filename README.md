# k8s-volumes-nfs
Kubernetes manifests for nfs-provisioning-client, related objects as well as sample deployment to test the scenario

# Example #1

First PVC and corresponding application pod writing to the PVC
```
test-claim.yaml
test-pod.yaml
```
On the NFS server you should see:
```
[root@localhost nfs-root-dynamic]# ls /var/spool/nfs-root-dynamic/ -l
drwxrwxrwx. 2 root root 37 Mar 25 13:08 default-test-claim-pvc-b2ce634a-5825-4397-b04e-828d2362b444
```
# Example #2

Second PVC and corresponding application pod writing to the PVC
```
test-another-claim.yaml
test-another-pod.yaml
```
On the NFS server's exports directory:
```
[root@localhost nfs-root-dynamic]# ls /var/spool/nfs-root-dynamic/ -l
drwxrwxrwx. 2 root root 37 Mar 25 13:08 default-test-claim-pvc-b2ce634a-5825-4397-b04e-828d2362b444
drwxrwxrwx. 2 root root 25 Mar 25 14:12 default-test-another-claim-pvc-bf1182b2-5b4a-4539-b504-1a63a9a4438f
```

# Example #3 - utilizing default StorageClass functionality 

Third PVC created WITHOUT any StorageGroup defined and corresponding application pod writing to the PVC
Mark an existing StorageClass as a default class. In this case the PVC is created using the default StorageClass.
```
test-claim-no-sc-specified.yaml
test-pod-using-default-sc.yaml
```
To mark any existing Kubernetes StorageClass as default, use:
```
kubectl patch storageclass managed-nfs-storage -p '{"metadata": {"annotations":{"storageclass.kubernetes.io/is-default-class":"true"}}}'

[root@master ~]# kubectl get sc
NAME                            PROVISIONER                      AGE
managed-nfs-storage (default)   demo.local-nfs-provisioner/nfs   75m
```
On the NFS server's exports directory:
```
[root@localhost nfs-root-dynamic]# ls /var/spool/nfs-root-dynamic/ -l
drwxrwxrwx. 2 root root 37 Mar 25 13:08 default-test-claim-pvc-b2ce634a-5825-4397-b04e-828d2362b444
drwxrwxrwx. 2 root root 25 Mar 25 14:12 default-test-another-claim-pvc-bf1182b2-5b4a-4539-b504-1a63a9a4438f
drwxrwxrwx. 2 root root 36 Mar 25 14:24 default-test-claim-no-sc-specified-pvc-3246f8e5-2d7b-424c-824b-93794e9c1376
```








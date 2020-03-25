# k8s-volumes-nfs
Kubernetes manifests for nfs-provisioning-client, related objects as well as sample deployment to test the scenario

# Example #1

First PVC and corresponding application pod writing to the PVC
'''
test-claim.yaml
test-pod.yaml
'''
On the NFS server you should see:
'''

'''
# Example #2

Second PVC and corresponding application pod writing to the PVC
'''
test-another-claim.yaml
test-another-pod.yaml
'''

# Example #3 - utilizing default StorageClass functionality 

Third PVC created WITHOUT any StorageGroup defined and corresponding application pod writing to the PVC
Mark an existing StorageClass as a default class. In this case the PVC is created using the default StorageClass.
'''
test-claim.yaml
test-pod.yaml
'''






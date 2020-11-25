
# Problemas para acceder al cluster de AWS

## error
```
kubectl get nodes
```
result:
```
Error from server (Forbidden): nodes is forbidden: User "arn:aws:iam::828839038281:user/blazed" cannot list resource "nodes" in API group "" at the cluster scope
```

## Commands 

### obtener session token
```
aws --region us-east-2 eks get-token --cluster-name blazedcloud-dev-cluster
```
result: 
```
{"kind": "ExecCredential", "apiVersion": "client.authentication.k8s.io/v1alpha1", "spec": {}, "status": {"expirationTimestamp": "2020-08-19T08:29:06Z", "token": "k8s-aws-v1.aHR0cHM6Ly9zdHMudXMtZWFzdC0yLmFtYXpvbmF3cy5jb20vP0FjdGlvbj1HZXRDYWxsZXJJZGVudGl0eSZWZXJzaW9uPTIwMTEtMDYtMTUmWC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBNEI2VklCVkVXQjJNRDI2MiUyRjIwMjAwODE5JTJGdXMtZWFzdC0yJTJGc3RzJTJGYXdzNF9yZXF1ZXN0JlgtQW16LURhdGU9MjAyMDA4MTlUMDgxNTA2WiZYLUFtei1FeHBpcmVzPTYwJlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCUzQngtazhzLWF3cy1pZCZYLUFtei1TaWduYXR1cmU9MmY4ZjYzMDgwNjk5ZGIyNDRiN2Y5NTM2NzE5OGQ5NjU1OTI5ZWEzZDRmYmUzYzMxZDVkZGVlZGQwNjMzYThkYg"}}
```

### listar cluster de aws
```
eksctl get cluster
```
result:
```
NAME                    REGION
blazedcloud-dev-cluster us-east-2
```
### listar nodegroups
```
eksctl get nodegroups --cluster blazedcloud-dev-cluster
```
result:
```
CLUSTER                 NODEGROUP               CREATED                 MIN SIZE        MAX SIZE        DESIRED CAPACITY        INSTANCE TYPE   IMAGE ID
blazedcloud-dev-cluster mixed-instances         2020-07-09T10:07:03Z    3               20              3                       t2.medium       ami-0ce799fcbc744c156
blazedcloud-dev-cluster mixed-instances-c5      2020-08-17T15:07:51Z    2               20              2                       c5.2xlarge      ami-012f5805740ae1de2
```

### get identity
```
aws sts get-caller-identity
```
result:
```
{
    "UserId": "AIDA4B6VIBVEZE3LKYAPX",
    "Account": "828839038281",
    "Arn": "arn:aws:iam::828839038281:user/blazed"
}
```


### update kubeconfig
```
aws eks --region us-east-2 update-kubeconfig --name blazedcloud-dev-cluster
```
result:
```
Updated context arn:aws:eks:us-east-2:828839038281:cluster/blazedcloud-dev-cluster in /home/sysadmin/.kube/config
```

eksctl get nodegroups --cluster blazedcloud-dev-cluster

eksctl get iamserviceaccount --cluster blazedcloud-dev-cluster
eksctl get iamidentitymapping --cluster blazedcloud-dev-cluster





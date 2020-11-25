

# lista los pods en el namespace
kubectl get pods -n interactions

# lista servicios
kubectl get svc -n interactions -o wide

# describe un servicio
kubectl describe svc labengine-msengine

# para ingresar al pod
kubectl exec -it labengine-msinteractionrepository-64b48f56c4-frl6z /bin/bash -n interactions
//una vez dentro ejecutar printenv  para ver las variables de entorno.
printenv 

# trabajar con kubeconfig
kubectl get svc --kubeconfig ../kubeconfig.yaml 
kubectl get pods --kubeconfig ../kubeconfig.yaml 
kubectl describe svc app-bession-server --kubeconfig ../kubeconfig.yaml
kubectl describe pods app-bession-server-677f5f4b64-vdn84  --kubeconfig ../kubeconfig.yaml 
kubectl logs app-bession-server-677f5f4b64-vdn84  --kubeconfig ../kubeconfig.yaml

# borra todo del namespace
kubectl delete all --all --namespace=blazed --kubeconfig ../kubeconfig.yaml

kubectl delete all --all --namespace=client-000002
 


# get info
https://kubernetes.io/docs/reference/kubectl/cheatsheet/

# metrics

## quotas por namespace
kubectl get quota -n company-dev-blazedpath-1 -ojson
kubectl get quota --all-namespaces -l blazedEnv=dev,companyCode=blazedpath,environmentId=1 -ojson

kubectl get quota --all-namespaces -l companyCode=blazed -ojson


## pods de todos los namespaces por compania
kubectl get pods --all-namespaces -l blazedEnv=dev,companyCode=2

## pods de todos los namespaces por compania , salida completa por json 
kubectl get pods --all-namespaces -l blazedEnv=dev,companyCode=2 -o json

## pods por comoania y environments
kubectl get pods --all-namespaces -l blazedEnv=dev,companyCode=2,environmentId=3 

## namespace por comoania y environments
kubectl get namespace --all-namespaces -l blazedEnv=dev,companyCode=2,environmentId=3 

## pods por comoania, environments y solution
kubectl get pods --all-namespaces -l blazedEnv=dev,companyCode=2,environmentId=3,solutionId=2 

## listar todos los recursos 
kubectl get all  --all-namespaces -l blazedEnv=dev,companyCode=2,environmentId=3,solutionId=2 

## listar todos los recursos mostrando algunas columnas
kubectl get all  --all-namespaces -l blazedEnv=dev,companyCode=2,environmentId=3,solutionId=2 -o custom-columns=NAME:.metadata.name,TYPE:.kind,RSRC:.metadata.resourceVersion 

## Detener un pods
kubectl scale --replicas=0 deployment/solution-2-myfrontend -n company-2-3

## Listar Config VolumesClaim  Volumes, Deployments, Services, Ingress por solucion
kubectl get ingress --all-namespaces -l blazedEnv=dev,companyCode=blazed,environmentId=dev,solutionId=blzcloud
kubectl get service --all-namespaces -l blazedEnv=dev,companyCode=blazed,environmentId=dev,solutionId=blzcloud
kubectl get deployment --all-namespaces -l blazedEnv=dev,companyCode=blazed,environmentId=dev,solutionId=blzcloud 
kubectl get persistentvolume --all-namespaces -l blazedEnv=dev,companyCode=blazed,environmentId=dev,solutionId=blzcloud
kubectl get persistentvolumeclaim --all-namespaces -l blazedEnv=dev,companyCode=blazed,environmentId=dev,solutionId=blzcloud
kubectl get secret --all-namespaces -l blazedEnv=dev,companyCode=blazed,environmentId=dev,solutionId=blzcloud
kubectl get configmap --all-namespaces -l blazedEnv=dev,companyCode=blazed,environmentId=dev,solutionId=blzcloud

## Get Info
kubectl get deployment --all-namespaces -l blazedEnv=dev,companyCode=1,environmentId=1,solutionId=2 -o json
kubectl get ingress --all-namespaces -l blazedEnv=dev,companyCode=1,environmentId=1,solutionId=2 -o json

## Eliminar un pod
kubectl delete pods solution-2-myfrontend-5997ddd856-5pfgq --grace-period=0 --force -n company-2-3

## list history deployments 
kubectl rollout history deploy blzcloud-apicloud  -n blazed-dev -o json
## List Replicasets por deployment
kubectl get replicaset -l app.kubernetes.io/version=20201019-02,app.kubernetes.io/name=blzcloud-apicloud -n blazed-dev -o json 
## Rollback deployments
kubectl rollout undo deploy blzcloud-apicloud -n blazed-dev --to-revision=3




# crear service account
kubectl create sa blzcluster-deployer

# obtener el yaml del service account
kubectl get sa blzcluster-deployer -o yaml

# obtener el token del service account creado
kubectl get secrets blzcluster-deployer-token-rnvzz -o yaml

# port forward 
kubectl port-forward service/minioclients-blzcloud -n blazed 9000:9000

# ingresar a pod
kubectl exec -n blazed  --stdin --tty msdeployer-blzcloud-86d4c4bffd-pk56p -- /bin/bash

# create ClusterRoleBinding


blzcluster-deployer-token-secret

# get current context
(kubectl config current-context)
result: minikube

# get cluster name of context
(kubectl config get-contexts $c | awk '{print $3}' | tail -n 1)
result: minikube

# get endpoint of current context 
(kubectl config view -o jsonpath="{.clusters[?(@.name == \"minikube\")].cluster.server}")

result: https://10.0.2.15:8443

=======
result: 
    mv   =  https://10.0.2.15:8443
    wiki =  https://192.168.102.113:8443


# create image pull secert

kubectl create secret docker-registry aws-registry-secret --docker-server=828839038281.dkr.ecr.us-east-2.amazonaws.com --docker-username=AWS --docker-password=eyJwYXlsb2FkIjoiNmJJK3llenI1RWFWRW90MFVmOWkxUkJQT3UvYWdSbHVoRjhpNi9wK3JOSFVrbkZ4cERaUEo0M2FwQ05lYStrV3NDR2FBbUF4ZUZLaXBKaGx2MEl0Q0FvN3d2eTNMRGxJNnVKNXRWdllyNnU2UlYyMzlpOWM4UjhuOE9SK0x2SUhBRUM4M01YYTd3ZEV1UlFpbVhFSlB0Uk05cENTVjFpY1dkQ0RxNHZEQ3F4T0h3dm5mekRhR29sQmpxd0lrbWRmdC85QWI2RThVSkt3U1RJWUVkZ0YvRmVvcWxMb0RUV0NYNXBrQzRMcmIyeGk1Tk1uNVZ2aEhDVU5FMXlzMDNCemNERzhqYy93Q1JJQnlXOVNsRnNsVC9CTE4rY2JZRFFwSEpBaXpCWkREajhyK3N6dGpLUUxheEpZOTR1Y0EzRFdGcWhyMWZ2dkpZV04zV2Qvd2lucFpheEpRSmhkUTFRcHB4SjU1QW9lNVFIbitkS3JGbDNGQmxCVEFZOFlRSW1jcWdWUnRYRWUwdkd0TFMvUWZUTUMvZjJTQVFlSzJjc3Y5NUtvaU1uNnBMTXIrbGUvSUd0MHE3UVNKT1JyYndmWlVUQWM0YzJJMHVrc29hbERyZ1NUbzBkc2VoVmpnMytnV2FoVXRyTHJTaFc2RGVNTUFMUDZYL0pGK2Y4ekhRRW1jOXhSTG5yZWY1MVpsTmJ5aW5tZklxeHdZc3R2WHMzVVhvcnNFbHJhVGtyNExKTldCN2dwbE00c1MxUEpBY0xqL0lUT1k4a1lyZnU0ZkZEd25EWXlsR2VHN056Tjh6UDd1d2Z5dHZ2eDhwMno1czBnamdOekRQemZaMDV4Y2JZQytIa29CcUlFczhHTEFWbEpjL1B1RGJEQWVWVXVWUXoxZzJBL0xkdUhmNEUvMXdBbGNoVU8zbzRVMWgwY1VhTlFjc2JESUNFK3VrWTBnVDJOSzBMSTFuTlcyc2w5YUdCZEg4VEF4Z01HWmsvSkhQK2lHbGhZVXMvZmc5cmRYakNKV2RDZFE0QmUrdHl2b2d4RFJwZFd2TnlUQjZucXAzdDN4VkREdXRxSlV4cVFFUWljSjhFUEpvb3RhNk5odGloRXRtUHMxMm1DZUs2YlhwUUNEV2t3ZjZDUmNnVXJnOFpEWVExeGZRcHBoOWI1aTZxVzhjdHBQUklsM29PMjlMZ29MVmNCMlVFWEdTQ3ozVXd4bkI4akRsMDZJSy9OUnhBQjNhT01ka1R4Zm5HbnVFajhKemZabUZVMHNKRkZQWU9LSjUzSkxZditnZ2JydTlMcFlveFZOWFNrTUROc0RUelJtemY4UmNTem9rSEpIYjFxRUVMWTZDai90ZS9ENmUydjIzUG9HYWh5bEtSQXZ4VEpYSEh4UVNmaktweFRQNDd2RVd2dzFQS05OTmJZM1VFZ3MrK3AxbVMyL05ZVVQwUzY1cXZzUkxyTStrdmVPWGhXeU1MV0JPKy9XUG95azBwUWJlaHR2aTFDUEdHSDAyTEQrNW05MDlPb2IxdHpiVWlFK2dTc0lRRWVWZ1JBZ0E9PSIsImRhdGFrZXkiOiJBUUVCQUhqQjcvaWd3TWc0TlB3YXVyeFNJWXg0SGZueHVHYy80OGJEd3Z3RHBOWVdaZ0FBQUg0d2ZBWUpLb1pJaHZjTkFRY0dvRzh3YlFJQkFEQm9CZ2txaGtpRzl3MEJCd0V3SGdZSllJWklBV1VEQkFFdU1CRUVESk9tdW5GSHloREpibmlWbXdJQkVJQTdoSHNNQ2lUMzdvVVRXazFiSktDSzRTVzVQajZIcGlzb2lya0FMRHM4dEtBcHJXVFhrdlduenlqZ0M5L2pUbjQ2QUhzOUUzTmdPdi80L01nPSIsInZlcnNpb24iOiIyIiwidHlwZSI6IkRBVEFfS0VZIiwiZXhwaXJhdGlvbiI6MTU5NDg0MzQ5MX0= --docker-email=frita@beesion.com

//si ya existe se puede eliminar con 
kubectl delete secret aws-registry-secret
//para obtener el yaml
kubectl get secret aws-registry-secret -o yaml


# port foawrd 
// para poder probar temporalmente

kubectl port-forward service/minioclients-blzcloud 59001:9000 --context arn:aws:eks:us-east-2:828839038281:cluster/blazedcloud-dev-cluster

kubectl port-forward service/minioblazed-blzcloud 59000:9000 --context arn:aws:eks:us-east-2:828839038281:cluster/blazedcloud-dev-cluster

kubectl port-forward service/webauth-blzauth 10001:10001 --context arn:aws:eks:us-east-2:828839038281:cluster/blazedcloud-dev-cluster

kubectl port-forward service/mysql 33060:33060 --context arn:aws:eks:us-east-2:828839038281:cluster/blazedcloud-dev-cluster

# listar los nodes de aws 
kubectl get nodes --show-labels  --context arn:aws:eks:us-east-2:828839038281:cluster/blazedcloud-dev-cluster

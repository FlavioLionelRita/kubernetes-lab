

sum(node_namespace_pod_container:container_cpu_usage_seconds_total:sum_rate{cluster="arn:aws:eks:us-east-2:828839038281:cluster/blazedcloud-dev-cluster", namespace="blazed-dev"}) by (pod)


container_memory_usage_bytes{alpha_eksctl_io_cluster_name="blazedcloud-dev-cluster",alpha_eksctl_io_instance_id="i-012130411105030f2",alpha_eksctl_io_nodegroup_name="mixed-instances",beta_kubernetes_io_arch="amd64",beta_kubernetes_io_instance_type="c5.2xlarge",beta_kubernetes_io_os="linux",failure_domain_beta_kubernetes_io_region="us-east-2",failure_domain_beta_kubernetes_io_zone="us-east-2c",id="/",instance="ip-10-0-6-20.us-east-2.compute.internal",job="kubernetes-nodes-cadvisor",kubernetes_io_arch="amd64",kubernetes_io_hostname="ip-10-0-6-20.us-east-2.compute.internal",kubernetes_io_os="linux",nodegroup_type="mixed-instances"}


sum(rate(container_cpu_usage_seconds_total{container_name!="POD",pod_name!=""}[5m]))

sum(rate(container_cpu_usage_seconds_total{container_name!="POD",pod_name!=""}[5m])) by (container_name)


container_cpu_usage_seconds_total{alpha_eksctl_io_cluster_name="blazedcloud-dev-cluster",alpha_eksctl_io_instance_id="i-012130411105030f2",alpha_eksctl_io_nodegroup_name="mixed-instances",beta_kubernetes_io_arch="amd64",beta_kubernetes_io_instance_type="c5.2xlarge",beta_kubernetes_io_os="linux",cpu="total",failure_domain_beta_kubernetes_io_region="us-east-2",failure_domain_beta_kubernetes_io_zone="us-east-2c",id="/",instance="ip-10-0-6-20.us-east-2.compute.internal",job="kubernetes-nodes-cadvisor",kubernetes_io_arch="amd64",kubernetes_io_hostname="ip-10-0-6-20.us-east-2.compute.internal",kubernetes_io_os="linux",nodegroup_type="mixed-instances"}


sum(rate(kube_resourcequota{namespace="blazed"}[4w]))

kube_resourcequota{app_kubernetes_io_instance="blz-prometheus",app_kubernetes_io_managed_by="Helm",app_kubernetes_io_name="kube-state-metrics",helm_sh_chart="kube-state-metrics-2.8.14",instance="192.168.68.120:8080",job="kubernetes-service-endpoints",kubernetes_name="blz-prometheus-kube-state-metrics",kubernetes_namespace="monitoring",kubernetes_node="ip-10-0-5-68.us-east-2.compute.internal",namespace="blazed",resource="memory",resourcequota="pods-low",type="hard"}



## Range Vectors
Example:  rate(container_cpu_usage_seconds_total{container_name!="POD",namespace="blazed"}[1w])
puede usar (s, m, h, d, w, y) para representar (segundos, minutos, horas, ...) respectivamente.

- offset : 
  - example: sum(rate(http_requests_total[5m] offset 5m))

## funtions

- rate: promedio
- irate : irate usa solo dos últimos puntos de datos en cada intervalo entre píxeles subsiguientes (también conocido como paso), mientras que la tasa calcula la tasa promedio por segundo en todos los puntos de datos en cada intervalo
- increase: incrementa
    

## aggregation expression
  - sum  
  - min
  - max
  - avg
  - count
  - quantile

# listado de consumo de CPU agrupado por namespaces
sum(rate(container_cpu_usage_seconds_total{container_name!="POD",namespace!=""}[1d])) by (namespace)

# consumo de CPU por namespace
sum(rate(container_cpu_usage_seconds_total{container_name!="POD",namespace="blazed"}[1h]))

sum(irate(container_cpu_usage_seconds_total{container_name!="POD",namespace="blazed"}[1h]))

# consumo de CPU por aplicacion en namespace
sum(rate(container_cpu_usage_seconds_total{container_name!="POD",namespace="blazed-dev",pod=~"blzcloud.*"}[1h]))



sum(rate(container_cpu_usage_seconds_total{container_name!="POD",namespace="blazed"}[1h])) by (namespace)

sum(rate(container_cpu_usage_seconds_total{container_name!="POD",namespace="blazed-dev",pod=~"blzcloud.*"}[1h]))



container_cpu_usage_seconds_total{container_name!="POD",namespace="blazed"}

container_cpu_usage_seconds_total{container_name!="POD",namespace="blazed",pod=~"*nexus*"}

"\/nexus-blzcloud-\/\*"

container_cpu_usage_seconds_total{alpha_eksctl_io_cluster_name="blazedcloud-dev-cluster",alpha_eksctl_io_instance_id="i-012130411105030f2",alpha_eksctl_io_nodegroup_name="mixed-instances",beta_kubernetes_io_arch="amd64",beta_kubernetes_io_instance_type="c5.2xlarge",beta_kubernetes_io_os="linux",cpu="total",failure_domain_beta_kubernetes_io_region="us-east-2",failure_domain_beta_kubernetes_io_zone="us-east-2c",id="/kubepods/burstable/poda0a41303-d380-46f0-9a99-24ce9ce4f760",instance="ip-10-0-6-20.us-east-2.compute.internal",job="kubernetes-nodes-cadvisor",kubernetes_io_arch="amd64",kubernetes_io_hostname="ip-10-0-6-20.us-east-2.compute.internal",kubernetes_io_os="linux",namespace="blazed",nodegroup_type="mixed-instances",pod="nexus-blzcloud-5bf6ddd84b-nztsg"}
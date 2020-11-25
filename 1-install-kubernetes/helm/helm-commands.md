
helm uninstall testcontrols-webapp


helm upgrade --install app-bession helm-chart --set image=flaviolionelrita/app-beesion:test --set customVar='!!Bession!!' --kubeconfig ../kubeconfig.yaml
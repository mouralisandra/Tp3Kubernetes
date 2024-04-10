kubectl apply -f deployment.yml
kubectl apply -f frontend-service.yml
kubectl apply -f backend-service.yml
kubectl port-forward frontend-service 8011:80
kubectl port-forward backend-service 8012:80

get pods
kubectl get deployments
get service my-app
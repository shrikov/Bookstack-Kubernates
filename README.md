Deployment Instructions

Step 1: Apply Persistent Volumes First
kubectl apply -f k8s/persistent-volumes/bookstack-local-pv.yaml
kubectl apply -f k8s/persistent-volumes/mariadb-local-pv.yaml
kubectl get pv

Step 2: Create Namespace
kubectl apply -f k8s/namespaces/namespace.yaml

Step 3: Apply Persistent Volume Claims
kubectl apply -f k8s/persistent-volumes/bookstack-pvc.yaml
kubectl apply -f k8s/persistent-volumes/mariadb-pvc.yaml
kubectl get pvc -n bookstack

Step 4: Apply Sealed Secret
kubectl apply -f k8s/sealed-secrets/sealed-secret.yaml

# Wait a few seconds for decryption
kubectl get secrets -n bookstack

Step 5: Deploy MariaDB
kubectl apply -f k8s/deployments/mariadb-deployment.yaml
kubectl apply -f k8s/services/mariadb-service.yaml

Step 6: Deploy BookStack
kubectl apply -f k8s/deployments/bookstack-deployment.yaml
kubectl apply -f k8s/services/bookstack-service.yaml


Step 7: Apply Ingress
kubectl apply -f k8s/ingresses/ingress.yaml
kubectl get pods -n bookstack

# Check all services
kubectl get svc -n bookstack

# Check PVC binding
kubectl get pvc -n bookstack

Step 9: Get Ingress IP and Access BookStack
kubectl get ingress -n bookstack

# Update your DNS to point bookstack.yourdomain.com to this IP
Access BookStack
Once deployed, access BookStack at: https://bookstack.yourdomain.com

Default Credentials:
Email: admin@admin.com
Password: password

# Push to GitHub
git push origin main

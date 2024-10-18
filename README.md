cat <<EOF > README.md
# Helm Chart Deployment with Minikube

This README walks through deploying an Nginx application using a Helm chart on a Minikube Kubernetes cluster, covering steps from chart creation, modification, deployment, scaling, and rollback.

### Prerequisites
- Minikube is installed and running.
- Helm is installed on your system.

### Steps to Deploy Nginx Application:

1. **Create a Helm Chart**:
   \`\`\`bash
   helm create my-web-app
   \`\`\`

2. **Modify \`values.yaml\`** to configure the application:
   \`\`\`yaml
   replicaCount: 3 # Scale to 3 replicas
   image:
     repository: nginx
     tag: "latest" # Use the latest version of Nginx
     pullPolicy: IfNotPresent
   \`\`\`

3. **Deploy the Helm Chart**:
   Navigate to the parent directory of the \`my-web-app\` folder and run:
   \`\`\`bash
   helm install my-nginx ./my-web-app
   \`\`\`

4. **Verify the Deployment**:
   Check the running pods and services:
   \`\`\`bash
   kubectl get pods
   kubectl get svc
   \`\`\`

5. **Scale the Application**:
   Update the replica count in \`values.yaml\` and apply the changes:
   \`\`\`yaml
   replicaCount: 1
   \`\`\`
   Upgrade the release to apply the new replica count:
   \`\`\`bash
   helm upgrade my-nginx ./my-web-app
   \`\`\`

6. **Rollback the Release**:
   If needed, roll back to a previous release version:
   \`\`\`bash
   helm rollback my-nginx 1
   \`\`\`

7. **Clean Up**:
   Uninstall the release and remove all associated resources:
   \`\`\`bash
   helm uninstall my-nginx
   \`\`\`


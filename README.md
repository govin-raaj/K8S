# Kubernetes Projectflow

## Prerequisites

1. **Docker Desktop**: Ensure Docker Desktop is installed and running.
2. **Docker Hub**: Sign in to Docker Hub.
3. **Minikube**: Install Minikube.

---

## Steps taken

### **1. Build the Application**
1. Create or use an existing application.
2. Test it locally to ensure it works as expected.

---

### **2. Prepare and Build the Docker Image**

1. Create a `Dockerfile` in your project directory.
2. Build the Docker image:
   ```bash
   docker build -t kubernetes-test-app:latest .
   ```
3. Verify the image:
   ```bash
   docker images
   ```
4. Test the image locally:
   ```bash
   docker run -p 5000:5000 kubernetes-test-app:latest
   ```

---

### **3. Create the Deployment YAML File**
Define a Kubernetes deployment in a file named `deployment.yaml`.

---

### **4. Install Minikube**
Installed the minikube via powershell command available on site.

Start Minikube:
```bash
minikube start
# or
minikube start --embed-certs
```

---


### **5. Verify Minikube Status**

Check the status of the Minikube cluster:
```bash
minikube status
```

Verify Kubernetes resources:
```bash
kubectl get all -A
kubectl get pods -A
kubectl get nodes -A
```

---

### **6. Adding Nodes**

To add a new node to the cluster:
```bash
minikube start --nodes=2
# or
minikube start --nodes=2 --embed-certs
```

---

### **7. Load Docker Image to Minikube**

1. Verify the Docker images:
   ```bash
   minikube image list
   docker images
   ```
2. Load the Docker image into Minikube:
   ```bash
   minikube image load kubernetes-test-app:latest
   ```

---

### **8. Apply Deployment**

Deploy the application:
```bash
kubectl apply -f deployment.yaml
```

To delete the deployment (if needed):
```bash
kubectl delete deployment kubernetes-test-app
```

---

### **9. Test the Application**

1. Check Pods and Nodes:
   ```bash
   kubectl get pods -A
   kubectl get nodes -A
   ```

2. Delete a specific Pod (optional):
   ```bash
   kubectl delete pod <pod-name/id>
   ```

3. Access the application service:
   ```bash
   minikube service kubernetes-test-app
   ```

4. Open the Minikube dashboard:
   ```bash
   minikube dashboard
   ```

---

### **10. Debugging and Logs**

- View Pod logs:
  ```bash
  kubectl logs -f <pod-id>
  ```

- Check Endpoints and Services:
  ```bash
  kubectl get endpoints
  kubectl get service
  ```

---

### **11. Load Testing with Postman**

1. Use Postman to run performance tests:
   - Go to **Collection > Runs > Performance > Run Performance Test**.
   - Example: Fixed configuration with 10 users for 1 minute.

---

### **12. Stop Minikube**

Stop the Minikube cluster:
```bash
minikube stop
```

---

### **13. Handling ImagePullBackOff Issue**

If you encounter the `ImagePullBackOff` error:

1. Tag the Docker image with your Docker Hub username:
   ```bash
   docker tag kubernetes-test-app:latest <your-dockerhub-username>/kubernetes-test-app:latest
   ```
2. Push the image to Docker Hub:
   ```bash
   docker push <your-dockerhub-username>/kubernetes-test-app:latest
   ```

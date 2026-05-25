**Kubernetes Blue-Green Deployment Lab (Minikube)**

**📌 Overview**

This project demonstrates a production-style Blue-Green deployment strategy in Kubernetes using a single-cluster Minikube environment.

It simulates real-world application release behavior by running two identical environments:

Blue (NGINX - current production)
Green (Apache HTTP Server - new release candidate) Apache HTTP Server

Traffic is switched between environments using Kubernetes Service selectors.
**
CI/CD was implemented to automate the deployment process.

🎯 Objectives**
Simulate production-grade deployment strategy in Kubernetes
Implement Blue-Green deployment using Services and labels
Demonstrate safe traffic switching and rollback strategy
Understand trade-offs between Blue-Green, Rolling, and Canary deployments

**🧱 Architecture**
Users
↓
Kubernetes Service (Selector-based routing)
↓
Blue Deployment (NGINX) OR Green Deployment (Apache HTTPD)

Both environments run simultaneously inside a single Kubernetes cluster (Minikube).

**⚙️ Technologies Used**
Kubernetes
Minikube
NGINX
Apache HTTP Server NGINX
kubectl

CI/CD (GitHub Actions) to automate deployment

**📦 Deployment Strategy**
Blue Environment
NGINX deployment
Label: app=app-blue
Exposed via NodePort service

Green Environment
Apache HTTPD deployment
Label: app=app-green
Exposed via NodePort service

**🔄 Traffic Switching Mechanism**

Traffic routing is controlled using Kubernetes Service selectors:

selector:
app: app-blue

Switching to green:

selector:
app: app-green

This enables instant traffic redirection without downtime.

🧪 Key Commands Used

kubectl apply -f manifests/
kubectl get pods -n production
kubectl get svc -n production
kubectl delete deployment nginx-blue -n production
**
📸 Proof of Execution**

Screenshots included:

Pod creation and readiness
Service exposure via NodePort
Successful traffic switch from Blue → Green
Blue environment deletion after validation

**⚠️ Key Engineering Insights**

Blue-Green Tradeoffs
Requires duplicate infrastructure
Higher cost at scale
Risky for database schema changes
Why It’s Not Always Used in Production
No gradual rollout mechanism
High resource consumption
Instant 100% traffic switch increases blast radius

**🆚 Alternative Strategies**

Strategy | Strength
Rolling Deployment | Low cost, gradual rollout
Canary Deployment | Safer real-user testing
Blue-Green | Fast switch, instant rollback

**🧠 Key Learning Outcome**

This project demonstrates how Kubernetes abstracts deployment strategies using:

Labels + Service Selectors = Traffic Control Layer

**📁 How to Run This Project**

minikube start
kubectl apply -f manifests/namespace.yaml
kubectl apply -f manifests/
kubectl get all -n production

**👨‍💻 Author**

Tolulope Philip Olalere
Cloud & DevOps Engineer | AWS Enthusiast
Focused on Kubernetes, Cloud Security, and Scalable Infrastructure

**📌 Future Improvements**

Implement Canary deployment version
Add Ingress Controller instead of NodePort
# Instructions for Deploying and Validating Advanced Scheduling Rules

## 1. Automated Deployment
Execute the bootstrap script from the root directory to initiate cluster scaling and deployments:
```bash
./bootstrap.sh
```

---

## 2. Advanced Scheduling Validation

### Step 2.1: Verify Node Taints Presence
Ensure that worker nodes labeled with app=mysql successfully received the protection taint:
```bash
kubectl get nodes -o custom-columns=NAME:.metadata.name,TAINTS:.spec.taints
```

### Step 2.2: Verify MySQL StatefulSet Node Distribution
Validate that MySQL pods scaled properly and settled exclusively on the matching database nodes:
```bash
kubectl get pods -n mysql -o wide
```

### Step 2.3: Verify Deployment Anti-Affinity Rule
Check the distribution of the application pods to confirm they do not overlap on the same host system:
```bash
kubectl get pods -n mateapp -l app=todolist -o wide
```

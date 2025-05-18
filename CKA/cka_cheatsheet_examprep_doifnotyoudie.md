## 🚀 CKA Exam Prep Bootstrap Script (Speed & Survival Mode)

### 🔄 Persistent Aliases & Shortcuts

Add to `~/.bashrc` or run manually at start:

```bash
alias k='kubectl'                     # Short alias for kubectl
alias kgp='kubectl get pods'         # Get pods quickly
alias kgs='kubectl get svc'          # Get services
alias kgn='kubectl get nodes'        # Get nodes
alias kaf='kubectl apply -f'         # Apply YAML
alias kdf='kubectl delete -f'        # Delete from file
alias kctx='kubectl config use-context' # Switch context
alias kns='kubectl config set-context --current --namespace'  # Set default ns
alias kd='kubectl describe'          # Describe resource
alias ke='kubectl exec -it'          # Exec into pod
```

```bash
source ~/.bashrc                     # Reload after adding aliases
```

### 🧠 Set Current Namespace

```bash
kubectl config set-context --current --namespace=default  # Avoid repeated -n
```

### 🔍 Create Must-Use Vim Templates

Create starter files for YAML manifests:

```bash
echo "apiVersion: v1\nkind: Pod\nmetadata:\n  name: mypod\nspec:\n  containers:\n  - name: mycontainer\n    image: nginx" > pod.yaml  # Pod template

cp pod.yaml deploy.yaml          # Copy and edit for deployments
```

### 📁 Setup Workspace

```bash
mkdir -p ~/cka/tmp && cd ~/cka/tmp     # Temp dir for manifests
```

### 🧪 Dry Run Alias for Safe Testing

```bash
alias kdry='kubectl apply -f - --dry-run=client -o yaml'  # Validate YAML without applying
```

### 📚 Launch Docs and Cheatsheets

```bash
echo "https://kubernetes.io/docs" &    # Official docs
firefox https://kubernetes.io/docs/concepts/ &  # Open in browser (if allowed)
```

### 📊 Set Kubeconfig Context Explicitly (in case reset)

```bash
export KUBECONFIG=/etc/kubernetes/admin.conf  # Use admin kubeconfig
```

### 🧹 Vim Config Cleanup (Optional)

```bash
set number               # Line numbers
set tabstop=2            # Tab spacing
syntax on                # Syntax highlight
```

Add to `~/.vimrc` if time allows.

---

🔥 Final Note:

* Run all aliases and shortcuts on startup.
* Use templates for everything.
* Never write YAML from scratch during the exam.
* Use `k get <resource> -oyaml > file.yaml` as the fastest way to generate templates.

> "Speed is survival. Efficiency is life. YAML is pain—automate everything you can."

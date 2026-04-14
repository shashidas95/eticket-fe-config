
# ⚙️ E-Ticket Frontend Infrastructure (Config)

This repository manages the deployment environment and automated pipelines for the **E-Ticket Frontend**. It ensures the Vue.js/Next.js application is containerized, tagged, and deployed to Kubernetes clusters with zero manual intervention.

---

## 🏗️ Automated Deployment Logic

The core of this repository is the automated versioning and deployment logic. It handles the dynamic updating of Kubernetes manifests during the CI/CD process.

### **🛠️ Cross-Platform Deployment Scripting**
When running deployment scripts (like `sed`) on **macOS** during local testing or CI/CD, the BSD version of `sed` requires a specific syntax for in-place editing. 

**Updating Image Tags in K8s Manifests:**
To update the frontend image version without creating backup files, use the following command:

```sh
sed -i '' 's/eticket-fe.*/eticket-fe:20/g' ./k8s/deployment.yaml
```

* `-i ''`: Instructs the macOS `sed` engine to perform an in-place edit without generating a backup suffix.
* `'s/eticket-fe.*/eticket-fe:20/g'`: Replaces the existing image tag with the target version (e.g., version 20).

---

## 🏗️ DevOps Ecosystem

- **CI/CD Architecture**: Integrated Jenkins pipelines that trigger on code commits to `eticket-fe`.
- **Image Management**: Automated tagging logic ensures that the frontend build matches the specific deployment version.
- **Orchestration**: Kubernetes manifests for managing LoadBalancers, Ingress, and Frontend Pods.

---

## 📂 Configuration Assets

| Asset | Purpose |
| :--- | :--- |
| `/k8s/deployment.yaml` | Primary Kubernetes manifest for the frontend service. |
| `/jenkins/Jenkinsfile` | Declarative pipeline defining the Build-Push-Deploy stages. |
| `/scripts/update-version.sh` | Utility scripts for dynamic image tagging (macOS compatible). |

---

## 🚀 Deployment Pipeline

1.  **Build**: Frontend assets are compiled and packaged into a Docker image.
2.  **Tag**: The `sed` automation updates the `deployment.yaml` with the new image ID.
3.  **Deploy**: Kubernetes applies the updated manifest to the cluster for a rolling update.

---

## 👨‍💻 Author
**Shashi Kanta Das**
*Software Architect | DevOps Engineer | Assistant Director @ BSTI*

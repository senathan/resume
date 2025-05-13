## Welcome to GitHub Pages

You can use the [editor on GitHub](https://github.com/senathan/resume/edit/master/README.md) to maintain and preview the content for your website in Markdown files.

Whenever you commit to this repository, GitHub Pages will run [Jekyll](https://jekyllrb.com/) to rebuild the pages in your site, from the content in your Markdown files.

Here’s a comprehensive structure for your **Confluence deployment design document**, including:

1. **Deployment Overview**
2. **Pipeline Stage Breakdown**
3. **Branching & Release Strategy**
4. **Helm Folder Structure**
5. **Release Flow Diagram (non-pipeline)**
6. **Developer vs Release Process Differences**

---

## 🧩 1. Deployment Overview

This document outlines the deployment architecture for our GitLab-based CI/CD pipeline. It covers every stage from development to production, including build, test, security scans, and aPaaS deployments. The pipeline is parameterized and designed for flexibility and repeatability, integrating Vault secrets, Veracode, SonarQube, Nexus, and Helm.

---

## ⚙️ 2. Pipeline Stage Breakdown

### 🔐 Pre-Stage (Setup)

* Fetch variables and credentials from Vault (AD and KV secret engine)
* Set workflow context and GitLab cache
* Retrieve builder images

### 🏗️ Stage 1: Pre-Release

* **Checks if release version is passed** as a variable
* If not passed, **generates release version using Maven** (from API module)

```bash
mvn -f api/pom.xml build-helper:parse-version
```

---

### 🛠️ Stage 2: Build (Frontend + Backend)

* **Runs in parallel**
* **Frontend**

  * Node.js image
  * Creates `/dist` folder artifact
  * Generates Veracode artifact
* **Backend**

  * Java 21 image
  * JAR built under `/target`

---

### ✅ Stage 3: Unit Tests

* **Only backend** has JUnit tests currently
* Executed via `mvn test`

---

### 🔍 Stage 4: Security & Quality Scans

* **Secrets pulled from RMS**
* **Scans run in parallel**:

  * Veracode pipeline scan
  * Veracode SCA scan
  * SonarQube scan for backend
  * SonarQube scan for frontend

---

### 🐳 Stage 5: Docker Build & Push

* Login using system account
* Build Docker image (uses internal Nexus registry)
* Push to:

  ```
  docker.repo/project-name/release-version
  ```

---

### 📦 Stage 6: Nexus Publish

* Bundle frontend static assets inside backend JAR
* Set Maven release version
* Push to Nexus repository as `.jar`

---

### ☁️ Stage 7: aPaaS Dev Deployment (2 regions: UU & PI)

Runs in parallel per region

#### a. **Deploy**

* `oc login` to aPaaS with system account
* Create generic secrets (keystore/truststore)
* `helm upgrade --install`
* `oc wait` for pod readiness

#### b. **Test**

* Re-authenticate with `oc login`
* Check pod status
* Fail fast if pods crash or don't start

---

### 🚀 Stage 8: UAT Promote

* Log in to aPaaS
* Create generic secrets (basic auth for source/destination)
* Delete any existing jobs
* Apply deployment templates via `oc apply`
* Wait for completion

---

### 🌐 Stage 9: UAT Deploy

* Same as Stage 7 (Dev Deploy)

---

## 🌳 3. Branching & Release Strategy

| Activity         | Branch Type                     | Trigger                    | Deployment Target                        |
| ---------------- | ------------------------------- | -------------------------- | ---------------------------------------- |
| **Feature Work** | `feature/*`                     | Developer Push             | Does not deploy beyond Unit Test & Scans |
| **Release Cut**  | `release/*`                     | Lead triggers pipeline     | UAT (via pipeline)                       |
| **Hotfix**       | `hotfix/*`                      | Developer / Lead           | Same pipeline flow as release            |
| **Production**   | Manual Trigger (on `release/*`) | Lead triggers `prod` stage | aPaaS Production Environment             |

**Production Deployment Notes**:

* Manual approval required
* Same pipeline re-used
* Variables passed manually or picked from CI/CD config

---

## 🗂️ 4. Helm Template Folder Structure

```plaintext
helm/
  └── my-app/
      ├── charts/
      ├── templates/
      │   ├── deployment.yaml
      │   ├── service.yaml
      │   ├── configmap.yaml
      │   └── ingress.yaml
      ├── values.yaml
      └── Chart.yaml
```

* `templates/`: All Kubernetes manifests
* `values.yaml`: Contains env-specific configurations (ports, replicas, env vars)
* `Chart.yaml`: Helm chart metadata

---

## 🔄 5. High-Level Flow Diagram

A **non-pipeline flow diagram** representing the release lifecycle:

```plaintext
Developer Work
    ↓
Feature Branch Pushed
    ↓
Backend Unit Test + Scans (Sonar, Veracode)
    ↓
Lead Creates Release Branch
    ↓
Build & Docker Push to Nexus
    ↓
Deploy to aPaaS Dev (UU, PI)
    ↓
Run Smoke Tests on Dev
    ↓
Trigger UAT Promote Job
    ↓
Deploy to UAT
    ↓
Final Validation (Manual QA)
    ↓
Manual Trigger for Production
    ↓
Deploy to aPaaS Prod
```

---

## 🔄 6. Developer vs Lead Release Responsibility

| Responsibility             | Developer | Lead               |
| -------------------------- | --------- | ------------------ |
| Feature Branch Push        | ✅         | ❌                  |
| Local Testing              | ✅         | ❌                  |
| Trigger Release Cut        | ❌         | ✅                  |
| Trigger Manual Prod Deploy | ❌         | ✅                  |
| Hotfix Patch               | ✅         | ✅                  |
| Pipeline Debugging         | ✅         | ✅                  |
| Helm Value Changes         | ✅ (minor) | ✅ (final sign-off) |

---

Let me know if you’d like:

* Markdown export
* Flow diagram as a PNG/SVG
* Confluence-ready layout with collapsible sections

Would you like me to generate the **visual flow diagram now**?

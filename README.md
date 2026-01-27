# 🚀 CI/CD Templates for GitHub Actions

![GitHub Actions](https://img.shields.io/badge/GitHub_Actions-CI%2FCD-blue?logo=githubactions)
![DevSecOps](https://img.shields.io/badge/DevSecOps-Sonar_%7C_Trivy-green)
![Reusable Workflows](https://img.shields.io/badge/Reusable-Workflows-orange)

A **clean, flexible, and production-ready CI/CD templates repository** built with **GitHub Actions reusable workflows**.

This project is designed to help teams quickly set up **consistent CI pipelines** across multiple repositories (backend, frontend, microservices) with **job-level toggles**, **change detection**, and **DevSecOps integrations**.

---

## ✨ Key Features

- 🔁 **Reusable GitHub Actions workflows**
- 🎛️ **Job-level toggles** (enable/disable jobs per repo)
- 🔍 **Change detection** for monorepos & microservices
- 🧪 **Build & Test automation**
- 📊 **Static code analysis with SonarCloud**
- 🛡️ **Container image security scanning with Trivy**
- 🧱 **Language-agnostic** (Node.js, Python, Java, etc.)
- 📦 **Frontend & Backend friendly**

---

## 🧩 Pipeline Overview

The reusable CI pipeline is composed of **5 optional jobs**:

| Order | Job Name | Description |
|-----|---------|-------------|
| 1️⃣ | Detect Changes | Detects source code changes based on path filters |
| 2️⃣ | Setup Environment | Sets up runtime (Node, Python, Java, etc.) |
| 3️⃣ | Build & Test | Installs dependencies, builds and tests the app |
| 4️⃣ | Sonar Scan | Runs static code analysis using SonarCloud |
| 5️⃣ | Trivy Scan | Scans Docker images for vulnerabilities |

Each job can be **enabled or disabled independently** via inputs.

---

## 🖼️ Demo Pipeline

> Example GitHub Actions workflow execution using this template:

![CI Pipeline Demo](docs/images/ci-demo.png)

> 📌 _Replace the image with your real pipeline screenshot_

---

## ⚙️ Core Configuration

Every repository using this template must define **three core inputs**. These inputs tell the CI pipeline **what to run and where to run it**.

### 🧠 Required Inputs

| Input | Description | Example |
|------|------------|---------|
| `language` | Runtime / ecosystem used by the project | `node`, `python`, `java`, `etc`. |
| `version` | Runtime version | `20`, `3.11`, `17`, `etc`. |
| `workdir` | Working directory of the service | `frontend`, `backend`, `etc`. |

---

### 🔧 Example: Backend (Python)

```yaml
with:
  language: python
  version: "3.11"
  workdir: backend/auth
```

---

### 🔧 Example: Frontend (Node.js)

```yaml
with:
  language: node
  version: "20"
  workdir: frontend
```

---

## 🛠️ How to Use

### 1️⃣ Reference the reusable workflow

```yaml
jobs:
  my-ci:
    uses: thuantv-uit/ci-cd-templates/.github/workflows/ci-reusable.yml@main
```

---

### 2️⃣ Enable only the jobs you need

```yaml
with:
  enable_detect_job: true
  enable_setup_job: true
  enable_build_job: true
  enable_sonar_job: true
  enable_trivy_job: false
```

---

### 3️⃣ Configure build & test commands

```yaml
with:
  install_cmd: npm ci
  build_cmd: npm run build
  test_cmd: npm test
```

---

## 🔐 DevSecOps Integrations

### 📊 SonarCloud

- Static code analysis
- Code quality & security hotspots
- Coverage reporting

Required secret:

```yaml
SONAR_TOKEN
```

---

### 🛡️ Trivy

- OS & dependency vulnerability scanning
- Configurable severity levels
- Fail pipeline on critical issues

Example:

```yaml
with:
  enable_trivy_job: true
  trivy_image_name: my-app
  trivy_severity: CRITICAL,HIGH
  trivy_exit_code: 1
```

---

## 🎛️ Job Toggles

| Input | Description | Default |
|-----|------------|--------|
| enable_detect_job | Enable change detection | true |
| enable_setup_job | Enable runtime setup | true |
| enable_build_job | Enable build & test | true |
| enable_sonar_job | Enable SonarCloud scan | true |
| enable_trivy_job | Enable Trivy image scan | false |

---

## 🏗️ Supported Use Cases

- ✅ Frontend CI (React, Vue, Angular, etc.)
- ✅ Backend CI (Python, Node.js, Java, etc.)
- ✅ Microservices monorepo
- ✅ DevSecOps pipelines
- ✅ Team-wide CI standardization

---

## 📁 Repository Structure

```text
.github/
└── workflows/
    ├── ci-reusable.yml
    ├── detect-change.yml
    ├── setup-environment.yml
    ├── build.yml
    ├── sonarcloud-scan.yml
    └── trivy-scan.yml
```

---

## 📌 Best Practices

- 🔹 Enable only required jobs per repository
- 🔹 Use change detection for monorepos
- 🔹 Run Trivy only when Docker images are built
- 🔹 Keep secrets in the calling repository

---

## 🤝 Contributing

Contributions are welcome!

- Open an issue for suggestions
- Submit a PR for improvements
- Share best practices with the team

---

## 📜 License

This project is licensed under the **MIT License**.

---

## ❤️ Credits

Built with ❤️ for **clean CI/CD**, **DevSecOps**, and **scalable GitHub Actions workflows**.

Happy shipping 🚀

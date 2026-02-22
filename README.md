# 🛡️ Enterprise DevSecOps Pipeline | Secure SDLC Implementation

![GitHub Actions](https://img.shields.io/github/actions/workflow/status/ashhadali10/enterprise-devsecops-pipeline/pipeline.yml?branch=main&label=Pipeline%20Status&logo=github)
![Security](https://img.shields.io/badge/Security-Scan%20Passed-brightgreen)
![License](https://img.shields.io/badge/License-MIT-blue.svg)

> **Building security into the pipeline, not bolting it on at the end.**

## 📖 Overview

This project demonstrates a production-ready **DevSecOps Pipeline** designed to automate security testing within a CI/CD workflow. It implements the **Shift-Left Security** approach, ensuring vulnerabilities are detected and blocked before deployment.

Built as part of my research into automated security controls for regulated environments (Banking/FinTech), this pipeline integrates **SAST**, **SCA**, and **Container Security** scanning directly into GitHub Actions.

## 🎯 Objective

Traditional DevOps focuses on speed. DevSecOps focuses on **Secure Speed**. The goals of this project were:
1.  **Automate Security:** Remove manual bottlenecks in security testing.
2.  **Enforce Gates:** Prevent vulnerable code from reaching production (Exit Code 1 on failure).
3.  **Visibility:** Provide developers with immediate feedback on security issues.

## 🏗 Architecture

```mermaid
graph TD
    A[Developer Push] --> B(GitHub Actions)
    B --> C{SAST Scan}
    C -->|Fail| D[Block Build]
    C -->|Pass| E{Dependency Scan}
    E -->|Fail| D
    E -->|Pass| F{Build Docker}
    F --> G{Container Scan}
    G -->|Fail| D
    G -->|Pass| H[Deploy Ready]

## 🛠 Tech Stack & Security Tools

| Category | Tool | Purpose |
| :--- | :--- | :--- |
| **Language** | Python 3.9 | Application Logic |
| **Framework** | Flask | Web Server |
| **CI/CD** | GitHub Actions | Orchestration |
| **SAST** | Semgrep | Static Code Analysis |
| **SCA** | pip-audit | Dependency Vulnerability Scan |
| **Container** | Trivy | Image & OS Vulnerability Scan |
| **Containerization** | Docker | Environment Consistency |

## 🚀 Pipeline Workflow

The pipeline triggers on every `push` to the `main` branch.

### 1. Static Application Security Testing (SAST)
Scans source code for insecure patterns (e.g., hardcoded secrets, unsafe functions).
```yaml
- name: Run SAST
  run: semgrep --config=auto .
```

### 2. Software Composition Analysis (SCA)
Checks third-party libraries against known CVEs.
```yaml
- name: Run Dependency Scan
  run: pip-audit
```

### 3. Container Security
Scans the built Docker image for OS-level vulnerabilities.
```yaml
- name: Scan Docker Image
  uses: aquasecurity/trivy-action@master
  with:
    image-ref: 'devsecops-app'
```

## 📸 Pipeline Results

### ❌ Failed Build (Security Gate Active)
![Pipeline Failure](./assets/pipeline_fail.png)
*When vulnerabilities are detected, the pipeline fails automatically to prevent deployment.*

### ✅ Successful Build
![Pipeline Success](./assets/pipeline_success.png)
*Once vulnerabilities are remediated, the build passes and is marked ready for deployment.*

> **Note:** To see these images, please ensure you have uploaded screenshots of your GitHub Actions tab to an `assets` folder in your repository.

## 📂 Project Structure

```bash
.
├── .github/workflows/pipeline.yml   # CI/CD Configuration
├── app.py                           # Flask Application
├── Dockerfile                       # Container Configuration
├── requirements.txt                 # Dependencies
├── README.md                        # Documentation
└── SECURITY.md                      # Security Policy
```

## 🏃 Getting Started

### Prerequisites
- Python 3.9+
- Docker
- GitHub Account

### Local Installation
1. Clone the repository:
   ```bash
   git clone https://github.com/ashhadali10/enterprise-devsecops-pipeline.git
   ```
2. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```
3. Run locally:
   ```bash
   python app.py
   ```
4. Access at `http://localhost:5000`

### Run Security Scans Locally
```bash
# SAST
semgrep --config=auto .

# Dependency Scan
pip-audit

# Container Scan
trivy image devsecops-app
```

## 🧠 Key Learnings & Challenges

1.  **Hidden Files:** Learned to manage `.github` hidden directories in Linux environments.
2.  **Exit Codes:** Configured tools to return `exit code 1` on high-severity findings to enforce pipeline failure.
3.  **False Positives:** Tuned Semgrep rules to reduce noise while maintaining security coverage.
4.  **Shift-Left:** Realized that fixing a vulnerability in CI is 10x cheaper than in Production.

## 🔮 Future Roadmap (AI Integration)
*Currently exploring AI-driven security automation.*
- [ ] Integrate LLM-based vulnerability triage (using Ollama/Phi-3).
- [ ] Auto-remediation suggestions for developers.
- [ ] Deploy to AWS using Terraform (IaC Security).

## 🤝 Contributing
Security is a community effort. If you find a better way to configure these tools, please open a PR!

## 📬 Connect With Me
*   **LinkedIn:** [Asad Ali](https://linkedin.com/in/ashhadali10/)
*   **Email:** ashhadali2019@gmail.com
*   **Portfolio:** [GitHub Profile](https://github.com/ashhadali10)

## 📄 License
This project is licensed under the MIT License.
```

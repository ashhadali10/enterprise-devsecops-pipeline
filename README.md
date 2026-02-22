# Enterprise DevSecOps Pipeline | Secure SDLC Implementation

![GitHub Actions](https://img.shields.io/github/actions/workflow/status/ashhadali10/enterprise-devsecops-pipeline/pipeline.yml?branch=main&label=Pipeline%20Status&logo=github)
![Security](https://img.shields.io/badge/Security-Scan%20Passed-brightgreen)
![License](https://img.shields.io/badge/License-MIT-blue.svg)

> **Building security into the pipeline, not bolting it on at the end.**

## Overview

This project demonstrates a production-ready **DevSecOps Pipeline** designed to automate security testing within a CI/CD workflow. It implements the **Shift-Left Security** approach, ensuring vulnerabilities are detected and blocked before deployment.

Built as part of my research into automated security controls for regulated environments (Banking/FinTech), this pipeline integrates **SAST**, **SCA**, and **Container Security** scanning directly into GitHub Actions.

## Objective

Traditional DevOps focuses on speed. DevSecOps focuses on **Secure Speed**. The goals of this project were:
1.  **Automate Security:** Remove manual bottlenecks in security testing.
2.  **Enforce Gates:** Prevent vulnerable code from reaching production (Exit Code 1 on failure).
3.  **Visibility:** Provide developers with immediate feedback on security issues.

## Architecture

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


.
├── .github/workflows/pipeline.yml   # CI/CD Configuration
├── app.py                           # Flask Application
├── Dockerfile                       # Container Configuration
├── requirements.txt                 # Dependencies
├── README.md                        # Documentation
└── SECURITY.md                      # Security Policy



📬 Connect With Me
LinkedIn: Asad Ali
Email: ashhadali2019@gmail.com
Portfolio: GitHub Profile

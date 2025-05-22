---
title: "Writing Efficient GitLab Jobs – before_script, script, and after_script"
date: 2025-05-11
categories:
  - DevOps
  - Gitlab
tags:
  - GitLab
  - CI/CD
  - Automation
  - DevOps
---

# Writing Efficient GitLab Jobs – `before_script`, `script`, and `after_script`

Hello everyone!

In this week’s GitLab CI/CD series post, let’s zoom into the heart of every pipeline — the Job — and understand how to write clean and effective scripts using `before_script`, `script`, and `after_script`.

---

## 1. What is a Job in GitLab?

A **Job** is a single task executed by a GitLab Runner.  
Every job performs specific steps (like testing code or installing dependencies) and runs inside the environment defined by its executor (e.g., Docker, Shell).

---

## 2. Key Script Sections in a Job

Each job has three optional script blocks:

### 2.1 `before_script`
- Runs before the main script.
- Used for setup (installing tools, setting environment variables).
- Can be defined globally or per job.

### 2.2 `script`
- This is the main block.
- Contains the commands you want the job to execute.

### 2.3 `after_script`
- Runs after the job, even if it fails.
- Useful for cleanup actions (e.g., removing temp files).

---

## 3. Barclays Example – Provisioning EKS via AWS Service Catalog

Here’s a lightweight and secure example you might see within Barclays — provisioning an EKS cluster using a Service Catalog product:

```yaml
provision_eks:
  image: python:3.10  # Lightweight image with pre-installed tools
  before_script:
    - echo "Setting AWS region and credentials..."
    - export AWS_REGION=eu-west-2
    - export AWS_ACCESS_KEY_ID=$AWS_ACCESS_KEY_ID
    - export AWS_SECRET_ACCESS_KEY=$AWS_SECRET_ACCESS_KEY
  script:
    - echo "Triggering EKS provisioning via AWS Service Catalog..."
    - aws servicecatalog provision-product \
        --product-id prod-abc123 \
        --provisioned-product-name eks-control-plane \
        --provisioning-artifact-id pa-xyz789 \
        --provisioning-parameters Key=ClusterName,Value=barclays-eks Key=NodeCount,Value=2
  after_script:
    - echo "Checking EKS cluster status..."
    - aws eks describe-cluster --name barclays-eks --query 'cluster.status'
```

### What this job does:
- Uses lightweight `python:3.10` image (assuming AWS CLI is already available in the runner)
- Sets up AWS credentials using environment variables
- Provisions EKS using a Service Catalog product
- Verifies the provisioning status post-execution

---

## 4. Summary

- `before_script` helps set up the environment.
- `script` is the main task runner.
- `after_script` is your cleanup and validation phase.
- Barclays use cases often involve infrastructure steps like provisioning EKS, and this can be securely automated through GitLab jobs.

Stay tuned for next week’s post – we’ll explore how GitLab handles **Variables** and how to use them smartly in your pipelines!

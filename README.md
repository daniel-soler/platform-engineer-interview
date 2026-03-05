# Platform Engineer interview - Technical Exercise

AWS · Data Platform · Infrastructure & Automation

## Context

Our data platform integrates with external systems that trigger internal data processing workflows.
These workflows are orchestrated using Apache Airflow running on AWS Managed Workflows for Apache Airflow (MWAA).

In this exercise, you will design and propose a solution that automatically triggers an Airflow DAG when metadata files are delivered to an S3 bucket.

The goal is not to build a perfectly working production system, but to demonstrate how you reason about architecture, infrastructure, code structure, and deployment workflows.


## Scenario

An external system triggers data processing jobs by writing JSON files into an Amazon S3 bucket.

Each JSON file contains:

- The Airflow DAG ID to run

- The user that triggered the process

- A set of DAG run parameters

### Example JSON payload

```json
{
  "dag_id": "us-mapfreus-guidewire-policy",
  "triggered_by": "external_system",
  "params": {
    "start_date": "2026-03-01",
    "end_date": "2026-03-02"
  }
}
```

Once a file is written to S3, the corresponding Airflow DAG must be triggered programmatically using the information contained in the file.

There are multiple valid AWS-native approaches to solve this problem. You are free to choose the one you consider most appropriate and explain your reasoning.


## Pre-Existing Infrastructure

### S3 bucket (landing zone)
s3-snowflake-integration

### MWAA environment
Public URL:
https://prod-airflow.mwaa.amazonaws.com

### Example DAG ID
us-mapfreus-policy

### AWS account
All resources are located in the same AWS account.


## Repository

You will work in the following GitHub repository:

👉 https://github.com/daniel-soler/platform-engineer-interview.git

### Git workflow

Feature branch → develop → main

You do not need to open a pull request or merge branches; just structure your work as if you were following this workflow and push your changes to the repository.


## Objectives

This exercise is designed to evaluate your ability to:

- Design an event-driven AWS architecture

- Explain architectural tradeoffs clearly

- Organize a repository in a clean, maintainable way

- Write Infrastructure as Code using Terraform

- Write Python code and manage dependencies

- Explain how code and infrastructure would be deployed using CI/CD


## Tasks

### 1. Architecture Design

Draw a high-level architecture diagram using Draw.io [https://app.diagrams.net/]

Show all relevant AWS components and how they interact


### 2. Repository Structure

Propose a repository structure for:

- Infrastructure (Terraform)

- Application code (Python)

- CI/CD configuration

Explain why you structured the repository this way.

### 3. Infrastructure as Code (Terraform)

Write Terraform code to deploy:

- An AWS Lambda function (or any alternative AWS service that you consider most appropriate)

- An S3 event notification that triggers the service

- Required IAM roles and permissions

The code does not need to be executed or applied.

### 4. Lambda Implementation (Python)

Implement the service that:

- Receives S3 events

- Reads and parses the JSON file

- Extracts the DAG ID and parameters

- Triggers the corresponding Airflow DAG in MWAA

You may assume authentication and permissions are correctly configured

Focus on clarity, structure, and error handling rather than completeness

Explain what happens if the Lambda requires additional libraries or dependencies.

### 5. CI/CD Proposal

Explain how the solution would be deployed using GitHub Actions

Describe:

- Pipeline stages

- Branch/environment strategy

- How Terraform and Lambda code would be deployed

YAML examples are welcome but not required

## Notes & Assumptions

You are not required to deploy or execute the solution

The code does not need to be production-ready

Pseudocode is acceptable where appropriate

You may add documentation, comments, or assumptions to clarify your design

Focus on how the pieces fit together, not on AWS-specific edge cases

## What We Are Looking For

We will evaluate:

- Clarity of architecture and design decisions

- Code organization and maintainability

- Familiarity with AWS services and event-driven systems

- Infrastructure as Code best practices

- Understanding of CI/CD workflows

- Ability to communicate tradeoffs and assumptions

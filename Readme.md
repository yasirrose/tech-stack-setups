# LocalStack Setup Guide

This repository contains detailed instructions and configurations to set up LocalStack on a local machine. LocalStack provides a fully functional AWS cloud stack that can be run on your local machine for development and testing purposes.

---

## Table of Contents
- [Prerequisites](#prerequisites)
- [Installation](#installation)
  - [Using Docker Compose](#using-docker-compose)
- [Configuration](#aws-cli-configuration)
---

## Prerequisites
Ensure the following software is installed:
- [Docker](https://www.docker.com/)
- [Docker Compose](https://docs.docker.com/compose/)
- [Python](https://www.python.org/) (optional for CLI installation)

---

## Installation

### Using Docker Compose
1. [`docker-compose.yml`](#https://github.com/yasirrose/tech-stack-setups/blob/main/docker-compose.yml) file is created at the root of this directory to start localstack with docker compose:

2. Go to the root folder of directory and start the container:
   ```bash
   docker compose up
   ```

3. Verify services:
    ```bash
    curl http://localhost:4566/_localstack/health
    ```

---

## AWS CLI configuration
Use AWS Command Line Interface (CLI) to create local AWS resources with LocalStack.

You can use the AWS CLI with LocalStack using either of the following approaches:

- [AWS CLI](#aws-cli) 
- [LocalStack AWS CLI](#localstack-aws-cli)

### AWS CLI

- Installation
    ```bash
    pip install awscli
    ```

#### Configuring an endpoint URL
- Set environment variables:
  ```bash
  export AWS_ACCESS_KEY_ID=test
  export AWS_SECRET_ACCESS_KEY=test
  export AWS_DEFAULT_REGION=us-east-1
  ```
- Test Command:
    ```bash  
    aws --endpoint-url=http://localhost:4566 s3 ls
    ```
#### Configuring an custom profile

- Add to `~/.aws/config`:
    ```ini
    [profile localstack]
    region = us-east-1
    output = json
    endpoint_url = http://localhost:4566
    ```
- Add to `~/.aws/credentials`:
    ```ini
    [localstack]
    aws_access_key_id=test
    aws_secret_access_key=test
    ```
- Test Commands:
    ```bash  
    aws s3 ls --profile localstack
    export AWS_PROFILE=localstack
    aws s3 ls
    ```

---
LocalStack AWS CLI 
---
- Installation
    ```bash
    pip install awscli-local[ver1]
    ```
    This is a substitute for the standard aws command.
- Test Command:
    ```bash 
    awslocal s3 ls
    ```

Now, your setup for LocalStack and AWS CLI is complete, and you are ready to use the functionalities of both.
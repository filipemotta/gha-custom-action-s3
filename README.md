# GitHub Actions: Custom Python Action to Upload Files to AWS S3

## Introduction:

In today's fast-paced development world, continuous integration (CI) and continuous deployment (CD) have become central to successful software projects. GitHub Actions is one of the tools that offer developers the ability to automate their CI/CD processes right within their GitHub repositories.

In this article, we'll explore how to create a custom GitHub Action using Python to upload files to an AWS S3 bucket. This can be particularly useful when you want to store build artifacts, backup data, or deploy static websites.

## Use Cases:

- **Storing Build Artifacts:** After a build process, you might want to store generated binaries or libraries in S3 for later use or distribution.
- **Backup of Data:** If your workflow includes processes that generate valuable data, using S3 as a backup location is a good idea.
- **Deploying Static Websites:** Post-build, you can push your static website assets to an S3 bucket configured for web hosting.

## Solution Overview:

We'll develop a custom action using Python's `boto3` library. The action will take a directory as input and upload its contents to a specified S3 bucket.

### Step by Step Guide:

1. **Directory Structure:**

   Our custom action will have a straightforward directory structure:

s3-upload-action
│
├── action.yml
└── upload-to-s3.py

2. **Action Metadata (`action.yml`):**

This file defines the metadata of the action, its inputs, and its main script.

```yaml
name: 'Upload to S3'
description: 'Upload files to AWS S3 using Python'
inputs: ...
runs: ...
```

### 3. Python Script (upload-to-s3.py)
Our Python script leverages the boto3 library to interact with AWS services. It fetches action inputs, connects to S3, and uploads files from the specified directory.
```python
import os
import boto3
...
```

### 4. Usage in Workflows:

Once you've added this custom action to your repo, you can reference it in your workflows to utilize the S3 upload functionality.

```yaml
jobs:
  upload:
    ...
    - name: Upload to S3
      uses: ./.github/actions/s3-upload-action
      with: ...
```

### Security Note:
Always store your AWS credentials securely using GitHub's secret management. Never hard-code sensitive information. Also, ensure you're providing only the necessary permissions for the S3 operations, ideally following the principle of least privilege.

### Conclusion:
Custom GitHub Actions like the one we've explored can significantly enhance your CI/CD capabilities, making workflows more efficient and effective. By integrating with tools and platforms like AWS S3, you can seamlessly blend the development, build, and deployment phases of your projects, ensuring consistent and automated processes.

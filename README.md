# Lambda Python Libraries

This repository contains pre-bundled Python dependencies for AWS Lambda functions, packaged for specific Python runtimes. These libraries are structured as Lambda Layers, ready to be deployed and attached to Lambda functions.

## Overview

AWS Lambda has package size limits and sometimes requires specific dependency configurations. This repository maintains pre-built dependency packages that can be:

- Deployed as Lambda Layers
- Included directly in Lambda deployment packages
- Version-controlled and shared across multiple Lambda functions

## Current Packages

### `requests_aws4auth-python313`

**Runtime:** Python 3.13  
**Dependencies:**
- `requests` (2.32.5) - HTTP library
- `requests_aws4auth` (1.3.1) - AWS Signature Version 4 authentication for requests
- `urllib3` (2.5.0) - HTTP client
- `certifi` (2025.10.5) - Root certificates
- `charset_normalizer` (3.4.4) - Character encoding detection
- `idna` (3.11) - Internationalized Domain Names

**Use Case:** Lambda functions that need to make authenticated requests to AWS services like OpenSearch, API Gateway, or other AWS endpoints using AWS Signature Version 4.

## Adding New Dependency Packages

Follow these steps to add dependencies for a new Python runtime or a different set of libraries:

### 1. Create Directory Structure

```bash
# Create the package directory with runtime specification
mkdir -p <package-name>-python<version>/python
cd <package-name>-python<version>/python
```

Example:

```bash
mkdir -p requests_aws4auth-python314/python
cd requests_aws4auth-python314/python
```

### 2. Create the requirements.txt File

Create a `requirements.txt` file listing the dependencies you want to include. For example:

```plain
requests==2.32.5
requests-aws4auth==1.3.1
```

### 3. Install Dependencies

Use the following `pip` command to install the dependencies into the `python` directory. Make sure to specify the correct Python version.

```bash
python3.13 -m pip install --requirement requirements.txt --target python --upgrade  --platform manylinux2014_x86_64 --implementation cp --only-binary=:all:
```

### 4. Clean Up (Optional)

Remove unnecessary files to reduce package size:

```bash
find . -type d -name "__pycache__" -exec rm -rf {} +
```

### 5. Verify Structure

Ensure your directory follows the Lambda Layer structure:

```plain
<package-name>-python<version>/
└── python/
    ├── <library>/
    ├── <library>-<version>.dist-info/
    └── ... (other dependencies)
```

### 6. Commit to Repository

```bash
git add <package-name>-python<version>
git commit -m "Add <package-name> dependencies for Python <version>"
git push
```

## Related Resources

- [AWS Lambda Layers Documentation](https://docs.aws.amazon.com/lambda/latest/dg/configuration-layers.html)
- [AWS Lambda Python Runtimes](https://docs.aws.amazon.com/lambda/latest/dg/lambda-python.html)
- [pip install options](https://pip.pypa.io/en/stable/cli/pip_install/)

## License

Dependencies retain their original licenses. Check each package's license before use.

--- 
**Last Updated:** 17 November 2025
# AWS CloudFormation Templates

## Introduction

A **CloudFormation Template** is a text file that defines AWS infrastructure using code.

Instead of manually creating resources through the AWS Management Console, you describe the desired infrastructure in a template, and CloudFormation provisions it automatically.

Templates are written in:

- YAML (recommended)
- JSON

---

# Why Use Templates?

Without a template:

```
Administrator

↓

Create VPC

↓

Create EC2

↓

Create RDS

↓

Configure Security
```

Manual deployments are slow and prone to errors.

With a template:

```
CloudFormation Template

↓

CloudFormation

↓

AWS Infrastructure
```

Templates ensure consistent, repeatable deployments.

---

# How Templates Work

```
Write Template

↓

Validate Template

↓

Create Stack

↓

AWS Resources
```

CloudFormation reads the template and creates the resources in the correct order.

---

# Basic Template Structure

A CloudFormation template is made up of several optional and required sections.

```
Template

├── AWSTemplateFormatVersion
├── Description
├── Parameters
├── Mappings
├── Conditions
├── Resources
├── Outputs
└── Metadata (Optional)
```

The **Resources** section is required. The others are optional but commonly used.

---

# Template Sections

## 1. AWSTemplateFormatVersion

Specifies the template version.

Example:

```yaml
AWSTemplateFormatVersion: '2010-09-09'
```

---

## 2. Description

Provides a brief explanation of the template.

Example:

```yaml
Description: Creates an EC2 instance and Security Group.
```

---

## 3. Parameters

Parameters allow users to provide input values when creating a stack.

Example:

```yaml
Parameters:
  InstanceType:
    Type: String
    Default: t3.micro
```

Common uses:

- Instance type
- Key pair name
- Environment (Dev, Test, Prod)
- VPC ID

---

## 4. Mappings

Mappings define fixed values that vary by region or environment.

Example:

```yaml
Mappings:
  RegionMap:
    us-east-1:
      AMI: ami-123456
```

Useful for selecting region-specific AMIs.

---

## 5. Conditions

Conditions determine whether specific resources should be created.

Example:

```yaml
Conditions:
  CreateProdResources: true
```

Typical use cases:

- Development vs Production
- Optional resources
- Environment-specific deployments

---

## 6. Resources

The **Resources** section is the heart of every template.

It defines the AWS resources that CloudFormation creates.

Example:

```yaml
Resources:
  MyBucket:
    Type: AWS::S3::Bucket
```

Examples of supported resources:

- EC2
- VPC
- S3
- RDS
- IAM
- Load Balancers
- Lambda

---

## 7. Outputs

Outputs display useful information after stack creation.

Example:

```yaml
Outputs:
  BucketName:
    Value: !Ref MyBucket
```

Common outputs include:

- Instance ID
- Public IP
- VPC ID
- Load Balancer DNS Name

---

# YAML vs JSON

CloudFormation supports both YAML and JSON.

YAML:

```yaml
Resources:
  MyBucket:
    Type: AWS::S3::Bucket
```

JSON:

```json
{
  "Resources": {
    "MyBucket": {
      "Type": "AWS::S3::Bucket"
    }
  }
}
```

YAML is generally preferred because it is easier to read and maintain.

---

# Example Workflow

```
Write YAML Template

↓

Validate Template

↓

Create Stack

↓

CloudFormation

↓

AWS Resources Created
```

---

# Template Validation

Before deploying, validate your template to detect syntax errors.

Validation helps ensure:

- Correct syntax
- Valid resource types
- Required properties are present

---

# Real-World DevOps Example

A company wants identical environments for Development, Testing, and Production.

```
CloudFormation Template

        │

        ▼

Development

Testing

Production
```

The same template is reused with different parameter values.

---

# Benefits

- Infrastructure as Code
- Repeatable deployments
- Version control
- Faster provisioning
- Reduced human error
- Easy automation
- Consistent environments

---

# Best Practices

- Prefer YAML over JSON.
- Use Parameters instead of hardcoded values.
- Keep templates modular and reusable.
- Validate templates before deployment.
- Store templates in Git.
- Add meaningful Descriptions and Outputs.
- Use Conditions for environment-specific resources.

---

# Common Mistakes

- Hardcoding resource values.
- Creating very large templates instead of modular ones.
- Ignoring Parameters and Outputs.
- Making manual changes to stack-managed resources.
- Not validating templates before deployment.

---

# Interview Questions

### What is a CloudFormation Template?

A CloudFormation Template is a YAML or JSON file that defines AWS infrastructure as code.

---

### Which section of a CloudFormation template is required?

The **Resources** section.

---

### What is the purpose of Parameters?

Parameters allow users to provide input values when creating or updating a CloudFormation stack.

---

### Why are Outputs useful?

Outputs display useful resource information, such as an EC2 Instance ID or Load Balancer DNS name, after stack creation.

---

### Why is YAML preferred over JSON?

YAML is more readable, requires less syntax, and is easier to maintain.

---

# Key Takeaways

- CloudFormation Templates define AWS infrastructure using code.
- Templates can be written in YAML or JSON.
- The Resources section is mandatory.
- Parameters, Mappings, Conditions, and Outputs improve flexibility and reusability.
- Templates enable repeatable, automated, and version-controlled infrastructure deployments.
- Writing clean templates is a fundamental DevOps skill.
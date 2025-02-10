# AWS Deployment Guide

## Prerequisites
1. Install and configure AWS CLI
2. Install Docker
3. Create an AWS ECR repository
4. Set up an AWS S3 bucket for frontend
5. Configure AWS CloudFront (for CDN)

## Backend Deployment (API)

### 1. Build and Push Docker Image
```bash
# Login to AWS ECR
aws ecr get-login-password --region YOUR_REGION | docker login --username AWS --password-stdin YOUR_ACCOUNT_ID.dkr.ecr.YOUR_REGION.amazonaws.com

# Build Docker image
docker build -t srcbook-api ./packages/api

# Tag image
docker tag srcbook-api:latest YOUR_ACCOUNT_ID.dkr.ecr.YOUR_REGION.amazonaws.com/srcbook-api:latest

# Push to ECR
docker push YOUR_ACCOUNT_ID.dkr.ecr.YOUR_REGION.amazonaws.com/srcbook-api:latest
```

### 2. Deploy to ECS
1. Create an ECS cluster
2. Create a task definition using the ECR image
3. Create an ECS service
4. Set up Application Load Balancer

## Frontend Deployment (Web)

### 1. Build Frontend
```bash
cd packages/web
pnpm build
```

### 2. Deploy to S3
```bash
aws s3 sync dist/ s3://YOUR_BUCKET_NAME
```

### 3. Configure CloudFront
1. Create a CloudFront distribution pointing to the S3 bucket
2. Configure custom domain if needed
3. Set up SSL certificate using AWS Certificate Manager

## Environment Variables
Make sure to set these in AWS Systems Manager Parameter Store or AWS Secrets Manager:
- Database connection strings
- API keys
- Other sensitive configuration

## Monitoring and Logging
1. Set up CloudWatch for logs and metrics
2. Configure alarms for important metrics
3. Set up X-Ray for tracing (optional)

## CI/CD Setup (Optional)
1. Use AWS CodePipeline or GitHub Actions
2. Configure automatic deployments on main branch updates
3. Set up staging and production environments

## Security Considerations
1. Use AWS WAF for web application firewall
2. Configure security groups and NACLs
3. Implement proper IAM roles and permissions
4. Enable AWS Shield for DDoS protection (optional)

## Cost Optimization
1. Use auto-scaling groups
2. Configure proper instance sizes
3. Use reserved instances for predictable workloads
4. Set up AWS Cost Explorer alerts

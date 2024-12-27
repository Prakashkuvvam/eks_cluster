# AWS EKS Terraform Configuration

This Terraform configuration creates a complete VPC setup and an EKS cluster in AWS.

## Prerequisites

1. AWS CLI installed and configured
2. Terraform installed (version >= 1.0)
3. kubectl installed
4. AWS credentials configured with appropriate permissions

## Deployment Steps

1. Initialize Terraform:
```bash
terraform init
```

2. Review the planned changes:
```bash
terraform plan
```

3. Apply the configuration:
```bash
terraform apply
```

4. After successful deployment, configure kubectl:
```bash
aws eks update-kubeconfig --region $(terraform output -raw region) --name $(terraform output -raw cluster_name)
```

5. Verify cluster connection:
```bash
kubectl get nodes
```

## Clean Up

To destroy all resources:
```bash
terraform destroy
```

## Architecture

This configuration creates:
- A VPC with public and private subnets across 3 availability zones
- NAT Gateway for private subnet internet access
- EKS cluster in private subnets
- Managed node group with t3.medium instances
- All necessary security groups and IAM roles

## Important Notes

- The cluster uses EKS managed node groups
- Public endpoint is enabled for cluster access
- Default node group runs 2 t3.medium instances, scalable from 1 to 3
- Single NAT Gateway is used to reduce costs (for production, consider using multiple NAT Gateways)
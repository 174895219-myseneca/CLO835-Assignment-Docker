# CLO835-Assignment1-Terraform
The code creates an infrastructure on AWS including:
1. ECR
2. An EC2 instance with Docker installed
3. A path-based Application Load Balancer that routes traffic to other 3 containers on the EC2 instance.
4. Corresponding dependencies including security groups, target groups, ECR repositories.


### Deploy steps
```bash
terraform init
terraform validate
terraform plan
terraform apply
```

### Destroy infrastructure
```bash
terraform destroy
```

# hello-ecs-terraform

🚀 Terraform を使って、ALB なしの最小構成で AWS Fargate にコンテナをデプロイするテンプレートです。

## 使用技術
- AWS ECS Fargate
- CloudWatch Logs
- Terraform
- パブリックIPアクセス（開発用途）

## セットアップ手順

```bash
cd terraform
terraform init
terraform apply
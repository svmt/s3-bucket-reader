# Helm chart s3-bucket-reader

Helm chart to deploy demo app to read contents of S3 bucket

## TL;DR
```bash
helm repo add demo https://svmt-helm-repo-s3.s3.eu-central-1.amazonaws.com/charts/
helm repo update
helm search repo s3-bucket-reader
helm install -i s3-reader --set s3BucketName=<s3-bucket-name> demo/s3-bucket-reader-chart
```

## Requirements
Deployment requires S3 bucket name to be set either in values file or with `--set s3BucketName=<s3-bucket-name>`  

For protected s3 bucket AWS credentials should be set as environment variables from a secret
Example values:
```yaml
extraEnv:
  - name: AWS_ACCESS_KEY_ID
    valueFrom:
      secretKeyRef:
        name: aws-credentials
        key: access_key
  - name: AWS_SECRET_ACCESS_KEY
    valueFrom:
      secretKeyRef:
        name: aws-credentials
        key: secret_key
```

## GitHub Actions to publish helm chart

Github actions will auto-publish new chart on merge to `main` branch if Chart.yaml file has been modified

### Github actions requirements   

Github actions relies on AWS credentials with write access to S3 bucket to be configured in repo secrets
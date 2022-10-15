This repo contains reusable GitHub Action workflows.

# Workflows

## Build and push ECR repo:

- `ecr-repo` is the name of the repo in ECR (not the full URL)
- `github-role-arn` is a GitHub role with permission to push the repo to ECR

```yml
jobs:
  build-image:
    uses: kismet-healthcare/github-actions/.github/workflows/build-ecr-image.yml@main
    with:
      aws-region: ap-southeast-2
      ecr-repo:
      github-role-arn:
      image-tag: 
```

## Deploy task definition to ECS

Assumes image is hosted in ECR.

- `ecr-repo` is the name of the repo in ECR (not the full URL)
- `github-role-arn` is a GitHub role with permission to push the repo to ECR

```yml
jobs:
  build-image:
    uses: kismet-healthcare/github-actions/.github/workflows/build-ecr-image.yml@main
    with:
      aws-region: ap-southeast-2
      ecr-repo:
      ecs-cluster:
      ecs-service:
      ecs-container:
      github-role-arn:
      task-definition-s3-uri:
```

# Gotchas

- Sensitive data can't be expored, such as AWS accounts and ECR URLs
- GitHub is fussy about what data is available when. See this: https://docs.github.com/en/actions/learn-github-actions/contexts
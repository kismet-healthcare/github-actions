This repo contains reusable GitHub Action workflows.

# Workflows

## Build and push ECR repo:

Builds a docker image and pushes it to ECR.

- `aws-region` is the AWS region where the repo is located
- `ecr-repo` is the name of the repo in ECR (not the full URL)
- `github-role-arn` is a GitHub role with permission to push the repo to ECR
- `image-tag` the tag applied to the pushed image, recommend using `${{ github.sha }}`

```yml
jobs:
  build-image:
    uses: kismet-healthcare/github-actions/.github/workflows/build-image.yml@main
    with:
      aws-region: ap-southeast-2
      ecr-repo:
      github-role-arn:
      image-tag: 
```

## Copy image from one ECR to another

Copies an image from one ECR to another.

- `aws-region` is the AWS region where the repo is located
- `from-repo` is the name of the repo in ECR (not the full URL) with the image you want to copy
- `from-role-arn` is a GitHub role with permission to read the `from-repo`
- `to-repo` is the name of the repo in ECR (not the full URL) that you want to copy the image to
- `to-role-arn` is a GitHub role with permission to write to the `to-repo`
- `image-tag` is the tag of the image to copy, recommend using `${{ github.sha }}`

```yml
jobs:
  copy-image:
    uses: kismet-healthcare/github-actions/.github/workflows/copy-image.yml@main
    with:
      aws-region: ap-southeast-2
      from-repo: 
      from-role-arn:
      to-repo: 
      to-role-arn:
      image-tag:
```

## Deploy task definition to ECS

Deploys an image that is hosted in ECR to ECS.

- `aws-region` is the AWS region where the repo is located
- `ecr-repo` is the name of the repo in ECR (not the full URL)
- `ecs-cluster` is the name of the ECS cluster to deploy to
- `ecs-service` is the name of the ECS service to deploy to
- `ecs-container` is the name of the ECS container to deploy to (only supports single container right now)
- `github-role-arn` is a GitHub role with permission to access the image in ECR and deploy to ECS
- `task-definition-s3-uri` is the S3 path to a task definition JSON file (e.g. `s3://kismet-dev/tasks/definition.json`)

```yml
jobs:
  build-image:
    uses: kismet-healthcare/github-actions/.github/workflows/deploy-image.yml@main
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

- Sensitive data can't be exported from workflows, such as AWS accounts and ECR URLs, so you need to be able to deterministically recreate that data when orchestrating workflows (e.g. don't user a random number for a Docker image tag)
- GitHub is fussy about what data is available when. See this: https://docs.github.com/en/actions/learn-github-actions/contexts

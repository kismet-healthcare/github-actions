This repo contains reusable GitHub Action workflows.

# Build and push ECR repo:

- `ecr-repo-name` is the name of the repo in ECR (not the full URL)
- `github-role-arn` is a GitHub role with permission to push the repo to ECR

```yml
jobs:
  build-image:
    uses: kismet-healthcare/github-actions/.github/workflows/build-ecr-image.yml@main
    with:
      aws-region: ap-southeast-2
      ecr-repo-name:
      github-role-arn:
```
# argus-gh-actions

Shared GitHub Actions for Argus projects.

## docker-releaser-ecr

Builds and pushes multi-arch Docker images to AWS ECR with automatic GitHub releases.

### Usage

Single image:
```yaml
- uses: NSXBet/argus-gh-actions/docker-releaser-ecr@main
  with:
    image: 'argus-tools'
    gha-pat: ${{ secrets.GHA_PAT }}
```

Multiple images (parallel with matrix):
```yaml
jobs:
  release:
    strategy:
      matrix:
        image: [argus-api, argus-gateway, argus-controller]
    steps:
      - uses: NSXBet/argus-gh-actions/docker-releaser-ecr@main
        with:
          image: ${{ matrix.image }}
          use-bake: 'true'
          gha-pat: ${{ secrets.GHA_PAT }}
```

### Inputs

- `image` - Image name (required)
- `use-bake` - Use Docker Bake (default: false)
- `gha-pat` - GitHub PAT for private repos
- `ecr-registry` - ECR registry (default: 492684252576.dkr.ecr.us-east-1.amazonaws.com)
- `aws-region` - AWS region (default: us-east-1)
- `role-to-assume` - IAM role (default: arn:aws:iam::492684252576:role/GithubEcr)

<!-- start title -->

# GitHub Action:Run Terraform

<!-- end title -->
<!-- start description -->

Runs a specified terraform command and comments on pull requests. Has built in support for authenticating to AWS.

<!-- end description -->
<!-- start contents -->
<!-- end contents -->
<!-- start usage -->

```yaml
- uses: catalystcommunity/action-terraform@undefined
  with:
    # Which Terraform command to execute, supports `plan`, `apply`, and `validate`.
    command: ""

    # Which version of Terraform to install. Defaults to latest. Supports semver
    # ranges
    # Default: latest
    terraform-version: ""

    # Location of the Terraform root module to execute from
    # Default: ./
    work-dir: ""

    # Check format with `terraform fmt`, report errors in PR comment
    # Default: true
    check-format: ""

    # Validate configuration with `terraform validate`, report errors in PR comment
    # Default: true
    check-validate: ""

    # Whether to comment the command's result on the pull request if the event is a
    # pull request
    # Default: true
    comment-on-pr: ""

    # Github token to use for creating comments
    # Default: ${{ github.token }}
    github-token: ""

    # Cloud provider to get credentials for. Currently only supports `aws`.
    # Default:
    provider: ""

    # AWS region
    # Default: us-west-2
    aws-region: ""

    # AWS access key id to use
    # Default:
    aws-access-key-id: ""

    # AWS secret access key
    # Default:
    aws-secret-access-key: ""

    # AWS IAM role to assume
    # Default:
    aws-role-to-assume: ""

    # Whether to skip session tagging during AWS role assumption
    # Default:
    aws-role-skip-session-tagging: ""
```

<!-- end usage -->
<!-- start inputs -->

| **Input**                           | **Description**                                                                            |      **Default**      | **Required** |
| :---------------------------------- | :----------------------------------------------------------------------------------------- | :-------------------: | :----------: |
| **`command`**                       | Which Terraform command to execute, supports `plan`, `apply`, and `validate`.              |                       |   **true**   |
| **`terraform-version`**             | Which version of Terraform to install. Defaults to latest. Supports semver ranges          |       `latest`        |  **false**   |
| **`work-dir`**                      | Location of the Terraform root module to execute from                                      |         `./`          |  **false**   |
| **`check-format`**                  | Check format with `terraform fmt`, report errors in PR comment                             |        `true`         |  **false**   |
| **`check-validate`**                | Validate configuration with `terraform validate`, report errors in PR comment              |        `true`         |  **false**   |
| **`comment-on-pr`**                 | Whether to comment the command's result on the pull request if the event is a pull request |        `true`         |  **false**   |
| **`github-token`**                  | Github token to use for creating comments                                                  | `${{ github.token }}` |  **false**   |
| **`provider`**                      | Cloud provider to get credentials for. Currently only supports `aws`.                      |                       |  **false**   |
| **`aws-region`**                    | AWS region                                                                                 |      `us-west-2`      |  **false**   |
| **`aws-access-key-id`**             | AWS access key id to use                                                                   |                       |  **false**   |
| **`aws-secret-access-key`**         | AWS secret access key                                                                      |                       |  **false**   |
| **`aws-role-to-assume`**            | AWS IAM role to assume                                                                     |                       |  **false**   |
| **`aws-role-skip-session-tagging`** | Whether to skip session tagging during AWS role assumption                                 |                       |  **false**   |

<!-- end inputs -->
<!-- start outputs -->

| **Output**      | **Description** | **Default** | **Required** |
| :-------------- | :-------------- | ----------- | ------------ |
| `random-number` | Random number   |             |              |

<!-- end outputs -->
<!-- start examples -->

### Example usage

Terraform Plan:

```yaml
name: Validate pull request
on:
  pull_request:
    branches:
      - main
jobs:
  plan:
    name: Plan
    runs-on: ubuntu-latest
    steps:
      - name: Plan
        uses: catalystcommunity/action-terraform@v1
        with:
          command: plan
          work-dir: my-tf-env
          provider: aws
          aws-region: us-west-2
          aws-access-key-id: ${{ secrets.TERRAFORM_AWS_ACCESS_KEY_ID }}
          aws-secret-access-key: ${{ secrets.TERRAFORM_AWS_SECRET_ACCESS_KEY }}
```

Terraform Apply:

```yaml
name: Deploy
on: # only trigger on prs to main closed
  pull_request:
    types:
      - closed
    branches:
      - main
jobs:
  apply:
    if: github.event.pull_request.merged == true # only deploy on merged PRs
    name: Apply
    runs-on: ubuntu-latest
    steps:
      - name: Apply
        uses: catalystcommunity/action-terraform@v1
        with:
          command: apply
          work-dir: my-tf-env
          provider: aws
          aws-region: us-west-2
          aws-access-key-id: ${{ secrets.TERRAFORM_AWS_ACCESS_KEY_ID }}
          aws-secret-access-key: ${{ secrets.TERRAFORM_AWS_SECRET_ACCESS_KEY }}
```

<!-- end examples -->
<!-- start [.github/ghdocs/examples/] -->
<!-- end [.github/ghdocs/examples/] -->

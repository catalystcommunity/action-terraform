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
- uses: catalystsquad/action-terraform@undefined
  with:
    # Which Terraform command to execute, supports `plan` and `apply`
    command: ""

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
```

<!-- end usage -->
<!-- start inputs -->

| **Input**                   | **Description**                                                                            |      **Default**      | **Required** |
| :-------------------------- | :----------------------------------------------------------------------------------------- | :-------------------: | :----------: |
| **`command`**               | Which Terraform command to execute, supports `plan` and `apply`                            |                       |   **true**   |
| **`work-dir`**              | Location of the Terraform root module to execute from                                      |         `./`          |  **false**   |
| **`check-format`**          | Check format with `terraform fmt`, report errors in PR comment                             |        `true`         |  **false**   |
| **`check-validate`**        | Validate configuration with `terraform validate`, report errors in PR comment              |        `true`         |  **false**   |
| **`comment-on-pr`**         | Whether to comment the command's result on the pull request if the event is a pull request |        `true`         |  **false**   |
| **`github-token`**          | Github token to use for creating comments                                                  | `${{ github.token }}` |  **false**   |
| **`provider`**              | Cloud provider to get credentials for. Currently only supports `aws`.                      |                       |  **false**   |
| **`aws-region`**            | AWS region                                                                                 |      `us-west-2`      |  **false**   |
| **`aws-access-key-id`**     | AWS access key id to use                                                                   |                       |  **false**   |
| **`aws-secret-access-key`** | AWS secret access key                                                                      |                       |  **false**   |

<!-- end inputs -->
<!-- start outputs -->

| **Output**      | **Description** | **Default** | **Required** |
| :-------------- | :-------------- | ----------- | ------------ |
| `random-number` | Random number   |             |              |

<!-- end outputs -->
<!-- start examples -->

### Example usage

```yaml
on: [push]

jobs:
  hello_world_job:
    runs-on: ubuntu-latest
    name: A job to say hello
    steps:
      - uses: actions/checkout@v2
      - id: foo
        uses: actions/hello-world-composite-action@v1
        with:
          who-to-greet: "Mona the Octocat"
      - run: echo random-number ${{ steps.foo.outputs.random-number }}
        shell: bash
```

<!-- end examples -->
<!-- start [.github/ghdocs/examples/] -->
<!-- end [.github/ghdocs/examples/] -->

# action-pipenv-aws-setup

Common github action setup steps. This is a common infrastructure setup which:

1. Checks out code
2. Sets up python
3. Sets up pipenv
4. Installs dependencies
5. Assumes an AWS role with OIDC integration. This requires that OIDC integration with an IAM role is setup so that the github repo can assume the role to deploy to your AWS account. See below for more information.

## Recent updates

### v3 update

We've recently released a v3 of this action that updates to using OIDC integration with the [aws-actions/configure-aws-credentials](https://github.com/aws-actions/configure-aws-credentials) action.

This is a breaking change.

You should update your action references to v3 once you have setup OIDC integration. See `To setup github OIDC` under [Github OIDC Setup README](https://github.com/Sage-Bionetworks-IT/organizations-infra/blob/master/org-formation/650-identity-providers/README.md) for how to setup your github repo with OIDC integration for use with v3 of this repo. See the following steps + example for how to implement the integration in your github actions workflow for use with v3 of this action.

Other minor changes include making more inputs for user to specify when implementing this action into their Github (GH) Actions workflow as well as upgrading all actions' versions.

## Getting Started

### For v3 - present of this action

There are some inputs that the user can specify values for in this action. See [action.yaml](https://github.com/Sage-Bionetworks/action-pipenv-aws-setup/blob/main/action.yaml) for further details for this action's inputs.

For inputs related to aws credentials and role assuming, see [configure-aws-credentials-for-github-actions](https://github.com/aws-actions/configure-aws-credentials#configure-aws-credentials-for-github-actions) for the full documenation including limitations on those inputs.

Also be sure to include the following permissions in your GH Actions workflow for the job or job(s) that use this action:

```
# These permissions are needed to interact with GitHub's OIDC Token endpoint.
permissions:
    id-token: write
    contents: read
```

### For v1-v2 of this action

Highly recommended to update to using OIDC integration.

- See [PR #551](https://github.com/Sage-Bionetworks-IT/organizations-infra/pull/551) as an example for how the GH action `configure-aws-credentials` was previously integrated with static IAM credentials by using repository secrets.
- See [Encrypted Secrets](https://docs.github.com/en/actions/security-guides/encrypted-secrets) on how to add secrets to your github repo
- See [Assume role with static IAM credentials in repository secrets](https://github.com/aws-actions/configure-aws-credentials#assumerole-with-static-iam-credentials-in-repository-secrets) for an example of an implementation to allow for role assuming using secrets.

### Contributing

Read through the [contribution guidelines](CONTRIBUTING.md) for more information.

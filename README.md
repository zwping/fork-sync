# 仅升级原项目中node版本号，具体使用请移步至原项目[tgymnich/fork-sync](https://github.com/tgymnich/fork-sync)


![Version](https://img.shields.io/github/v/release/zwping/fork-sync?style=flat-square)



## Auto approve

If you use a workflow which does not allow to merge pull requests without a review 
("Require pull request reviews before merging" in your [repo settings](https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/configuring-pull-request-merges/managing-auto-merge-for-pull-requests-in-your-repository))
you can set `auto_approve` to `true`. In that case you'll have to provide a [personal access token](https://docs.github.com/en/free-pro-team@latest/github/authenticating-to-github/creating-a-personal-access-token)
for a user which is allowed to review the pull requests changes. Make sure the token has at least
`public_repo` permissions and store the token inside of the [repository secrets](https://docs.github.com/en/free-pro-team@latest/actions/reference/encrypted-secrets#creating-encrypted-secrets-for-a-repository).

An example workflow would then look like this:

```yml
name: Sync Fork

on:
  schedule:
    - cron: '*/30 * * * *' # every 30 minutes
  workflow_dispatch: # on button click

jobs:
  sync:

    runs-on: ubuntu-latest

    steps:
      - uses: zwping/fork-sync@v1.6.5
        with:
          token: ${{ secrets.PERSONAL_TOKEN }}
          owner: llvm
          base: master
          head: master
```

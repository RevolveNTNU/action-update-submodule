# action-update-submodule
Action for Github actions to trigger an update of a single submodule.

Add a workflow with this action in your submodule to trigger a PR with an update of this repo on the parent repo.

Any other submodules that might be present in the parent repo are ignored

## Usage

Example workflow:

```yml
name: Submodule Update
 
on:
  push:
    branches: [main]
 
jobs:
  build:
    name: Submodule update
    runs-on: ubuntu-latest
 
    steps:
      - name: 'Update submodule on parent'
        uses: 'RevolveNTNU/action-update-submodule@v1'
        with:
          self_dot_git: 'my_test_submodule.git'

          name: 'Test submodule'

          pat_token:  ${{ secrets.PAT_TOKEN }}

          pr_branch_name: 'submodule-update'

          target_branch: 'dev'

          parent_repository: 'parent'

          checkout_branch: 'main'

          owner: 'RevolveNTNU'
```

This file should be placed in the `my_test_submodule`-repo.

This would make a pull request on `dev` in the repo `RevolveNTNU/parent`, updating the `my_test_submodule`-submodule to the latest `main`.


## Convert "uat" as the default branch instead of "main"
1. Create the branch "uat".
2. Go to Settings and change the default branch from "main" to "uat".
3. Click "Update".
4. Click the button "I understand, update the default branch"

https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-branches-in-your-repository/changing-the-default-branch 

## Create a GitHub Action to 
block-non-uat-prs.yml

```
name: Block PRs not from UAT

on:
  pull_request:
    branches:
      - main

jobs:
  block_non_uat:
    runs-on: ubuntu-latest
    steps:
      - name: Check PR source branch
        run: |
          echo "PR source branch is ${{ github.head_ref }}"
          if [[ "${{ github.head_ref }}" != "uat" ]]; then
            echo "❌ Pull requests to main are only allowed from 'uat'."
            exit 1
          else
            echo "✅ Valid PR from 'uat'."
          fi
```

# `git` basics live demonstration


## Before demonstration

Before the live demo, slides and/or some browser navigation will have introduced the following concepts and/or commands:

- `add/commit/push` (including `commit` flavors) `status`, `diff`
- `.gitignore` and `.gitkeep` files
- _Briefly_, the concept of feature branches
- Exploring project history in GitHub using `scpca-nf`
  - See past commits, releases and/or tags
  - `Blame` view (use [`scpca-nf/bin/post_process_sce.R`](https://github.com/AlexsLemonade/scpca-nf/blob/main/bin/post_process_sce.R), a script with three contributors)
- Undoing or modifying changes
  - `checkout`, `reset`, `revert`, `commit --amend`

## Live demonstration

- In browser, navigate to https://github.com/AlexsLemonade/2023-chop-training-demo/issues to see an issue that we are going to demonstrate tackling
- Locally, use terminal to navigate to repo and checkout a feature branch named `sjspielman/<issue #>-<feature description>`
- Perform first code change necessary to address issue
  - As part of this, open a different file and make "accidental" changes (for purposes of running `git checkout` soon)
- Show `add/commit` (using `git commit -m`)
  - `git status` should be run before running each command
  - `git diff` shoud be used before adding file changes; each file is added one a time
  - At some point we realize we need to run `git checkout` on the accidental changes; do so!
- Perform second code change necessary to address the issue
- Second round of `add/commit` for the other file change
  - This demonstrates discretizing commits into small bites
- Finally, `push` which will fail since there is no remote branch; `git` gives us the command for success
- In browser, see the pushed code and demonstrate opening a PR to `main`. PR should include the following components:
  - Before writing any text, see how you can view the file changes and then make any code updates _before_ filing the PR (with any luck GitHub will demand a newline somewhere)
  - `Closes #<issue>`
  - Text explaining changes made
  - Specific things reviewer might check for

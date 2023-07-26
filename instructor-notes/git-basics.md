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
  - `checkout`, `reset`, `revert`, `commit --amend`, `restore --staged`

## Live demonstration

- In browser, navigate to https://github.com/AlexsLemonade/2023-chop-training-demo/issues to see an issue that we are going to demonstrate tackling
- Locally, use terminal to navigate to repo and checkout a feature branch named `<your user name>/<issue #>-histogram-bins>`
- In the directory, create and open an RStudio project, which will have the effect of creating a `.gitignore` file with some pre-populated contents.
Look around the repository to show trainees what we are working with in general; "accidentally modify" an existing file while doing this.

- There will now be a few `add/commit` (using `git commit -m`) cycles in this order, using `git status` liberally, and using `git diff` on each file before it is added
  1. Run a `git status` before beginning to code.
  Discuss the `.gitignore` changes, and `git checkout` accidentally modified file. Add/commit `.gitignore`.
  2. Add `ggsave()` to the script. Add/commit.
  3. Add `optparse` with the bins options to the script, and modify export file name. Add/commit.
  4. Run script so a plot is included now in `plots/`. Remove the `plots/.gitkeep`. Add/commit.
- Perform first code change necessary to address issue
  - As part of this, open a different file and make "accidental" changes (for purposes of running `git checkout` soon)
- Finally, `push` which will fail since there is no remote branch; `git` gives us the command for success
- In browser, see the pushed code and demonstrate opening a PR to `main`. PR should include the following components:
  - Before writing any text, see how you can view the file changes and then make any code updates _before_ filing the PR (with any luck GitHub will demand a newline somewhere)
  - `Closes #<issue>`
  - Text explaining changes made
  - Specific things reviewer might check for

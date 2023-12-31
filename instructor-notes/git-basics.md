# `git` basics live demonstration


## Before demonstration

Before the live demo, slides and/or some browser navigation will have introduced the following concepts and/or commands:

- `add/commit/push` (including `commit` flavors) `status`, `diff`
- `.gitignore` and `.gitkeep` files
- _Briefly_, the concept of feature branches
- Undoing or modifying changes
  - `checkout`/`restore (--staged)`, `reset`, `revert`, `commit --amend`

## Live demonstration

- In browser, navigate to https://github.com/AlexsLemonade/2023-chop-training-demo/issues to see an issue that we are going to demonstrate tackling
- Locally, use terminal to navigate to repo and create a feature branch: `git switch -c <your user name>/<issue #>-histogram-bins>`
- In the directory, create and open an RStudio project, which will have the effect of creating a `.gitignore` file with some pre-populated contents, and it will allow us to use `{here}` throughout.
Look around the repository to show trainees what we are working with in general; "accidentally modify" an existing file while doing this.
- There will now be a few `add/commit` (using `git commit -m`) cycles in this order, using `git status` liberally, and using `git diff` on each file before it is added
  1. Run a `git status` before beginning to code.
  Discuss the `.gitignore` changes, and `git restore` accidentally modified file. Add/commit `.gitignore`.
  2. Add `ggsave()` to the script. Add/commit.
  3. Add `optparse` with the bins options to the script, and modify export file name. Add/commit.
  4. Run script so a plot is included now in `plots/`. `git rm` the `plots/.gitkeep`. Add/commit.
- Finally, `push` which will fail since there is no remote branch; `git` gives us the command for success
- In browser, see the pushed code and demonstrate opening a PR to `main`. PR should include the following components:
  - Before writing any text, see how you can view the file changes and then make any code updates _before_ filing the PR (with any luck GitHub will demand a newline somewhere)
  - `Closes #<issue>`
  - Text explaining changes made
  - Specific things reviewer might check for

# Stacking branches live demonstration

## Before demonstration

Before the live demo, slides will have covered only the concept of git branch stacking, as well as why it's a challenging thing to do in forks.
There are no new `git` commands that need to be introduced for this live demo.

## Live demonstration

### Part 1: How to stack branches

This first part of the demonstration is based around two issues:
* Issue 1: Write a `utils.R` script with a function that, given a data frame and two numeric variables, build a regression and returns the `broom::tidy()` output
* Issue 2: Write a script called `model-penguins.R` that sources `utils.R`, builds a model from penguin variables, and exports results to a TSV

* First, run `git pull` in `main` to ensure I am synced up before I start new work
* Create and switch to the branch `<username>/<issue #>-utils-linear-model`
* Perform one `add/commit/push` (with `status` and `diff`) to create the `utils.R` script
  * For this first commit, _do not_ include documentation of this function
* Open PR GitHub, but don't spend much time crafting a perfect PR as that is not the point of this demo
  * In the background, co-teacher will leave a review that the code needs docs
* While still in `<username>/<issue #>-utils-linear-model`, create and switch to branch `<username>/<issue #>-build-penguin-model`
* Perform one `add/commit/push` (with `status` and `diff`) to create the `model-penguins.R` script
* File a PR in GitHub, setting the base branch to `<username>/<issue #>-utils-linear-model`
  * Demonstrate how the overall file diff is different depending on the base
* Return to original PR where I see a review comment
* Back on command line, return to `<username>/<issue #>-utils-linear-model`, implement requested changes, and `add/commit/push`.
* PR is now accepted and merged, and we _delete_ the remote branch `<username>/<issue #>-utils-linear-model`
* Return to other open PR with the script that performs penguin modeling
  * Note that the base has changed to `main` now that the remote branch was deleted
  * Also note that the branch is no longer up-to-date with `main`.
  Explain two ways to handle this (but ultimately do the first one):
    * Within GitHub, merge `main` into `<username>/<issue #>-build-penguin-model`, and then pull down
    * Within your local repo, checkout `main`, pull down, checkout `<username>/<issue #>-build-penguin-model`, merge on command line, and then push.
* The second PR can now be approved and merged into `main`.


### Part 2: How to approximate stacking when you are working in a fork

The second part of the demonstration is based around two similar two issues:
* Issue 1: Add a function to the `utils.R` script that, given a data frame and two numeric variables, exports a scatterplot
* Issue 2: Modify the script `model-penguins.R` to make and export a scatterplot of variables used in the regression

* Explain again that stacking won't work well, _unless_ you want to have a review performed in your fork.
  * If you want the full project history including reviews to be present in the `upstream` repository, this will not meet your needs
* Navigate via command line to the _fork_ of the repo, and ensure the `main` branch is up-to-date with the `upstream`'s `main` branch
* Create and enter branch off of `main`, `<username>/<issue #>-scatterplot-function`
* Within this branch perform three `add/commit` (but _not_ push) cycles:
  * First, add the plotting function to the `utils.R` script
  * Second, use the function in the `model-penguins.R` script
  * Third, run the script to export PNG to `plots/`
* View the `git log`, and identify which commits should be "stacked" on which: The latter two commits should be stacked on the first commit.
* Return to `main` and create/enter a branch, `<username>/<issue #>-penguins-scatterplot`
* `git cherry-pick` the latter two commits into this branch
  * **TODO**: Unsure how to handle duplicate histories?
    * I could run a `git revert` in first branch (`<username>/<issue #>-scatterplot-function`)?
    * I could introduce a third branch? Would entail 2 cherry picks and then delete the first branch.
* Now we have two branches which are _sort of_ stacked, at least in the scope of their work.
* Both branches can be filed to the `upstream` repo's `main` branch, with sufficient information in the two PRs to help reviewers understand how the PRs are related
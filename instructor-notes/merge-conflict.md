# Dealing with merge conflicts live demonstration

## Dependencies

This live demo will make use of two frameworks for resolving merge conflicts:
- [GitKraken](https://www.gitkraken.com/)
- [Visual Studio Code](https://code.visualstudio.com/)

The instructor leading the live demo will need to have these softwares installed, and further ensure that the demo repository is already in `GitKraken`.

## Before demonstration

This live demo will build on code previously written as part of the [`git` basics](./git-basics.md) live demo, where a script will have been written to plot and export a histogram of a `palmerpenguins::penguins` numeric variable.
Before beginning this live demo, navigate to GitHub and show the script to re-orient trainees to the relevant code.

In addition, slides will have introduced the concept of merge conflicts, when they might arise, and how to avoid them in the first place to the extent possible.
Slides should also introduce a schematic of the live demo: We're going to have several branches off of the same base, each one modifying the same lines of code such that changes cannot be automatically merged.


## Live demonstration


* Ensure we are up-to-date in the `main` branch, and create (`git branch <branch name>`) three branches (emphasizing that these "quick and dirty" branch names are for the purposes of demonstrating merge conflicts only, and otherwise are not very good!):
  * `hist-mod-1`
  * `hist-mod-2`
  * `hist-mod-3`

### Setup to induce merge conflicts

First, we'll modify a line of code in `hist-mod-1`, which will allow `hist-mod-2` and `hist-mod-3` to have conflicts with `main`.

* Enter into the first branch `git switch hist-mod-1`
* Modify the histogram code as follows (ensure code changes are on the same line to induce later conflicts):
```r
# original code
geom_histogram(bins = n_bins)

# new code
geom_histogram(bins = n_bins, color = "blue")
```
* `add/commit/push` the change
* File a quick 'n dirty PR, which co-instructor quickly approves, and merge the PR.

### Merge conflict 1: Resolve with VS Code

* Locally, checkout the `main` branch and sync up (`git switch main; git pull`)
* Checkout the second branch: `git switch hist-mod-2`
  * Note that if we were to run `git merge main` _now_, we would avoid a merge conflict by keeping our `base` up to date before making changes in this new branch.
  We're not going to do that for the purposes of demonstratation, but it's good to know.
* Modify the histogram code to induce a conflict:
```r
# original code
geom_histogram(bins = n_bins)

# new code
geom_histogram(bins = n_bins, color = "purple", fill = "yellow")
```
* `add/commit/push` the change
* File quick 'n dirty PR to `main`, and the PR will tell us that we have merge conflict.
* Resolve the conflict in VS Code
  * Open the script in VS Code and explain the merge conflict view
  * Explain that "theirs" = "Incoming change" and "ours" = "Current change"
  * Click the handy "Accept current change" text
* Return to command line, run `git status`, `commit` the resolved conflict, and `push`
* In browser, refresh the PR and see that there is no longer a merge conflict message.
  * In the interest of time, this PR does not need to be approved/merged.



### Merge conflict 2: Resolve with GitKraken

* Checkout the third branch: `git switch hist-mod-3`
  * Remind everyone via `git log` that its base remains `main`, _before_ `hist-mod-1` was merged in
* Modify the histogram code to induce a conflict:
```r
# original code
geom_histogram(bins = n_bins)

# new code
geom_histogram(bins = n_bins, linewidth = 1.5, color = "cadetblue")
```
* `add/commit/push` the change (`push` is less critical for this demo; doesn't matter if that is skipped)
* Run `git merge main` via command line, which will inform us we have a merge conflict.
This approach shows a different way that one can discover a merge conflict, v.s. the last example where opening a PR identified the conflict
* Resolve the conflict in GitKraken.
  * Open the repository in GitKraken and show the conflict view
  * Explain that "theirs" is on the top left, and "ours" is on the top right
  * Fix the conflict by ensuring only "ours" is in the output frame below
  * Commit to resolve the merge conflict within GitKraken direcly
* Viola!





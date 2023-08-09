# Dealing with merge conflicts live demonstration

## Dependencies

This live demo will make use of two frameworks for resolving merge conflicts:
- [GitKraken](https://www.gitkraken.com/)
- [Visual Studio Code](https://code.visualstudio.com/)

The instructor leading the live demo will need to have these softwares installed, and further ensure that the demo repository is already in `GitKraken`.

## Before demonstration

This live demo will build on two pieces of code:

- The script `scripts/plot_penguins_histogram.R` written as part of the [`git` basics](./git-basics.md) live demo, which plots and exports a barebones histogram of `palmerpenguins::penguins` bill depth.
- The script `scripts/penguins_calculate_mass.R` written as part of the [working with branches](./working-with-branches.md) live demo, which calculates mean `palmerpenguins::penguins` mass across species.

Before beginning this live demo, navigate to GitHub and show the script to re-orient trainees to the relevant code.

In addition, slides will have introduced the concept of merge conflicts, when they might arise, and how to avoid them in the first place to the extent possible.
Slides should also introduce a schematic of the live demo: We're going to have several branches off of the same base, each one modifying the same lines of code such that changes cannot be automatically merged.
Further explain that in a real-life scenario, something like this might occur when three team members are each working in one of these branches, simultaneously modifying the same code.


## Live demonstration


* Ensure we are up-to-date in the `main` branch, and create (`git branch <branch name>`) three branches (emphasizing that these "quick and dirty" branch names are for the purposes of demonstrating merge conflicts only, and otherwise are not very good!):
  * `code-mod-1`
  * `code-mod-2`
  * `code-mod-3`

### Setup to induce merge conflicts

First we'll need to modify lines in each of the two relevant scripts, which will allow the `code-mod-2` and `code-mod-3` to have conflicts with `main`.


* Enter into the first branch `git switch code-mod-1`

* First, modify `scripts/penguins-calculate-mass.R` as follows, and `add/commit` the change.
```r
# original code
group_by(species)

# new code
group_by(species, island)
```
* Second, modify `scripts/plot_penguins_histogram.R` as follows (ensure code changes are on the same line to induce later conflicts), and `add/commit` the change.
```r
# original code
geom_histogram(bins = n_bins)

# new code
geom_histogram(bins = n_bins, color = "dodgerblue", fill = "gold")
```
* Push, and file a quick 'n dirty PR, which co-instructor quickly approves, and merge the PR.
  * Note aloud that we are moving through this step quickly only for the purpose of the demonstration!

### Merge conflict 1: Resolve with VS Code

This merge conflict will focus on changes to `scripts/penguins_calculate_mass.R`.

* Locally, checkout the `main` branch and sync up (`git switch main; git pull`)
* Checkout the second branch: `git switch hist-mod-2`
  * Note that if we were to run `git merge main` _now_, we would avoid a merge conflict by keeping our `base` up to date before making changes in this new branch.
  We're not going to do that for the purposes of demonstration, but it's good to know.
* Modify the script to induce a conflict, run the script to produce an updated TSV, and `add/commit/push` all changes.
```r
# original code
group_by(species, island)

# new code
filter(year == 2008) |>
group_by(species, island)
```
* File quick 'n dirty PR to `main`, and the PR will tell us that we have merge conflict.
* Return to local repository (not in browser), and open Resolve the conflict in VS Code
  * Open the _script_ in VS Code and explain the merge conflict view
  * Explain that "theirs" = "Incoming change" and "ours" = "Current change"
  * Click the handy "Accept current change" text
* Open the TSV file in VS Code and look at the conflict
  * Explain that we could, for this simple example, choose "ours"/"theirs", but it's easy to get confused since it is not immediately obvious from the data itself which is which (same columns & types).
  * This confusion would be even greater for larger/more realistic data files.
* Re-run the script whose conflict has been resolved to resolve the TSV conflict.
A bonus benefit of this step is extra confirmation that you have indeed resolved the conflict; if `>>>>` etc. remains in your file, the code will not run.
* Return to command line, run `git status`, `commit` the resolved conflict, and `push`.
* In browser, refresh the PR and see that there is no longer a merge conflict message.
  * In the interest of time, this PR does not need to be approved/merged.


### Merge conflict 2: Resolve with GitKraken

This merge conflict will focus on changes to `scripts/plot_penguins_histogram.R`.

* Checkout the third branch: `git switch code-mod-3`
  * Remind everyone via `git log` that its base remains `main`  _before_ `code-mod-1` was merged in
* Modify the script to induce a conflict, run it to produce an updated PNG, and `add/commit` all changes (`push` is less critical for this demo; doesn't matter if that is skipped)
```r
# original code
geom_histogram(bins = n_bins)

# new code
geom_histogram(bins = n_bins, color = "deepskyblue1", fill = "olivedrab3")
```
* Run `git merge main` via command line, which will inform us we have a merge conflict.
This approach shows a different way that one can discover a merge conflict, v.s. the last example when it was discovered by filing a PR.
* Note that we cannot directly compare "ours"/"theirs" in a PNG by just opening the file, but GitKraken can help
* Resolve the R script conflict in GitKraken.
  * Open the repository in GitKraken and show the conflict view
  * Explain that "theirs" is on the top left, and "ours" is on the top right
  * Fix the conflict by ensuring only "ours" is in the output frame below
* Resolve the PNG conflict.
GitKraken will allow us to choose which PNG, but we might prefer to re-run the script anyways to be sure the PNG is correct.
* Commit within GitKraken directly to conclude the merge

### Final punchlines of demo

* Sync up with your base branch sooner rather than later
* Don't let branches/PRs get too stale, as they will get increasingly out of sync
* Coordinate with your team to reduce odds of working on the same lines of code at once




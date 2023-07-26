# Working with multiple branches live demonstration

## Before demonstration

Before the live demo, slides will introduce the follow concepts/commands:

* Introduce feature branches conceptually and why we use them
 * Note that more discussion of feature branches will come later in the afternoon during git workflow slides
* Introduce `git checkout` (as in `git switch`) and `git branch`
* Introduce `git stash` and `git cherry-pick`
* Introduce concept of stacking, which we will come back to in day 2
Note that stacking will not be part of this live demo.
* Show a brief schematic of what we will do in the live demo to help orient trainees
  * We will have four branches working on complementary, _but different_ (no merge conflicts, please!), areas of the code base
  * Show issues that each branch is going to tackle
   * Branch 1: Add script to export TSV of penguins sampled in 2008 to `results/`
   * Branch 2: Add script to export TSV of only Adelie penguins to `results/`
   * Branch 3: Add script to export TSV of number of penguins on each island to `results/`
   * Branch 4: Add script to export TSV of number of penguins from each species to `results/`

## Live demonstration

* Ensure I am up to date with `main` branch, and create 4 branches for use during demonstration (saves time later):
  * Branch 1: `git branch <username>/<issue #>-2008-penguins`
  * Branch 2: `git branch <username>/<issue #>-adelie-penguins`
  * Branch 3: `git branch <username>/<issue #>-penguins-island-count`
  * Branch 4: `git branch <username>/<issue #>-penguins-species-count`
* Briefly introduce what the live demo will show:
  * Successfully working with two branches, and note that success is achieved in part by lots of `git status`
  * Two common "gotchas" when working with multiple branches

### Scenario 1: Working successfully between two branches: 2008 and Adelie penguins

* Use `git switch` to enter `<username>/<issue #>-2008-penguins`
* Three `add/commit/push` cycles with `git status` along the way:
  * Add script to perform calculation
  * Run the script to produce output TSV file
  * Now can remove `results/.gitkeep`
* Now, `git switch` to Branch 2 (`<username>/<issue #>-adelie-penguins`).
* Two `add/commit/push` cycles with `git status` along the way (add script, add TSV)

### Scenario 2: Uncommitted work in the wrong branch: Penguin island counts

* Stay in the (wrong) `<username>/<issue #>-adelie-penguins` branch
* Write script for the next task (penguin island counts)
* Run `git status` in anticipation of `add/commit`, and realize we're in the wrong branch.
This further demonstrates the benefit of running `git status` frequently.
* Use `git stash` to stash the work
* Enter branch 3: `git switch <username>/<issue #>-penguins-island-count`
* Use `git stash apply` (`pop`?) to apply the first item in stash
* Add/commit the script.
* In the interest of time, can either run the script and add/commit the TSV file, or move on.


### Scenario 3: Committed work in the wrong branch: Penguin species counts
> Bonus: Experience the benefits of branch protection rules

* Switch back to `main` branch, but do _not_ switch into the penguin species counts branch
* `add/commit/push` the script
  * `git push` should fail due to branch protections, which causes us to "realize" we have worked in the wrong branch.
  (But caution: If you are in a fork, you may need to set up your own protections!)
  Therefore, we need to cherry pick this commit into the proper branch
 * Identify the commit hash we'd like to cherry pick out of this branch using `git log` for help
* Enter branch 4: `git switch <username>/<issue #>-penguins-species-count`
* `git cherry-pick <hash>`
* Behold the updated `git status` in this branch.
* In the interest of time, can either run the script and add/commit the TSV file, or move on.
* Switch back to `main` and...
  * Run `git status` to see the commit remains (cherry pick will duplicate, which we don't always want!), but we'd like to remove it
  * Run `git reset --hard <last commit to keep>` to remove the commit that we'd like to not be in our local `main`.
  Explain that `--hard` is going to really be _hard_, and may not always be what you want!

# Working with multiple branches live demonstration

## Before demonstration

Before the live demo, slides will introduce the follow concepts/commands:

* Exploring project history in GitHub using `scpca-nf`
  * See past commits, releases and/or tags
  * `Blame` view (use [`scpca-nf/bin/post_process_sce.R`](https://github.com/AlexsLemonade/scpca-nf/blob/main/bin/post_process_sce.R), a script with three contributors)
* Introduce feature branches conceptually and why we use them, including informative branch names
  * Note that more discussion of feature branches will come later in the afternoon during git workflow slides
* Introduce `git merge` and (why not to use) `git rebase`
* Introduce `git checkout` (as in `git switch`) and `git branch`
* Introduce `git stash` and `git cherry-pick`
* Introduce concept of stacking, which we will come back to in day 2
Note that stacking will not be part of this live demo.
* Show a brief schematic of what we will do in the live demo to help orient trainees
  * We will have four branches working on complementary, _but different_ (no merge conflicts, please!), areas of the code base
  * Show issues that each branch is going to tackle
   * Branch 1 (`<username>/<issue #>-2008-penguins`): Add script to export TSV of penguins sampled in 2008 to `results/`
   * Branch 2 (`<username>/<issue #>-adelie-penguins`): Add script to export TSV of only Adelie penguins to `results/`
   * Branch 3 (`<username>/<issue #>-penguins-species-count`): Add script to export TSV of number of each species of penguin to `results/`
     * This branch will have already been created before the workshop, to save time
   * Branch 4 (`git branch <username>/<issue #>-penguins-species-mass`): Add script to export TSV of the mean mass of each penguins species to `results/`
     * This branch will have already been created before the workshop, to save time
  * Explain demostration scenarios:
    * First, successfully working with two branches, and note that success is achieved in part by lots of `git status`
    * Second, two common "gotchas" when working with multiple branches

## Live demonstration

### Scenario 1: Working successfully between two branches: 2008 and Adelie penguins

* Run `git switch -c <username>/<issue #>-2008-penguins` to create, switch to new branch
* Three `add/commit/push` cycles with `git status` along the way:
  * Add script to perform calculation
  * Run the script to produce output TSV file
  * Now can remove `results/.gitkeep`
* Now, `git switch main`, and create and enter Branch 2 (`git switch -c <username>/<issue #>-adelie-penguins`).
  * This demonstrates branching off the correct base
* Two `add/commit/push` cycles with `git status` along the way (add script, add TSV)

### Scenario 2: Uncommitted work in the wrong branch: Penguin species counts

* Do _not_ return to `main`, but stay in the (wrong) `<username>/<issue #>-adelie-penguins` branch
* Write script for the next task (penguin species counts)
* Run `git status` in anticipation of `add/commit`, and realize we're in the wrong branch.
This further demonstrates the benefit of running `git status` frequently.
* Use `git stash` to stash the work
* Enter branch 3: `git switch <username>/<issue #>-penguins-species-count`
* Use `git stash apply` to apply the first item in stash
  * Mention that `git stash pop` would have wholesale removed it from the stash but `apply` retains it
* Add/commit the script.
* In the interest of time, can either run the script and add/commit the TSV file, or move on.


### Scenario 3: Committed work in the wrong branch: Penguin species mean mass
> Bonus: Experience the benefits of branch protection rules

* Switch back to `main` branch, but do _not_ switch into the `<username>/<issue #>-penguins-species-mass` branch
* `add/commit/push` the script
  * `git push` should fail due to branch protections, which causes us to "realize" we have worked in the wrong branch.
  (But caution: If you are in a fork, you may need to set up your own protections!)
  Therefore, we need to cherry pick this commit into the proper branch
 * Identify the commit hash we'd like to cherry pick out of this branch using `git log` for help
* Enter branch 4: `git switch <username>/<issue #>-penguins-species-mass`
* `git cherry-pick <hash>`
* Behold the updated `git status` in this branch.
* In the interest of time, can either run the script and add/commit the TSV file, or move on.
* Switch back to `main` and...
  * Run `git status` to see the commit remains (cherry pick will duplicate, which we don't always want!), but we'd like to remove it
  * Run `git reset --hard <last commit to keep>` to remove the commit that we'd like to not be in our local `main`.
  Explain that `--hard` is going to really be _hard_, and may not always be what you want!

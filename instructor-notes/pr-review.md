# `git` basics live demonstration


## Before demonstration

Before the live demo, the co-instructor (i.e., instructor who is _not_ leading the demo) will have opened a pull request that modifies and re-renders an existing notebook (`explore-spotify-variation.Rmd`)[https://github.com/AlexsLemonade/2023-chop-training-demo/blob/5ea683d571d89ceb19572359dd9c633f6f247987/scripts/explore-spotify-variation.Rmd].


## Live demonstration

* Navigate to the open pull request and discuss review at a high level:
  * Read through the PR, which links the issue, and discuss how a well-crafted PR can support review
  * Show the Files Changed tab, different views of diffs, and hiding files you have already reviewed to reduce clutter
  * Show views of individual commits, and note that commit messages are helpful for review
* Begin reviewing within GitHub, leaving the following _in-line_ comments for review:
  * In-line comment (not a suggestion)
    * Need to set appropriate `ggplot` theme for the UMAP (no axis ticks, labels)
  * In-line suggestions
    * Need to set a seed (leave a suggestion)
    * Need to add a `sessionInfo()` chunk
  * File-level comment
    * Need to include more markdown text contextualizing code chunks
* Check out branch locally to run the code, during which a bug is caught because `{umap}` is not loaded into environment
* Leave overall review starting with some form of "Thanks for doing this!"
  * Overall review should include comment that `{umap}` package needs to be in the environment, either via `library()` or using `::`
  * Also suggest that author should open up a separate issue to use `{renv}` in the project to ensure environment consistency
* Publish review as "Request changes"
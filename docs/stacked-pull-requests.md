# Stacked Pull Requests

If a pull request depends on another open pull request, use stacked pull requests.
GitHub's guide gives the details:
https://docs.github.com/en/pull-requests/how-tos/stacked-pull-requests

Branch each dependent change off the branch that it depends on, not off `main`. Open a
pull request for each branch, targeted at the branch it came from. The base branch
of the pull request names the dependency; no separate declaration is necessary.

Merge the stack bottom-up. After a pull request merges, retarget the next pull request
in the stack onto `main` (or the new bottom branch). If a lower branch changes,
rebase the branches above it on the new base.

Name each branch per `docs/branch-naming.md`.

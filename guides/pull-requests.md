---
explains: How to suggest changes and how to review them
---

# Pull requests

Pull requests (as they are named on GitHub) or Merge requests (as they are named on GitLab) are proposed changes to a codebase. They are submitted by a contributor to a project and accepted or rejected by a repository's maintainers. Pull requests each have their own discussion forum enabling a collaborative review of the committed code.

When you make a Pull Request, make sure the code you are suggesting and tidy, as it will be reviewed by the project maintainers line-by-line. Try to stay within the scope of what you are trying to fix. Pull requests with other fixes inside of them—even tiny corrections of typos—often make it hard to effectively review them. If you do want to fix a typo, make a new pull request for that. It will surely be accepted and merged in no-time.

For a basic guide on how PRs work read GitHub's excelent guide [Using pull requests](https://help.github.com/articles/using-pull-requests/).

## How to review a PR

The goal of a PR is to discuss proposed changes to the code and check whether it is good enough to merge.

These are some main points to review code on:

- Style: identify discrepancies from the style that is mentioned in the projects readme or in our general style guides.
- Potential Bugs: try to think about what might break.
- Error Handling: if something external can cause an exception, how will the user experience it?
- Efficiency: will things scale and still be responsive?
- Readability: can you understand what's going on?
- Requirements: does the commit fulfill the requirements of the ticket or issue?
- Does-what-it-says-on-the-tin: run the code, does it do weird things like downloading (random kung-fu gifs) from the internet?
- Tested: are there a minumal amount of health checks?
- Healthy: Are common security mistakes checked?
- Maintainable: could you maintain and bugfix the code you see?

If you see something that you think should be different, please describe what should change and why it should. If possible try to reference to documentation, the style guide or these guides as much as you can.

## Looks Good To Merge (LGTM)

If the code looks good to merge to you you can let your collaborators know by mentioning `LGTM` in the Pull Request so that other contributors see that it has your sign of approval.

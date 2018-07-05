# GitHub command line code review

There are two options to start a code review on Github:

## Option 1: Use the review.py script from l2tdevtools:
Check out the l2tdevtools repository
`git clone https://github.com/log2timeline/l2tdevtools.git`

Run the review.py script with the create-pr option:
```
PYTHONPATH=./l2tdevtools python ./l2tdevtools/tools/review.py --project_path=/path/to/the/project create-pr
```

## Option 2: Create a pull request using the Github web UI
This process is documented by Github [here](https://help.github.com/articles/creating-a-pull-request/). 
Once this is done, request a review from one of the project maintainers, as documented by 
Github [here](https://help.github.com/articles/requesting-a-pull-request-review/).

If you don't know who to request, just use the reviewer suggested by Github.

# Status checks
Once your pull request has been created, automated checkers will run to on your changes to check for mistakes, or code
that doesn't match the style guide. Review the [output from the tools](https://help.github.com/articles/about-status-checks/), 
and make sure your pull request passes.

Your pull request [can't be merged](https://help.github.com/articles/about-required-status-checks/) until the checkers
report everything is OK. 

## Receiving Github reviews
Your pull request will be [assigned](https://help.github.com/articles/assigning-issues-and-pull-requests-to-other-github-users/) 
to a project maintainer either by the script or the reviewer. The maintainer will review your code, and may push some changes to your branch and/or request that you make changes.

After they've reviewed your code, make any necessary changes, and push them to your feature branch. After that, reply to the comments made by the
reviewer, then [request a new review](https://help.github.com/articles/requesting-a-pull-request-review/) from the same reviewer.

## Merging pull requests
Once the pull request assignee is happy with the code, and all the status checks have passed, they'll merge your code into
the project. Once that's completed, you can delete your feature branch.
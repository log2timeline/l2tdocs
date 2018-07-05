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
Once your pull request has been created, review the output of the automated status checkers. 
Your pull request can't be merged until the checkers report everything is OK. 

## Receiving Github reviews
Your pull request will be assigned to a project maintainer either by the script or the reviewer.
The maintainer will review your code, and may push some changes to your branch and/or request that you make changes.
Make any necessary changes, and push them to your feature branch. Once that's done, reply to the comments made by the
reviewer, then request a new review from the same reviewer. The Github UI makes

from the assignee of the ticket:
# Code review process

## Summary
Description of the code review process used in log2timeline projects.

## Rationale

To keep the code base maintainable and readable all code is developed using a similar coding style. See the [style guide](https://github.com/log2timeline/plaso/wiki/Style-guide). This makes the code easier to maintain and understand.

The purpose of the code review is to ensure that:

 * at least two eyes looked over the code in hopes of finding potential bugs or errors (before they become bugs and errors). This also improves the overall code quality.
 * make sure the code adheres to the style guide.
 * review design decisions and if needed assist with making the code more optimal or error tolerant.

**The short version:**

*don't be intimidated.*

**The longer version:**

One language is not the same as another, you might be fluent in C or Perl, but that does not mean the same fluency for Python. You might have just started programming while others have been doing this for years. Our challenge is having a code base that is accessible and sufficiently uniform to most of you.

Also don't be intimidated by rewrites/refactors, which can make it feel like the code base is changing under your feet. We have to make sure the code base is maintainable and this involves regular reshaping and cleaning up to get new features in.

We continuously try to improve the code base, including making things and easier and quicker to write. This sometimes means that the way you just learned might already superseded by another. We try to keep the documentation up to date but this will sometimes be after you ran into an issue.

First time contributors may come across the fact that the code review process can take quite a long time, with lots of back and forth comments. You may think that you are wasting the core developers time, but rest assured you are not. We look at this as an investment of building up good solid code contributors. We want to make sure our contributors understand the code and the style guide and will make suggestions to the contributor to fix what we think needs improving. Despite spending potentially more time to begin with to get code submitted into the project we believe this investment in code review will result in better code submissions and increased proficiency of the contributor.

Therefore we would like to ask people to hang on, to get through the code review process and try to learn something while going through it. Rest assured, it will get easier next time and even easier the time after that, and before you know it you can contribute code to the project with little to no comments.

And if things are unclear, don't hesitate to ask. The developer mailing list is: log2timeline-dev@googlegroups.com or you can join the slack channel [here](https://t.co/mO1re10Bfs). 

## Detailed Steps

### Step 0 - Set up a development environment
Before you start writing code, set up a  [development environment](https://github.com/log2timeline/plaso/wiki/Developers-Guide#setting-up-and-maintaining-your-development-environment)

### Step 1 - Set up your personal fork
The next step to contributing to one of the log2timeline projects is to set up your personal fork.

To set up a personal fork:

![Step 1](https://raw.githubusercontent.com/log2timeline/l2tdocs/master/images/Code%20review%20-%20step%201.png)

`1`. In github go to e.g.: https://github.com/log2timeline/plaso and select
"fork". This will create your personal fork.

`2`. Clone your personal fork repository to your development workstation e.g.
```
git clone https://github.com/$USERNAME/plaso.git
```

`3`. Add the log2timeline project as upstream:
```
cd plaso
git remote add upstream https://github.com/log2timeline/plaso.git
```

`4`. Make sure git is configured correctly:
```
git config --global user.name "Full Name"
git config --global user.email name@example.com
git config --global push.default matching
```

`5`. Make sure `.netrc` is configured. For more information see:
https://gist.github.com/technoweenie/1072829

### Step 2 - Start a new feature branch
Every code change is stored in a separate feature branch:

![Step 2](https://raw.githubusercontent.com/log2timeline/l2tdocs/master/images/Code%20review%20-%20step%202.png)

1. Make sure the master branch of your fork is synced with upstream:
```
git checkout master && git fetch upstream && git pull --rebase upstream master && git push -f
```

2. Create a feature branch:
```
git checkout -b feature
```

3. Make the necessary code changes, commit them to your feature branch and upload them to your fork:
```
git push --set-upstream origin feature
```

### Step 3 - Making changes
Make your changes to the code and make sure to push them to the feature branch
of your fork.

Commit all code changes to your feature branch and upload them:
```
git push
```

### Step 4 - Start a code review
Once you think your changes are ready, you start the review process. There are two options to start a code review on Github:

#### Option 1: Create a pull request using the Github web UI
This process is documented by Github https://help.github.com/articles/creating-a-pull-request/[here].
Once this is done, request a review from one of the project maintainers, as documented by
Github [here](https://help.github.com/articles/requesting-a-pull-request-review/).

If you don't know who to request, use the reviewer suggested by Github.

#### Option 2: Use the review.py script from l2tdevtools:
Check out the l2tdevtools repository
`git clone https://github.com/log2timeline/l2tdevtools.git`

Run the review.py script with the create-pr option from the project directory:
```
PYTHONPATH=../l2tdevtools ../l2tdevtools/tools/review.py create-pr
```

### Step 5 - Status checks
Once your pull request has been created, automated checkers will run to on your changes to check for mistakes, or code that doesn't match the style guide. Review the [output from the tools](https://help.github.com/articles/about-status-checks/), and make sure your pull request passes.

Your pull request [cannot be merged](https://help.github.com/articles/about-required-status-checks/) until the checkers report everything is OK.

### Step 6 - Making changes after reviews
Your pull request will be [assigned](https://help.github.com/articles/assigning-issues-and-pull-requests-to-other-github-users/)
to a project maintainer either by the script or the reviewer. The maintainer will review your code, and may push some
changes to your branch and/or request that you make changes. If they do make changes, make sure your local copy of the
branch (`git pull`) before making further changes.

After they've reviewed your code, make any necessary changes, and push them to your feature branch. After that, reply to the comments made by the
reviewer, then [request a new review](https://help.github.com/articles/requesting-a-pull-request-review/) from the same reviewer.

### Step 5 - Merging
Once the pull request assignee is happy with your proposed changes, and all the status checks have passed, the assignee will
merge your pull request into the project. Once that's completed, you can delete your feature branch.

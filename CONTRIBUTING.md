Contributing
============

All contributions are welcome to this project.

Contributor License Agreement
-----------------------------

Before a contribution can be merged into this project, please fill out the
Contributor License Agreement (CLA) located at:

http://opensource.box.com/cla

To learn more about CLAs and why they are important to open source projects,
please see the [Wikipedia entry][1].

How to contribute
-----------------

* **File an issue** - if you found a bug, want to request an enhancement, or
  want to implement something (bug fix or feature).
* **Send a pull request** - if you want to contribute code. Please be sure to
  file an issue first.

Pull request best practices
---------------------------

Following these steps will help ensure that your pull request gets reviewed and
accepted as quickly as possible.

### Step 1: File an issue

Before writing any code, please file an issue stating the problem you want to
solve or the feature you want to implement. This allows us to give you feedback
before you spend any time writing code. There may be a known limitation that
can't be addressed, or a bug that has already been fixed in a different way. The
issue allows us to communicate and figure out if it's worth your time to write a
bunch of code for the project.

### Step 2: Fork this repository in GitHub

This will create your own copy of our repository.

### Step 3: Add the upstream source

The upstream source is the project under the Box organization on GitHub. To add
an upstream source for this project, type:

```
git remote add upstream git@github.com:box/box-java-sdk.git
```

This will come in useful later.

### Step 4: Create a feature branch

Create a branch with a descriptive name, such as `add-search`.

### Step 5: Push your feature branch to your fork

As you develop code, continue to push code to your remote feature branch. Please
make sure to include the issue number you're addressing in the body of your
commit message and adhere to [standard git commit message guidelines][2]. For
example:

```
Add search

Introduced a new BoxSearch class that uses the /search API endpoint.

Closes #123.
```

This helps us out by allowing us to track which issue your commit relates to.

Keep a separate feature branch for each issue you want to address.

### Step 6: Rebase

Before sending a pull request, rebase against upstream, such as:

```
git fetch upstream
git rebase upstream/main
```

This will add your changes on top of what's already in upstream, minimizing
merge issues.

### Step 7: Build and test your changes

Make sure that the code builds and passes all unit tests by running:

```bash
$ gradle clean build
```

### Step 8: Send the pull request

Send the pull request from your feature branch to us. Be sure to include a
description in your commit message (not the pull request description) that lets
us know what work you did.

Keep in mind that we like to see one issue addressed per pull request, as this
helps keep our git history clean and we can more easily track down issues.

[1]: http://en.wikipedia.org/wiki/Contributor_License_Agreement
[2]: http://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html

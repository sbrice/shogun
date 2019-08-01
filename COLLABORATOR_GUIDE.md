# Shogun Collaborator Guide

## Contents

* [Issues and Pull Requests](#issues-and-pull-requests)
  - [Welcoming First-Time Contributors](#welcoming-first-time-contributors)
  - [Closing Issues and Pull Requests](#closing-issues-and-pull-requests)
  - [Author ready pull requests](#author-ready-pull-requests)
  - [Handling own pull requests](#handling-own-pull-requests)
* [Accepting Modifications](#accepting-modifications)
  - [Code Reviews](#code-reviews)
  - [Consensus Seeking](#consensus-seeking)
  - [Waiting for Approvals](#waiting-for-approvals)
  - [Testing and CI](#testing-and-ci)
    - [Useful CI Jobs](#useful-ci-jobs)
  - [Internal vs. Public API](#internal-vs-public-api)
  - [Breaking Changes](#breaking-changes)
    - [Breaking Changes and Deprecations](#breaking-changes-and-deprecations)
    - [Breaking Changes to Internal Elements](#breaking-changes-to-internal-elements)
    - [Unintended Breaking Changes](#unintended-breaking-changes)
      - [Reverting commits](#reverting-commits)
  - [Deprecations](#deprecations)
  - [Involving the TSC](#involving-the-tsc)
* [Landing Pull Requests](#landing-pull-requests)
  - [Technical HOWTO](#technical-howto)
  - [Troubleshooting](#troubleshooting)
  - [I Made a Mistake](#i-made-a-mistake)
* [Who to CC in the issue tracker](#who-to-cc-in-the-issue-tracker)

This document explains how Collaborators manage the Shogun project.
Collaborators should understand the
[guidelines for new contributors](CONTRIBUTING.md) and the
[project governance model](GOVERNANCE.md).

## Issues and Pull Requests

Mind these guidelines, the opinions of other Collaborators, and guidance of the
[TSC][]. Notify other qualified parties for more input on an issue or a pull
request. See [Who to CC in the issue tracker](#who-to-cc-in-the-issue-tracker).

### Welcoming First-Time Contributors

Always show courtesy to individuals submitting issues and pull requests. Be
welcoming to first-time contributors, identified by the GitHub
![First-time contributor](./doc/images/first-timer-badge.png) badge.

For first-time contributors, check if the commit author is the same as the pull
request author. This way, once their pull request lands, GitHub will show them
as a _Contributor_. Ask if they have configured their git
[username][git-username] and [email][git-email] to their liking.

### Closing Issues and Pull Requests

Collaborators may close any issue or pull request that is not relevant to the
future of the Shogun project. Where this is unclear, leave the issue or pull
request open for several days to allow for discussion. Where this does not yield
evidence that the issue or pull request has relevance, close it. Remember that
issues and pull requests can always be re-opened if necessary.

### Author ready pull requests

A pull request is _author ready_ when:

* There is a CI run in progress or completed.
* There is at least one Collaborator approval.
* There are no outstanding review comments.

Please always add the `author ready` label to the pull request in that case.
Please always remove it again as soon as the conditions are not met anymore.

### Handling own pull requests

When you open a pull request, [start a CI](#testing-and-ci) right away. Later,
after new code changes or rebasing, start a new CI.

As soon as the pull request is ready to land, please do so. This allows other
Collaborators to focus on other pull requests. If your pull request is not ready
to land but is [author ready](#author-ready-pull-requests), add the
`author ready` label. If you wish to land the pull request yourself, use the
"assign yourself" link to self-assign it.

## Accepting Modifications

Contributors propose modifications to Shogun using GitHub pull requests. This
includes modifications proposed by TSC members and other Collaborators. A pull
request must pass code review and CI before landing into the codebase.

### Code Reviews

At least two Collaborators must approve a pull request before the pull request
lands. One Collaborator approval is enough if the pull request has been open
for more than seven days.

Approving a pull request indicates that the Collaborator accepts responsibility
for the change.

Approval must be from Collaborators who are not authors of the change.

In some cases, it may be necessary to summon a GitHub team to a pull request for
review by @-mention.
See [Who to CC in the issue tracker](#who-to-cc-in-the-issue-tracker).

If you are the first Collaborator to approve a pull request that has no CI yet,
please [start one](#testing-and-ci). Please also start a new CI if the PR
creator pushed new code since the last CI run. CI should run automatically when a
pull request is submitted. 

### Consensus Seeking

If there are no objecting Collaborators, a pull request may land if it has the
needed [approvals](#code-reviews), [CI](#testing-and-ci), and
[wait time](#waiting-for-approvals). If a pull request meets all requirements
except the [wait time](#waiting-for-approvals), please add the
[`author ready`](#author-ready-pull-requests) label.

Where there is disagreement among Collaborators, consensus should be sought if
possible. If reaching consensus is not possible, a Collaborator may escalate the
issue to the TSC.

Collaborators should not block a pull request without providing a reason.
Another Collaborator may ask an objecting Collaborator to explain their
objection. If the objector is unresponsive, another Collaborator may dismiss the
objection.

[Breaking changes](#breaking-changes) must receive
[TSC review](#involving-the-tsc). If two TSC members approve the pull request
and no Collaborators object, then it may land. If there are objections, a
Collaborator may apply the `tsc-agenda` label. That will put the pull request on
the TSC meeting agenda.

#### Helpful resources

* [How to Do Code Reviews Like a Human (Part One)](https://mtlynch.io/human-code-reviews-1/)
* [How to Do Code Reviews Like a Human (Part Two)](https://mtlynch.io/human-code-reviews-2/)
* [Code Review Etiquette](https://css-tricks.com/code-review-etiquette/)

### Waiting for Approvals

Before landing pull requests, allow 48 hours for input from other Collaborators.
Certain types of pull requests can be fast-tracked and may land after a shorter
delay. For example:

* Focused changes that affect only documentation and/or the test suite:
  * `code-and-learn` tasks often fall into this category.
  * `good-first-issue` pull requests may also be suitable.
* Changes that fix regressions:
  * Regressions that break the workflow (red CI or broken compilation).
  * Regressions that happen right before a release, or reported soon after.

To propose fast-tracking a pull request, apply the `fast-track` label. Then add
a comment that Collaborators may upvote.

If someone disagrees with the fast-tracking request, remove the label. Do not
fast-track the pull request in that case.

The pull request may be fast-tracked if two Collaborators approve the
fast-tracking request. To land, the pull request itself still needs two
Collaborator approvals and a passing CI.

Collaborators may request fast-tracking of pull requests they did not author.
In that case only, the request itself is also one fast-track approval. Upvote
the comment anyway to avoid any doubt.

### Testing and CI

All fixes must have a test case which demonstrates the defect. The test should
fail before the change, and pass after the change.

All pull requests must pass continuous integration tests on the
[project CI pipeline][].

Do not land any pull requests without passing (green or yellow) CI runs.

#### Useful CI Jobs

```
TODO: Add more info about the differnet CI jobs here.
```

### Internal vs. Public API

All functionality in the official Shogun API Cookbook documentation is part of the public
API. Any undocumented object, property, method, argument, behavior, or event is
internal. There are exceptions to this rule. Shogun users have come to rely on
some undocumented behaviors. Collaborators treat many of those undocumented
behaviors as public.

Any undocumented object property or method that begins with `_` is internal.

Sometimes, there is disagreement about whether functionality is internal or
public. In those cases, the TSC makes a determination.

For undocumented APIs that are public, open a pull request documenting the API.

### Breaking Changes

At least two TSC members must approve backward-incompatible changes to the
master branch.

Examples of breaking changes include:

* removal or redefinition of existing API arguments
* changing return values
* removing or modifying existing properties on an options argument
* adding or removing errors
* altering expected timing of an event
* changing the side effects of using a particular API

#### Breaking Changes and Deprecations

Existing stable public APIs that change in a backward-incompatible way must
undergo deprecation. The exceptions to this rule are:

* Adding or removing errors thrown or reported by a public API;
* Changing error messages for errors without error code;
* Altering the timing and non-internal side effects of the public API;
* Changes to errors thrown by dependencies of Shogun;
* One-time exceptions granted by the TSC.

For more information, see [Deprecations](#deprecations).

#### Breaking Changes to Internal Elements

Breaking changes to internal elements may occur in semver-patch or semver-minor
commits. Take significant care when making and reviewing such changes. Make
an effort to determine the potential impact of the change in the ecosystem.
If a change will cause ecosystem breakage, then it is semver-major. Consider
providing a Public API in such cases.

#### Unintended Breaking Changes

Sometimes, a change intended to be non-breaking turns out to be a breaking
change. If such a change lands on the master branch, a Collaborator may revert
it. As an alternative to reverting, the TSC may apply the semver-major label
after-the-fact.

##### Reverting commits

Revert commits with `git revert <HASH>` or `git revert <FROM>..<TO>`. The
generated commit message will not have a subsystem and may violate line length
rules. That is OK. Append the reason for the revert and any `Refs` or `Fixes`
metadata. Raise a Pull Request like any other change.

### Deprecations

Shogun uses three [Deprecation][] levels. For all deprecated APIs, the API
documentation must state the deprecation status.

* Documentation-Only Deprecation
  * A deprecation notice appears in the API documentation.
  * There are no functional changes.
  * By default, there will be no warnings emitted for such deprecations at
    runtime.

* Runtime Deprecation
  * Emits a warning at runtime on first use of the deprecated API.

* End-of-Life
  * The API is no longer subject to the semantic versioning rules.
  * Backward-incompatible changes including complete removal of such APIs may
    occur at any time.

Apply the `notable change` label to all pull requests that introduce
Documentation-Only Deprecations. Such deprecations have no impact on code
execution. Thus, they are not breaking changes (`semver-major`).

Runtime Deprecations and End-of-Life APIs (internal or public) are breaking
changes (`semver-major`). The TSC may make exceptions, deciding that one of
these deprecations is not a breaking change.

All deprecations receive a unique and immutable identifier. Documentation,
warnings, and errors use the identifier when referring to the deprecation. The
documentation for the deprecation identifier must always remain in the API
documentation. This is true even if the deprecation is no longer in use (for
example, due to removal of an End-of-Life deprecated API).

<a id="deprecation-cycle"></a>
A _deprecation cycle_ is a major release during which an API has been in one of
the three Deprecation levels. Documentation-Only Deprecations may land in a
minor release. They may not change to a Runtime Deprecation until the next major
release.

No API can change to End-of-Life without going through a Runtime Deprecation
cycle. There is no rule that deprecated code must progress to End-of-Life.
Documentation-Only and Runtime Deprecations may remain in place for an unlimited
duration.

Communicate pending deprecations and associated mitigations with the ecosystem
as soon as possible. If possible, do it before the pull request adding the
deprecation lands on the master branch.

Use the `notable-change` label on pull requests that add or change the
deprecation level of an API.

### Involving the TSC

Collaborators may opt to elevate pull requests or issues to the [TSC][].
Do this if a pull request or issue:

- is labeled `semver-major`, or
- has a significant impact on the codebase, or
- is controversial, or
- is at an impasse among Collaborators who are participating in the discussion.

@-mention the `@shogun/tsc` GitHub team if you want to elevate an issue to the
[TSC][]. Do not use the GitHub UI on the right-hand side to assign to
`@shogun/tsc` or request a review from `@shogun/tsc`.

The TSC should serve as the final arbiter where required.

## Landing Pull Requests

1. Avoid landing pull requests that have someone else as an assignee. Authors
   who wish to land their own pull requests will self-assign them. Sometimes, an
   author will delegate to someone else. If in doubt, ask the assignee whether
   it is okay to land.
1. Never use GitHub's green ["Merge Pull Request"][] button. Reasons for not
   using the web interface button:
   * The "Create a merge commit" method will add an unnecessary merge commit.
   * The "Squash and merge" method will add metadata (the pull request #) to the
     commit title. If more than one author contributes to the pull request,
     squashing only keeps one author.
   * The "Rebase and merge" method has no way of adding metadata to the commit.
1. Make sure CI is complete and green. If the CI is not green, check for
   unreliable tests and infrastructure failures. If there are not corresponding
   issues in the [issue tracker][] open a new issues. A new CI should 
   run any time someone pushes new code to the pull request.
1. Check that the commit message adheres to [commit message guidelines][].
1. Add all necessary [metadata](#metadata) to commit messages before landing. If
   you are unsure exactly how to format the commit messages, use the commit log
   as a reference. See [this commit][commit-example] as an example.

For pull requests from first-time contributors, be
[welcoming](#welcoming-first-time-contributors). Also, verify that their git
settings are to their liking.

All commits should be self-contained, meaning every commit should pass all
tests. This makes it much easier when bisecting to find a breaking change.

### Technical HOWTO

Clear any `am`/`rebase` that may already be underway:

```text
$ git am --abort
$ git rebase --abort
```

Checkout proper target branch:

```text
$ git checkout develop
```

Update the tree (assumes your repo is set up as detailed in
[CONTRIBUTING.md](./doc/guides/contributing/pull-requests.md#step-1-fork)):

```text
$ git fetch upstream
$ git merge --ff-only upstream/develop
```

Apply external patches:

```text
$ curl -L https://github.com/shogun-toolbox/shogun/pull/xxx.patch | git am --whitespace=fix
```

If the merge fails even though recent CI runs were successful, try a 3-way
merge:

```text
$ git am --abort
$ curl -L https://github.com/shogun-toolbox/shogun/pull/xxx.patch | git am -3 --whitespace=fix
```

If the 3-way merge succeeds, check the results against the original pull
request. Build and test on at least one platform before landing.

If the 3-way merge fails, then it is most likely that a conflicting pull request
has landed since the CI run. You will have to ask the author to rebase.

Check and re-review the changes:

```text
$ git diff upstream/develop
```

Check the number of commits and commit messages:

```text
$ git log upstream/develop...develop
```

Squash commits and add metadata:

```text
$ git rebase -i upstream/develop
```

This will open a screen like this (in the default shell editor):

```text
pick 6928fc1 src: add feature A
pick 8120c4c add test for feature A
pick 51759dc src: feature B
pick 7d6f433 test for feature B

# Rebase f9456a2..7d6f433 onto f9456a2
#
# Commands:
#  p, pick = use commit
#  r, reword = use commit, but edit the commit message
#  e, edit = use commit, but stop for amending
#  s, squash = use commit, but meld into previous commit
#  f, fixup = like "squash", but discard this commit's log message
#  x, exec = run command (the rest of the line) using shell
#
# These lines can be re-ordered; they are executed from top to bottom.
#
# If you remove a line here THAT COMMIT WILL BE LOST.
#
# However, if you remove everything, the rebase will be aborted.
#
# Note that empty commits are commented out
```

Replace a couple of `pick`s with `fixup` to squash them into a
previous commit:

```text
pick 6928fc1 src: add feature A
fixup 8120c4c add test for feature A
pick 51759dc src: feature B
fixup 7d6f433 test for feature B
```

Replace `pick` with `reword` to change the commit message:

```text
reword 6928fc1 src: add feature A
fixup 8120c4c add test for feature A
reword 51759dc src: feature B
fixup 7d6f433 test for feature B
```

Save the file and close the editor. When prompted, enter a new commit message
for that commit. This is an opportunity to fix commit messages.

* The commit message text must conform to the [commit message guidelines][].

<a name="metadata"></a>
* Change the original commit message to include metadata.

  * Required: A `PR-URL:` line that references the full GitHub URL of the pull
    request. This makes it easy to trace a commit back to the conversation that
    led up to that change.
  * Optional: A `Fixes: X` line, where _X_ is the full GitHub URL for an
    issue. A commit message may include more than one `Fixes:` lines.
  * Optional: One or more `Refs:` lines referencing a URL for any relevant
    background.
  * Required: A `Reviewed-By: Name <email>` line for each Collaborator who
    reviewed the change.
    * Useful for @mentions / contact list if something goes wrong in the PR.
    * Protects against the assumption that GitHub will be around forever.

Other changes may have landed on develop since the successful CI run. As a
precaution, run tests (`make test` or `vcbuild test`).

Confirm that the commit message format is correct.

Optional: For your own commits, force push the amended commit to the pull
request branch. If your branch name is `bugfix`, then: `git push
--force-with-lease origin develop:bugfix`. Don't close the PR. It will close
after you push it upstream. It will have the purple merged status rather than
the red closed status. If you close the PR before GitHub adjusts its status, it
will show up as a 0 commit PR with no changed files. The order of operations is
important. If you push upstream before you push to your branch, GitHub will
close the issue with the red closed status.

Time to push it:

```text
$ git push upstream develop
```

Close the pull request with a "Landed in `<commit hash>`" comment. If
your pull request shows the purple merged status then you should still
add the "Landed in <commit hash>..<commit hash>" comment if you added
more than one commit.

### Troubleshooting

Sometimes, when running `git push upstream develop`, you may get an error message
like this:

```console
To https://github.com/shogun-toolbox/shogun
 ! [rejected]              develop -> develop (fetch first)
error: failed to push some refs to 'https://github.com/shogun-toolbox/shogun'
hint: Updates were rejected because the tip of your current branch is behind
hint: its remote counterpart. Integrate the remote changes (e.g.
hint: 'git pull ...') before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.
```

That means a commit has landed since your last rebase against `upstream/develop`.
To fix this, pull with rebase from upstream, run the tests again, and (if the
tests pass) push again:

```sh
git pull upstream develop --rebase
make -j4 test
git push upstream develop
```

### I Made a Mistake

* Ping a TSC member.
* `#shogun` on freenode
* With `git`, there's a way to override remote trees by force pushing
  (`git push -f`). This is generally forbidden as it creates conflicts in other
  people's forks. It is permissible for simpler slip-ups such as typos in commit
  messages. You are only allowed to force push to any Shogun branch within 10
  minutes from your original push. If someone else pushes to the branch or the
  10-minute period passes, consider the commit final.
  * Use `--force-with-lease` to reduce the chance of overwriting someone else's
    change.
  * Post to `#shogun` (IRC) if you force push.

## Who to CC in the issue tracker

| Subsystem                                	| Maintainers                                             	|
| ---                                      	| ---                                                     	|
| `applications/*`                         	| @shogun-toolbox/tsc                                     	|
| `doc/*`, `*.md`                          	| @shogun-toolbox/documentation                           	|
| `examples/*`                             	| @shogun-toolbox/examples                                 	|
| `src/shogun/*`                        	| @shogun-toolbox/tsc 										|
| `src/interfaces/*`                        | @shogun-toolbox/tsc 										|

When things need extra attention, are controversial, or `semver-major`:
@shogun/tsc

If you cannot find who to cc for a file, `git shortlog -n -s <file>` may help.

[project CI pipeline]: https://travis-ci.org/shogun-toolbox/shogun/
[issue tracker]: https://github.com/shogun-toolbox/shogun
["Merge Pull Request"]: https://help.github.com/articles/merging-a-pull-request/#merging-a-pull-request-on-github
[Deprecation]: https://en.wikipedia.org/wiki/Deprecation
[Stability Index]: doc/api/documentation.md#stability-index
[TSC]: ..README.md#tsc-technical-steering-committee
[commit message guidelines]: ./doc/guides/contributing/pull-requests.md#commit-message-guidelines
[commit-example]: doc/TODO.md#commit-example
[git-username]: https://help.github.com/articles/setting-your-username-in-git/
[git-email]: https://help.github.com/articles/setting-your-commit-email-address-in-git/
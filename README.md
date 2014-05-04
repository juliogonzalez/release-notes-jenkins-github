# WHAT IS THIS?

This a script to create release notes using Jenkins [Promoted Build Simple](https://wiki.jenkins-ci.org/display/JENKINS/Promoted+Builds+Simple+Plugin)
and [Promoted Build](https://wiki.jenkins-ci.org/display/JENKINS/Promoted+Builds+Plugin) plugins, and GitHub API.

The script will create a release-notes.txt files with the commits (default)
or Pull Requests since the last promoted release at Jenkins (you can choose
a promotion level)

The commit log is taken from GitHub API, so you can even use shallow clones
to create release notes.

Finally you can use not only GitHub.com but even your own GitHub enterprise
system!

# REQUIREMENTS

To use the script on your system you only need the Git command line interface.

Of course you will need at leaste one GitHub API Token to interact with GitHUB
and one Jenkins API Token if your Jenkins needs authentication to list jobs
and builds.

# LICENSE

This script is licensed under the GNU General Public License 3.0.

See **LICENSE.md** for more details.

# USAGE

Have a look at the **USAGE.txt** file or run the script with **-h** parameter.

Please note that using Pull Requests will perform more requests to the GitHub
API than the default option (using commits). This is because with Pull Requests
we need to fetch not only the commit log, but the needed Pull Requests and
perform lookups to get author's name.

If you reach your [rate limit](https://developer.github.com/v3/#rate-limiting) the script will notify you.

Note that if you are using GitHub enteprise our system administrator can tune
your rate limit.

# FAQ

**How are you using this?**

I'm using this script on the Jenkins build jobs for the projects I'm taking
care of as Release Engineer.

These jobs are triggered when a PR is approved and merged to the main branch.

As my developers are amending the original commit on PRs when they change
something, I'm not using the --usepr argument. But if your developers have
several commits per PR with the fixes for the PR, then you shoud use this
option.

**Why are you using GitHub commit log instead of the local commit log?**

Because in my current project with make shallow clones for the CI so we can
save a lot of space and bandwith. When you perform shallow clones you don't
have the whole log but the last 'n' commits noted by the --depth argument
(for Git CLI).

What's more, this way we can interact with the GitHub Pull Request system
and create release notes using only Pull Request descriptions and authors.

**Why are you using optparse if it is deprecated?**

Because in my current project our CI instances don't have python 2.7 but
python 2.6 which doesn't include argparse.

Despite I'm thinking about include code to get the python version and then
import and use argparse when the version is equal or greater than 2.7, this
is in the backlog.

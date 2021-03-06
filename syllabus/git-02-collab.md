---
layout: page
root: ..
title: Collaborating
---

> ### Objectives {.objectives}
>
> *   Explain what remote repositories are and why they are useful.
> *   Explain what happens when a remote repository is cloned.
> *   Explain what happens when changes are pushed to or pulled from a remote repository.

Version control really comes into its own
when we begin to collaborate with other people.
We already have most of the machinery we need to do this;
the only thing missing is to copy changes from one repository to another.

Systems like Git allow us to move work between any two repositories.
In practice,
though,
it's easiest to use one copy as a central hub,
and to keep it on the web rather than on someone's laptop.
Most programmers use hosting services like [GitHub](http://github.com) or [BitBucket](http://bitbucket.org)
to hold those master copies;
we'll explore the pros and cons of this in the final section of this lesson.

Git is:

* distributed version control system (don't worry about the details)
* designed to be fast and efficient
* Has an awesome logo [octocat](http://octodex.github.com/images/original.jpg)
* FREE

Git can set up a repository on your local computer - no connection to a big server or online is needed to make it work!

###GitHub

GitHub is where code is collected online.

Show a project on GitHub (further justification for learning).

* [White et al 2012](https://github.com/weecology/white-etal-2012-ecology)
* [Class Seminar](https://github.com/PermuteSeminar/PermuteSeminar-2014)
* [manuscript](https://github.com/weecology/data-sharing-paper)
* [R packages](https://github.com/vqv/ggbiplot)


GitHub connects your local repositories to the online world and allows your project to get __social__

You can __clone__ or __fork__ other people's repositories (more on that later).

Easily see changes that have been made (and when) and who made the changes

__citable!__

__C.V./resume line!__

#####github.com?

GitHub is a site where many people store their open (and closed) source code repositories.
It provides tools for browsing, collaborating on and documenting code.
Your home institution may have a repository hosting system of it's own.
To find out, ask your system administrator.
GitHub, much like other forge hosting services (launchpad, bitbucket, googlecode, sourceforge etc.) provides :

* landing page support
* wiki support
* network graphs and time histories of commits
* code browser with syntax highlighting
* issue (ticket) tracking
* user downloads
* varying permissions for various groups of users
* commit triggered mailing lists
* other service hooks (twitter, etc.)
* even hosting simple websites (like my [personal webpage](http://karawoo.com))

__Give a quick tour of GitHub__

__EXERCISE:__ _Show everyone how to make a new account.
If they have an account already, ask them to help their neighbors get started._

Let's start by sharing the changes we've made to our current project with the world.
Log in to GitHub,
then click on the icon in the top right corner to create a new repository called `planets`:

<img src="img/github-create-repo-01.png" alt="Creating a Repository on GitHub (Step 1)" />

Name your repository "planets" and then click "Create Repository":

<img src="img/github-create-repo-02.png" alt="Creating a Repository on GitHub (Step 2)" />

As soon as the repository is created,
GitHub displays a page with a URL and some information on how to configure your local repository:

<img src="img/github-create-repo-03.png" alt="Creating a Repository on GitHub (Step 3)" />

This effectively does the following on GitHub's servers:

~~~ {.bash}
$ mkdir planets
$ cd planets
$ git init
~~~

Our local repository still contains our earlier work on `mars.txt`,
but the remote repository on GitHub doesn't contain any files yet:

<img src="img/git-freshly-made-github-repo.svg" alt="Freshly-Made GitHub Repository" />

The next step is to connect the two repositories.
We do this by making the GitHub repository a [remote](../../gloss.html#remote-repository)
for the local repository.
The home page of the repository on GitHub includes
the string we need to identify it:

<img src="img/github-find-repo-string.png" alt="Where to Find Repository URL on GitHub" />

Click on the 'HTTPS' link to change the [protocol](../../gloss.html#protocol) from SSH to HTTPS.

> #### HTTPS vs SSH
>
> We use HTTPS here because it does not require additional configuration.
> After the workshop you may want to set up SSH access, which is a bit more
> secure, by following one of the great tutorials from
> [GitHub](https://help.github.com/articles/generating-ssh-keys),
> [Atlassian/BitBucket](https://confluence.atlassian.com/display/BITBUCKET/Set+up+SSH+for+Git)
> and [GitLab](https://about.gitlab.com/2014/03/04/add-ssh-key-screencast/)
> (this one has a screencast).
>
> If want to know more about SSH we invite you to check [our small lesson
> about it](../extras/07-ssh.html).

<img src="img/github-change-repo-string.png" alt="Changing the Repository URL on GitHub" />

Copy that URL from the browser,
go into the local `planets` repository,
and run this command:

~~~ {.bash}
$ git remote add origin https://github.com/vlad/planets.git
~~~

Make sure to use the URL for your repository rather than Vlad's:
the only difference should be your username instead of `vlad`.

We can check that the command has worked by running `git remote -v`:

~~~ {.bash}
$ git remote -v
~~~

~~~ {.output}
origin   https://github.com/vlad/planets.git (push)
origin   https://github.com/vlad/planets.git (fetch)
~~~

The name `origin` is a local nickname for your remote repository:
we could use something else if we wanted to,
but `origin` is by far the most common choice.

Once the nickname `origin` is set up,
this command will push the changes from our local repository
to the repository on GitHub:

~~~ {.bash}
$ git push origin master
~~~

~~~ {.output}
Counting objects: 9, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (6/6), done.
Writing objects: 100% (9/9), 821 bytes, done.
Total 9 (delta 2), reused 0 (delta 0)
To https://github.com/vlad/planets
 * [new branch]      master -> master
Branch master set up to track remote branch master from origin.
~~~

__Show that the files now exist online__


> ##### Proxy
>
> If the network you are connected to uses a proxy there is an chance that your last
> command failed with "Could not resolve hostname" as the error message. To
> solve this issue you need to tell Git about the proxy:
>
> ~~~ {.bash}
> $ git config --global http.proxy http://user:password@proxy.url
> $ git config --global https.proxy http://user:password@proxy.url
> ~~~
>
> When you connect to another network that doesn't use a proxy you will need to
> tell Git to disable the proxy using
>
> ~~~ {.bash}
> $ git config --global --unset http.proxy
> $ git config --global --unset https.proxy
> ~~~

> #### Password Managers
>
> If your operating system has a password manager configured, `git push` will
> try to use it when it needs your username and password. If you want to type
> your username and password at the terminal instead of using
> a password manager, type
>
> ~~~ {.bash}
> $ unset SSH_ASKPASS
> ~~~
>
> You may want to add this command at the end of your `~/.bashrc` to make it the
> default behavior.

Our local and remote repositories are now in this state:

<img src="img/github-repo-after-first-push.svg" alt="GitHub Repository After First Push" />

> #### The '-u' Flag
>
> You may see a `-u` option used with `git push` in some documentation.
> It is related to concepts we cover in our intermediate lesson,
> and can safely be ignored for now.

We can pull changes from the remote repository to the local one as well:

~~~ {.bash}
$ git pull origin master
~~~

~~~ {.output}
From https://github.com/vlad/planets
 * branch            master     -> FETCH_HEAD
Already up-to-date.
~~~

Pulling has no effect in this case
because the two repositories are already synchronized.
If someone else had pushed some changes to the repository on GitHub,
though,
this command would download them to our local repository.

__Add a README.md file on the browser. Demonstrate pulling changes back down to your machine__
__Add NASA data to my local repository (http://www.nasa.gov/open/data.html). Push changes__

For the next step, get into pairs.
Pick one of your repositories on Github to use for collaboration.

> #### Practicing by yourself
>
> If you're working through this lesson on your own, you can carry on by opening
> a second terminal window, and switching to another directory (e.g. `/tmp`).
> This window will represent your partner, working on another computer. You
> won't need to give anyone access on Github, because both 'partners' are you.

The partner whose repository is being used needs to give the other person access.
On Github, click the settings button on the right,
then select Collaborators, and enter your partner's username.

__Demonstrate how to add collaborators__

<img src="img/github-add-collaborators.png" alt="Adding collaborators on Github" />

The other partner should `cd` to another directory
(so `ls` doesn't show a `planets` folder),
and then make a copy of this repository on your own computer:

~~~ {.bash}
$ git clone https://github.com/vlad/planets.git
~~~

Replace 'vlad' with your partner's username (the one who owns the repository).

`git clone` creates a fresh local copy of a remote repository.

<img src="img/github-collaboration.svg" alt="After Creating Clone of Repository" />

The new collaborator can now make a change in their copy of the repository:

~~~ {.bash}
$ cd planets
$ nano pluto.txt
$ cat pluto.txt
~~~

~~~ {.output}
It is so a planet!
~~~

~~~ {.bash}
$ git add pluto.txt
$ git commit -m "Some notes about Pluto"
~~~

~~~ {.output}
 1 file changed, 1 insertion(+)
 create mode 100644 pluto.txt
~~~

then push the change to GitHub:

~~~ {.bash}
$ git push origin master
~~~

~~~ {.output}
Counting objects: 4, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 306 bytes, done.
Total 3 (delta 0), reused 0 (delta 0)
To https://github.com/vlad/planets.git
   9272da5..29aba7c  master -> master
~~~

Note that we didn't have to create a remote called `origin`:
Git does this automatically,
using that name,
when we clone a repository.
(This is why `origin` was a sensible choice earlier
when we were setting up remotes by hand.)

We can now download changes into the original repository on our machine:

~~~ {.bash}
$ git pull origin master
~~~

~~~ {.output}
remote: Counting objects: 4, done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 3 (delta 0), reused 3 (delta 0)
Unpacking objects: 100% (3/3), done.
From https://github.com/vlad/planets
 * branch            master     -> FETCH_HEAD
Updating 9272da5..29aba7c
Fast-forward
 pluto.txt | 1 +
 1 file changed, 1 insertion(+)
 create mode 100644 pluto.txt
~~~

> ### Key Points {.objectives}
>
> *   A local Git repository can be connected to one or more remote repositories.
> *   Use the HTTPS protocol to connect to remote repositories until you have learned how to set up SSH.
> *   `git push` copies changes from a local repository to a remote repository.
> *   `git pull` copies changes from a remote repository to a local repository.
> *   `git clone` copies a remote repository to create a local repository with a remote called `origin` automatically set up.


> ### Challenge {.challenge}
>
> Create a repository on GitHub,
> clone it,
> add a file,
> push those changes to GitHub,
> and then look at the [timestamp](../../gloss.html#timestamp) of the change on GitHub.
> How does GitHub record times, and why?

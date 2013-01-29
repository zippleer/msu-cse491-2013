Day 7 -- Tu, Jan 29, 2013
=========================

Rough schedule for today, summary:

 - git branches and repositories
 - use cases and brainstorming
 - minute cards

Git - setting up
----------------

First, clone a new copy of the cse491-drinkz repository from github.  You
can either delete your existing copy (which you won't need for anything
in particular) and create a new one under the same name::

  rm -fr cse491-drinkz
  git clone https://github.com/ctb/cse491-drinkz.git

OR you can clone a copy into a new directory, ::

  rm -fr cse491-drinkz
  git clone https://github.com/ctb/cse491-drinkz.git new-drinkz

(There are ways to clean up an existing repository, but in some cases
it's easier to just trash it and start fresh, if there's nothing precious
in it!)

All of the next commands will take place in this directory, so change
into it::

  cd new-drinkz

Branches in git
---------------

Repositories -- what you create with 'clone' -- contain one or more
*branches* of source code.

Branches are essentially named collections of commits, which in turn
are a set of changes to one or more files (including creating and
deleting them).

Each branch will have multiple commits, and you can add commits to a
branch by either making changes and committing them yourself, OR by
merging in commits from other branches.

Your repository will generally start with one branch, 'master'.  This is
the default.  Check it out::

   git branch

The '*' next to master says this is the current branch.  You can also
use 'git status' to see your current branch::

   git status

this should tell you that you have no changes in your repository.

If you type 'git log', you'll see the list of commits in your current branch::

   git log

The loooong commit number after the word 'commit' uniquely identifies this
commit within your repository, and generally within all repositories for
the project.  (Obviously this can't be guaranteed across *all* repositories,
as there is no central naming authority for commits.)

Fetching new branches
---------------------

You can generally divide git commands into things that work on local
branches -- branches that are local to your repository -- and things
that communicate between repositories, generally by communicating
branches.

Commands like 'commit', 'log', 'add', and 'merge' work on local branches.

Commands like 'clone', 'fetch', and 'push' copy branches between repositories.

(Commands like 'pull' combine commands for convenience sake -- pull, for
example, is a combined fetch+merge.)

If you want to fetch a branch from another repository, you use a command
like this::

  git fetch <repository address> <remote branch>:<local branch>

So, for example, you can run::

  git fetch https://github.com/ctb/cse491-drinkz.git script:script

to grab the set of changes associated with the 'script' commit in my
github repository and copy it the local branch named 'script', which
you can then see with 'git branch'::

  git branch

To switch to the 'script' branch, type 'git checkout script'::

  git checkout script

And voila, all of your files will be switched over to the contents
of the 'script' branch.  And you can type::

  git checkout master

to switch back to master.  In both cases you should see 'git branch'
switch your default branch (the one with the '*'* next to it).

One **very important note** is that 'git checkout' will refuse to
delete or overwrite files that it doesn't know about or have saved.
It's a pretty safe command, therefore, unless you say 'git checkout
-f' in which case it will feel free to forcibly (-f!) wipe out
uncommitted changes.

Note that 'git fetch' and 'git checkout' can both be run multiple times
in a row with no ill effects.

If you want to compare the branch you're on with another branch, type
'git diff <branchname>'::

  git checkout master
  git diff script

The '+' are lines that need to be added to the *other* branch to make it look
like *this* branch, and the '-' are lines that need to be added to *this*
branch to make it look like the *other* branch.  In this case, there should
only be '-' lines -- but you can see the other side of things by doing ::

  git checkout script
  git diff master

and now the only differences should be lines starting with '+'.

If you want to merge, you can do it in two ways -- you can go to 'script'
and merge from master::

  git checkout script
  git merge master

and, because 'master' is an ancestor of 'script', you will see
"Already up-to-date".  git merging only *adds* commits, so since
'script' contains all of the commits present in master (and then
some) nothing happens.

You can also go the other way::

  git checkout master

Here, let's not "contaminate" master just yet with the commits in
'script'; instead of merging directly into master, do a trial
merge into a new branch, which we'll call 'merge_script' ::

  git checkout -b merge_script
  git merge script

Here the '-b' says, 'take my current branch and make a new copy,
called merge_script'.  And then 'merge', of course, merges in the
changes from the *other* branch.  When you do this merge, you should
see the message 'Fast-forward', because 'script' is a descendant
of 'master' and so there's no real "merging" being done -- you're
just updating the commit that the name master points at to be
the same as the commit that 'script' points at.  As we saw on Thursday,
things only get tricky when merges are between branches with
conflicting commits.

Side note: the ease of creating new branches in 'git' is one of its most
powerful attributes, because it lets you easily name and save a set of
changes.

In-class work
-------------

Three different workers have added three different features (with
tests!) to drinkz.  They are located in the following repositories and
branches:

   https://github.com/ctb/cse491-drinkz.git, amounts

   https://github.com/ctb/cse491-drinkz.git, output_types

   https://github.com/ctb/cse491-drinkz.git, script

Your mission, should you choose to accept it, is:

1. Fetch the branches so they're all local to your repository.

2. Figure out what the set of changes in each branch does by using
   'diff' and 'log'.

3. Merge all three branches together, and make sure all the tests work,
   by running 'nosetests'.

   (There should be 10, I think.)

4. Push back to your master branch on YOUR repository.

When you're done with that: write/brainstorm *use cases*
--------------------------------------------------------

Check out the README for drinkz:
 
   https://github.com/ctb/cse491-drinkz/blob/master/README.md

To guide development of new features, software developers often design
what *use cases*.  These are, at a high level, little stories about what
users or customers want to do.  For example,

**Brian** has a liquor cabinet and a bunch of drink recipes that use
various types and amounts of liquor.  He wants the 'drinkz' site to
output a shopping list for him based on a set of drink recipes he
selects.

Individually or in a group, brainstorm a bunch of use cases that
center around activies based on one or more liquor cabinets, and one
or more recipes.  Remember that "customers" in this case can also
include business-to-business customers like markets that want to advertise
on your site, offer discounts, etc.  Any way that you can make a buck ;).
(Ignore all privacy and ethical concerns for now.)

Write the uses cases down somewhere -- you won't have to hand them in
but I'd like to get a class-wide list.

Minute Cards
~~~~~~~~~~~~

In the last 5 minutes of class, please fill out this `minute card survey <https://docs.google.com/spreadsheet/viewform?formkey=dHFMMmg5djBFMTFQV2paSlNtWG94X0E6MQ#gid=0>`__.

Day 6 -- Th, Jan 24, 2013
=========================

Rough schedule for today, summary:
 - testing, code paths, and branching paths
 - in class exercise on testing
 - git: resolving conflicts
 - in class exercise on resolving conflicts
 - minute cards (3:50)

Join the online chat for Q&A at: https://www.hipchat.com/gpAMmlQ4v

Testing and code paths
----------------------

Suppose I give you a function::

   def fut(a, b):
      "Return 0 if a and b are equal, 1 if a is bigger, and -1 if b is bigger."
      if a == b:
         return 0
      elif a > b:
         return 1
      else:
         return -1

How many different combinations of a and b should you pass into make
sure that every line of code in this function is tested?

Here's another::

   def corrected_fraction(a, b):
      "returns a/(b - 1) if b > 0, a/b otherwise."
      a = float(a)
      b = float(b)

      if b > 0:
         b -= 1
 
      return a/b

Here's a third::

   def slow_mod(a, b):
      "returns a mod b"
      while a > b:
         a -= b

      return a

What conditions should you feed into these functions in order to test
them thoroughly?  (Ignore out of bounds errors, please, like 'this
number is too big', etc.)

Answer `here <https://docs.google.com/spreadsheet/viewform?formkey=dFVJQ2pONndFOThoSWR1OW5QaGltSUE6MQ>`__, please.

git: Resolving conflicts during merge
-------------------------------------

The main thing I need to show you all before we move forward with
all the exciting features that git has to offer is the question of
how to resolve conflicts.

One of the primary purposes of version control is *collaboration* --
it's supposed to help multiple people work on the same project without
colliding.  This is easy (at a technical level) when the people are
working on different files or different lines of different files. But
what about when their changes collide, e.g. Emily makes a change to
the same line as Beth?

In that case, git forces you to *manually* resolve things.

Let's take a look at the cse491-ex-rezolve repository on github:

   https://github.com/ctb/cse491-ex-rezolve

This contains a bunch of text quotes that have been edited by a mad
professor and need to be fixed.  Specifically, the mad professor made
everything lowercase and replaced all of the 'e's with 'z's.  Your job
will be to fix one of these problems (say, lowercase), for one of the
quotes files, and then merge your fixes with someone else's fixes for
the OTHER problem (say, e->z).

Let's take a look at example-quote.txt::

   no synonym for god is so pzrfzct as bzauty. whzthzr as szzn carving thz linzs
   of thz mountains with glacizrs, or gathzring mattzr into stars, or planning thz
   movzmznts of watzr, or gardzning - still all is bzauty!
   
   ...
   THIS IS A BIG BLOCK OF STUFF THAT DOESN'T CHANGE
   ...
   
   zvzry crzator painfully zxpzriznczs thz chasm bztwzzn his innzr vision and its ultimatz zxprzssion.

Suppose someone comes in and fixes all of the e->z problems, and
pushes them to their repository on github (see, for example, this file
on the ze_fix branch:
https://github.com/ctb/cse491-ex-rezolve/blob/ze_fix/example-quote.txt).
And you come along and fix all of the capitalization problems, and
push them to a *different* repository on github (see this file on the
cap_fix branch:
https://github.com/ctb/cse491-ex-rezolve/blob/cap_fix/example-quote.txt).
There's no way for the computer to know how to merge these branches....
But you want to merge them!

First, what are the mechanics of merging?

Start by forking a copy of my repository,

   https://github.com/ctb/cse491-ex-rezolve.git

and then cloning it::

   git clone https://github.com/USERNAME/cse491-ex-rezolve.git

If you look at example-quote.txt, you'll see the completely unfixed
version.  Let's pull in the fixes from both branches in my repository::

   cd cse491-ex-rezolve
   git fetch https://github.com/ctb/cse491-ex-rezolve.git cap_fix:cap_fix
   git fetch https://github.com/ctb/cse491-ex-rezolve.git ze_fix:ze_fix

Check out the differences between them and the 'master' branch, which
is the default one when you clone a repository::

   git diff cap_fix

and

   git diff ze_fix

(The '+' at the beginning of the line means this line has been changed.)

Now let's try merging in the ze_fix::

   git merge ze_fix

You should see something like this::

   Updating 30d05e4..153c8d9
   Fast-forward
    example-quote.txt |    8 ++++----
    1 files changed, 4 insertions(+), 4 deletions(-)

and you'll see that all the 'z's in example-quote.txt have been fixed.
Wait -- how did it merge this without asking us anything!?

Well, git knows that the z->e changes are safe to apply to the master
branch, because it kept track of me making those changes ;).  (Edit,
commit, basically.)  git *also* knows that it's safe to apply the
capitalization fixes directly to master, too.  What git does *not*
know is how to *combine* the two.

So... now what?

Try merging in the cap_fix branch also::

   setenv EDITOR nano
   git merge cap_fix

Uh-oh! ::

   Auto-merging example-quote.txt
   CONFLICT (content): Merge conflict in example-quote.txt
   Automatic merge failed; fix conflicts and then commit the result.

'git status' will tell you that the problem is 'example-quote.txt'.  What
does this file look like?

You should see blocks like this::

   <<<<<<< HEAD
   no synonym for god is so perfect as beauty. whether as seen carving the lines
   of the mountains with glaciers, or gathering matter into stars, or planning the
   movements of water, or gardening - still all is beauty!
   =======
   No synonym for god is so pzrfzct as bzauty. Whzthzr as szzn carving thz linzs
   of thz mountains with glacizrs, or gathzring mattzr into stars, or planning thz
   movzmznts of watzr, or gardzning - still all is bzauty!
   >>>>>>> cap_fix

This is git's way of saying, "everything between <<<< and === is from
the current branch, everything from === to >>> is from the branch
you're telling me to merge, and I can't resolve it.  HELP."

To fix this, just merge them manually; make it look like::

   No synonym for god is so perfect as beauty. Whether as seen carving the lines
   of the mountains with glaciers, or gathering matter into stars, or planning the
   movements of water, or gardening - still all is beauty!

and delete all the >>> === and <<< stuff.  Then save, and at the command line
say::

   git add example-quote.txt
   git commit -am "merged ze fix and cap fix"

The first line is an explicit direction to git that you fixed the
merge problems in that file; the second line tells git that you're all
done.

Sharing branches with others
----------------------------

So, let's say I tell you to EITHER fix the capitals OR the 'z's in one
of the quotes files, and that I want you to share these changes via
github.  How do you do this?

First, make the changes.

Then, commit them with 'git commit -am "commit message"'.

Then *push* them to your github repo::

   git push origin master:remote_branch_name

You can now *fetch* other people's branches like so::

   git fetch <their github URL> remote_branch_name:local_branch_name

and use 'git merge' as above.

So I would like you to fix one or the other of the capitals and the
z/es in one of the quotes (as per handed-out directions), push them to
github as either 'ze_fix' or 'cap_fix' branches (see:
remote_branch_name, above), go find a compadre who has worked on the
*opposite* problem, and then merge their changes (and have them merge
your changes), and then push the merge to your master branch.

Minute Cards
~~~~~~~~~~~~

In the last 5 minutes of class, please fill out this `minute card survey <https://docs.google.com/spreadsheet/viewform?formkey=dHFMMmg5djBFMTFQV2paSlNtWG94X0E6MQ#gid=0>`__.

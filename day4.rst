Day 4 -- Th, Jan 17, 2013
=========================

Rough schedule for today, summary:
 - fill in office hours doodle
 - look at source code for exercise #2 from Tuesday
 - answer quizlet questions (2:50)
 - discuss more broadly
 - do exercise #3, below (debugging, git add, git push) (3:15)
 - discussion (3:45)
 - minute cards (3:55)

Join the online chat for Q&A at: https://www.hipchat.com/gpAMmlQ4v

Office hours
------------

Please go here:

   http://whenisgood.net/82igkrb

and fill in your availability/interest for office/TA hours.

Today!
------

Look at the source code for exercise #2 from :doc:`day3`, and prepare
to answer some questions about it.

.. `Quizlet <https://docs.google.com/spreadsheet/viewform?formkey=dEhQTjVKbm9OSXdBaElCazNocnkzREE6MQ>`__

Iterators
~~~~~~~~~

The example in series_iter.py has the following code::

   for i in series.adder():
      ...

This code expands to the following set of calls::

   x = series.adder()
   y = iter(x)
   while 1:
      i = y.next()
      ...

Which expands or simplifies to this::

   x = series.adder()
   y = x.__iter()__
   while 1:
      i = y.next()

which in turn simplifies to::

   x = series.adder()
   while 1:
      y = x.next()

You can read up online about other ways that iterators can be
manipulated, stopped, understood, etc; see, for example,
`StackOverflow
<http://stackoverflow.com/questions/19151/build-a-basic-python-iterator>`__
or `the Python docs themselves
<http://docs.python.org/2/library/stdtypes.html>`__.

Exercise #3
~~~~~~~~~~~

In your 'cse491-numberz' directory (the one you cloned from my github
URL, that contains all the source?) execute::

   git pull origin master

This will retrieve updates and new files.  You should now have a directory
'iter_bug'.

Try running it::

   cd iter_bug
   python2.7 test.py

Make 'iter_bug/test.py' work by editing both test.py and fib.py.  Bear
in mind that by "work" I mean that 'fib.fib()' should produce an
accurate and correct Fibonacci series, and all of the code in test.py
should run properly when 'test.py' is executed from the command line.

Once you have everything working, commit the changes::
 
   git commit -am "fixed the bug"

Next, push them to github.com.  Specifically, go to github.com, log
in, and go to

   https://github.com/ctb/cse491-numberz

Click the 'fork' button to fork this project into your own github
account.  Then, select the 'https' URL from the middle of the page of
your own copy of the cse491-numberz project -- it should look something
like this::

   https://github.com/YOUR_USERNAME/cse491-numberz.git

and, in your *local* copy of the repository, do::

   git remote rm origin
   git remote add origin https://github.com/YOUR_USERNAME/cse491-numberz.git
   git remote add ctb https://github.com/ctb/cse491-numberz.git

And, finally, do::

   git push origin master

You should now see the bugfix changes to your LOCAL files (on CSE or
wherever) up on the github Web site under your account.

...and this is how you will hand in homework :).

.. Minute Cards
.. ~~~~~~~~~~~~

.. In the last 5 minutes of class, please fill out this `minute card survey <>`__.

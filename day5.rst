Day 5 -- Tu, Jan 22, 2013
=========================

Rough schedule for today, summary:
 - announcement: syllabus updated; office hours Tuesday, 6-8pm, 2228 BPS
 - in-class project
 - minute cards (3:45)
 - pre-survey

Join the online chat for Q&A at: https://www.hipchat.com/gpAMmlQ4v

In-class Project: drinkz testing
--------------------------------

On the CSE cluster, do the following::

   cd
   python2.7 -m virtualenv env491
   source env491/bin/activate.csh
   easy_install nose

This creates a 'virtual' installation of Python 2.7 in the directory
'env491' that is under your own control -- see
http://pypi.python.org/pypi/virtualenv -- and then activates it so
that it is the first Python install in your PATH.  Then 'easy_install
nose' installs the `nose testing framework
<https://nose.readthedocs.org/en/latest/>`__ under that environment.

If you're running this on your own computer, you can skip the virtualenv
and activate steps, and just 'easy_install nose' as superuser.  Or you
can install virtualenv as superuser, and following everything as normal.

Next, go to https://github.com/ctb/cse491-drinkz and fork this repository
into your own github account.  On the CSE cluster, do ::

   git clone https://github.com/FAKEUSERNAME/cse491-drinkz.git

but replace 'FAKEUSERNAME' with your own github username.  If you do::

   cd cse491-drinkz
   ls -R

you should see the following files::

   .:
   README.md  drinkz

   ./drinkz:
   __init__.py  db.py  load_bulk_data.py  test_drinkz.py

Use 'less' to read the README, and ::

   nosetests -v

to run the tests.

**Your mission: fix the tests by implementing the various functions,
then commit your changes and push to your github repo.**

Once you have fixed all the tests, to commit and push do::

   git commit -am "fixed tests"
   git push origin master

Note that you can fix one test at a time (and then commit and push),
and share work, and thereby work in parallel on different tests and
functions; if you want to do this talk to me and I'll show you how to
pull from other people's repositories and merge.  We'll be discussing
this on Thursday anyway, however.

Pre Survey
~~~~~~~~~~~~
If you finish the in-class project, please take this `pre-survey <https://docs.google.com/spreadsheet/viewform?formkey=dEg0LUVQMV82QjV2WGJfRzhHb2xBbHc6MQ#gid=0>`__ about your experience with topics we will be studying in the course.

Minute Cards
~~~~~~~~~~~~

In the last 5 minutes of class, please fill out this `minute card survey <https://docs.google.com/spreadsheet/viewform?formkey=dHFMMmg5djBFMTFQV2paSlNtWG94X0E6MQ#gid=0>`__.

**git**
-------

Exercises
=========

Exercise 1:
~~~~~~~~~~~

Which command(s) below would save the changes of ``myfile.txt`` to my local Git repository?

.. code-block ::bash

	$ git commit -m "my recent changes"
	$ git init myfile.txt $ git commit -m "my recent changes"
	$ git add myfile.txt $ git commit -m "my recent changes"
	$ git commit -m  "my recent changes"  myfile.txt

Exercise 2:
~~~~~~~~~~~

The staging area can hold changes from any number of files that you want to commit as a single snapshot.
Add some text to ``mars.txt`` noting your decision to consider Venus as a base
Create a new file ``venus.txt`` with your initial thoughts about Venus as a base for you and your friends
Add changes from both files to the staging area, and commit those changes.

Exercise 3:
~~~~~~~~~~~

- Add some useful info to the `README.md` file for the planets repo.
- Commit the changes
- Push the changes to GitHub

Exercise 4:
~~~~~~~~~~~

- Create a new Git repository on GitHub called ``bio``.
- Clone the repository to your computer.
- Write a three-line biography for yourself in a file called `me.txt`, commit your changes
- Modify one line, add a fourth line, commit your changes
- Push the changes to GitHub

Exercise 5:
~~~~~~~~~~~

How would you ignore all ``.data`` files in your root directory except for ``final.data``? Hint: Find out what ``!`` (the exclamation point operator) does

Exercise 6:
~~~~~~~~~~~

Given a ``.gitignore`` file with the following contents:

.. code-block:: bash

	*.data
	!*.data

What will be the result?

Exercise 7:
~~~~~~~~~~~

Jennifer has made changes to the Python script that she has been working on for weeks, and the modifications she made this morning “broke” the script and it no longer runs. She has spent ~ 1hr trying to fix it, with no luck. Luckily, she has been keeping track of her project’s versions using Git! Which commands below will let her recover the last committed version of her Python script called `data_cruncher.py`?

.. code-block:: bash

	$ git checkout HEAD
	$ git checkout HEAD data_cruncher.py
	$ git checkout HEAD~1 data_cruncher.py
	$ git checkout <unique ID of last commit> data_cruncher.py
	Both 2 and 4

Capstone project:
~~~~~~~~~~~~~~~~~

- Create new repository
- Write shell script to [practice something from shell]
- Commit script and push to GitHub
- Write shell script to [practice something else from shell]
- Commit script and push to GitHub
- Clone your neighbor's repo from GitHub and look at their scripts
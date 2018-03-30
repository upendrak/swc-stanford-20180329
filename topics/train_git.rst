**Training session in Git**
---------------------------

In this session we will show you how to version control using git. 

Resources for the Git portion of the 2018-03-29-stanford Software Carpentry workshop.

Topics
======

The links below lead to the Software Carpentry lessons that our class was based on. Note that we didn't follow the lessons exactly.

1. Introduction to Git and GitHub
2. `Setting Up Git <https://swcarpentry.github.io/git-novice/02-setup/>`_
3. Creating a repository (we will create repositories using GitHub, but `these instructions <https://swcarpentry.github.io/git-novice/03-create/>`_ detail an alternative way to create a repo from the command line)
4. `Tracking Changes <https://swcarpentry.github.io/git-novice/04-changes/>`_
5. `Ignoring Things <https://swcarpentry.github.io/git-novice/06-ignore/>`_
6. `Exploring History <https://swcarpentry.github.io/git-novice/05-history/>`_
7. Capstone Project

Exercises
=========

Exercise 1: 
Which command(s) below would save the changes of myfile.txt to my local Git repository?

* `$ git commit -m "my recent changes"`
* `$ git init myfile.txt $ git commit -m "my recent changes"`
* `$ git add myfile.txt $ git commit -m "my recent changes"`
* `$ git commit -m  "my recent changes"  myfile.txt`

Exercise 2:
The staging area can hold changes from any number of files that you want to commit as a single snapshot.

* Add some text to mars.txt noting your decision to consider Mars as a base
* Create a new file venus.txt with your initial thoughts about Venus as a base for you and your friends
* Add changes from both files to the staging area, and commit those changes.

Exercise 3:

* Add some useful info to the README.md file for the planets repo.
* Commit the changes
* Push the changes to GitHub

Exercise 4:

* Create a new Git repository on GitHub called bio.
* Clone the repository to your computer.
* Write a three-line biography for yourself in a file called me.txt, commit your changes
* Modify one line, add a fourth line
* Push the changes to GitHub

Exercise 5:
How would you ignore all .data files in your root directory except for final.data? Hint: Find out what ! (the exclamation point operator) does

Exercise 6:
Given a .gitignore file with the following contents:
```
*.data
!*.data
```
What will be the result?

Exercise 7:
Jennifer has made changes to the Python script that she has been working on for weeks, and the modifications she made this morning “broke” the script and it no longer runs. She has spent ~ 1hr trying to fix it, with no luck. Luckily, she has been keeping track of her project’s versions using Git! Which commands below will let her recover the last committed version of her Python script called data_cruncher.py?

* `$ git checkout HEAD`
* `$ git checkout HEAD data_cruncher.py`
* `$ git checkout HEAD~1 data_cruncher.py`
* `$ git checkout <unique ID of last commit> data_cruncher.py`
Both 2 and 4

Capstone project:

* Create new repository on GitHub called amino-acid-analysis
* Write shell script to that prints out every amino acid that begins with an "A" using the "amino-acids.txt" file from the filesystem repo we used yesterday (https://github.com/eharstad/filesystem.git)
* Commit script and push to GitHub
* Modify your shell script to also print the number of amino acids that begin with "A"
* Commit script and push to GitHub
* Clone your neighbor's repo from GitHub and look at their scripts. Do their scripts differ from yours?

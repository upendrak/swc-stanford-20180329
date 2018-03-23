**Unix Shell**
--------------

1. What is Unix and Shell?
==========================

``Unix`` or ``Linux`` is our operating system – the program that controls the processes and their access to the network, screen, etc.

The ``shell`` is a process – it happens to be one that can see its own OS, which is one of the reasons it’s so useful.

The ``Unix shell`` has been around longer than most of its users have been alive. It has survived so long because it's a power tool that allows people to do complex things with just a few keystrokes. More importantly, it helps them combine existing programs in new ways and automate repetitive tasks so that they don't have to type the same things over and over again

The part of the operating system responsible for managing files and directories is called the file system. It organizes our data into files, which hold information, and directories (also called "folders"), which hold files or other directories.

2. Files and Directories
========================

Several commands are frequently used to create, inspect, rename, and delete files and directories. To start exploring them, let's open a shell window:

.. code-block :: bash

	$

The dollar sign is a prompt, which shows us that the shell is waiting for input; your shell may show something more elaborate.

Type the command ``whoami``, then press the Enter key (sometimes marked Return) to send the command to the shell. The command's output is the ID of the current user, i.e., it shows us who the shell thinks we are:

.. code-block :: bash

	$ whoami
	upendra_35

More specifically, when we type ``whoami`` in the shell. It does the following:

- finds a program called ``whoami``,
- runs that program,
- displays that program's output, then
- displays a new prompt to tell us that it's ready for more commands.

Next, let's find out where we are by running a command called ``pwd`` (which stands for "print working directory"). At any moment, our current working directory is our current default directory, i.e., the directory that the computer assumes we want to run commands in unless we explicitly specify something else. 

.. code-block :: bash

	$ pwd
	/Users/upendra_35

Here, the computer's response is ``/Users/upendra_35``, which is my "home directory"

To understand what a "home directory" is, let's have a look at how the file system as a whole is organized. At the top is the ``root`` directory that holds everything else. We refer to it using a slash character ``/`` on its own;

Inside that directory are several other directories: ``bin`` (which is where some built-in programs are stored), ``data`` (for miscellaneous data files), ``Users`` (where users' personal directories are located), ``tmp`` (for temporary files that don't need to be stored long-term), and so on:

|file_system|

2.1 The Filesystem
~~~~~~~~~~~~~~~~~~

We know that our current working directory ``/Users/upendra_35`` is stored inside ``/Users`` because ``/Users`` is the first part of its name. Similarly, we know that ``/Users`` is stored inside the root directory ``/`` because its name begins with ``/``.

.. Note ::

	There are two meanings for the ``/`` character. When it appears at the front of a file or directory name, it refers to the root directory. When it appears inside a name, it's just a separator.

Let's see what's in my home directory by running ``ls``, which stands for "listing":

.. code-block :: bash

	$ ls
	Applications	Documents	Dropbox		Movies		Pictures	PycharmProjects		git-prompt.sh		misc
	Desktop			Downloads	Library		Music		Public		data				miniconda3

Let's download a ``data`` directory and start using unix commands on it. Go ahead and run the below command on your home diretory. Don't worry about the sytax now as we will see that later in the session.

.. code-block :: bash

	$ wget -O- https://de.cyverse.org/dl/d/C84B7CF3-341B-461C-9069-4491C7E28487/data.tar.gz | tar xvz

``ls`` prints the names of the files and directories in the current directory in alphabetical order, arranged neatly into columns. We can make its output more comprehensible by using the flag ``-F``, which tells ls to add a trailing ``/`` to the names of directories:

.. code-block :: bash

	$ ls -F
	Applications/	Documents/		Dropbox/		Movies/			Pictures/		PycharmProjects/	git-prompt.sh		misc/
	Desktop/		Downloads/		Library/		Music/			Public/			data/				miniconda3/

Now let's take a look at what's in ``data`` directory by running ``ls -F data``, i.e., the command ``ls`` with the arguments ``-F`` and ``data``. The second argument --- the one without a leading dash --- tells ls that we want a listing of something other than our current working directory:

.. code-block :: bash

	$ ls -F data/
	amino-acids.txt		elements/		molecules/			planets.csv		sunspot.txt

The output shows us that there are four text files and two sub-sub-directories. Organizing things hierarchically in this way helps us keep track of our work: it's possible to put hundreds of files in our home directory, just as it's possible to pile hundreds of printed papers on our desk, but it's a self-defeating strategy.

.. Note ::

	We spelled the directory name ``data``. It doesn't have a trailing slash: that's added to directory names by ``ls`` when we use the ``-F`` flag to help us tell things apart. And it doesn't begin with a slash because it's a **relative path**, i.e., it tells ls how to find something from where we are, rather than from the root of the file system.

.. important ::

	Parameters vs. Arguments
	According to Wikipedia, the terms argument and parameter mean slightly different things. In practice, however, most people use them interchangeably or inconsistently, so we will too.

If we run ``ls -F /data`` (with a leading slash) we get a different answer, because ``/data`` is an absolute path:

.. code-block :: bash

	$ ls -F /data
	access.log	backup/		hardware.cfg	network.cfg

The leading ``/`` tells the computer to follow the path from the root of the filesystem, so it always refers to exactly one directory, no matter where we are when we run the command.

What if we want to change our current working directory? Before we do this, ``pwd`` shows us that we're in ``/Users/upendra_35``, and ``ls`` without any arguments shows us that directory's contents.

We can use ``cd`` followed by a directory name to change our working directory. ``cd`` stands for "change directory", which is a bit misleading: the command doesn't change the directory, it changes the shell's idea of what directory we are in.

.. code-block :: bash

	$ cd data

``cd`` doesn't print anything, but if we run ``pwd`` after it, we can see that we are now in ``/Users/upendra_35/data``. If we run ``ls`` without arguments now, it lists the contents of ``/Users/upendra_35/data``, because that's where we now are:

.. code-block :: bash

	$ pwd
	/Users/upendra_35/data

.. code-block :: bash

	$ ls -F
	amino-acids.txt		elements/		molecules/			planets.txt		sunspot.txt

We now know how to go down the directory tree: how do we go up? We could use two ways..

We could use an absolute path:

.. code-block :: bash

	$ cd /Users/upendra_35/

or a relative path:

.. code-block :: bash

	$ cd ..

``..`` is a special directory name meaning "the directory containing this one", or more succinctly, the parent of the current directory. Sure enough, if we run pwd after running ``cd ..``, we're back in /Users/upendra_35:

.. code-block :: bash

	$ pwd
	/Users/upendra_35

The special directory ``..`` doesn't usually show up when we run ``ls``. If we want to display it, we can give ls the ``-a`` flag:

``-a`` stands for "show all"; it forces ls to show us file and directory names that begin with `.`, such as ``..`` (which, if we're in ``/Users/upendra_35``, refers to the ``/Users`` directory). As you can see, it also displays another special directory that's just called ``.``, which means "the current working directory". It may seem redundant to have a name for it, but we'll see some uses for it soon.

- **Exercises**

|file_system2|

1. If ``pwd`` displays ``/users/thing``, what will ``ls ../backup`` display?

a. 	``../backup: No such file or directory``
b. ``2012-12-01 2013-01-08 2013-01-27``
c. ``2012-12-01/ 2013-01-08/ 2013-01-27/``
d. ``original pnas_final pnas_sub``


2. If ``pwd`` displays ``/users/backup``, and ``-r`` tells ls to display things in reverse order, what command will display:

.. code-block :: bash

	pnas-sub/ pnas-final/ original/

a. ``ls pwd``
b. ``ls -r -F``
c. ``ls -r -F /users/backup``
d. Either #2 or #3 above, but not #1

3. What does the command ``cd`` without a directory name do?

a. It has no effect.
b. It changes the working directory to /.
c. It changes the working directory to the user's home directory.
d. It produces an error message.

3. Creating files and folders
=============================

We now know how to explore files and directories, but how do we create them in the first place? 

Let's create a new directory called ``thesis`` using the command ``mkdir thesis`` (which has no output):

.. warning :: 

	Make sure you create this directory in your home directory which in my case is ``/Users/upendra_35``

.. code-block :: bash

	$ mkdir thesis

As you might (or might not) guess from its name, ``mkdir`` means "make directory". Since thesis is a relative path (i.e., doesn't have a leading slash), the new directory is created in the current working directory:

.. code-block :: bash

	$ ls -F
	Applications/		Documents/		Dropbox/		Movies/			Pictures/		PycharmProjects/	git-prompt.sh		misc/
	Desktop/			Downloads/		Library/		Music/			Public/			data/				miniconda3/			thesis/

However, there's nothing in it yet:

.. code-block :: bash

	$ ls -F thesis

There are several ways to create a file but one of the simplest ways to create an empty file is via the ``touch`` command. Change the working directory to ``thesis`` using ``cd``, then touch an empty file called ``draft.txt``:

.. code-block :: bash

	$ cd thesis
	$ touch draft.txt

If we check the directory contents now,

.. code-block :: bash

	$ ls 
	draft.txt

Another way to create a file is to run a text editor called Nano to create a file called ``draft.txt``:

.. code-block :: bash

	$ nano draft.txt

.. Tip ::

	Which Editor?
	When we say, "nano is a text editor," we really do mean "text": it can only work with plain character data, not tables, images, or any other human-friendly media. We use it in examples because almost anyone can drive it anywhere without training, but please use something more powerful for real work. On Unix systems (such as Linux and Mac OS X), many programmers use Emacs or Vim (both of which are completely unintuitive, even by Unix standards), or a graphical editor such as Gedit. On Windows, you may wish to use Notepad++.

	No matter what editor you use, you will need to know where it searches for and saves files. If you start it from the shell, it will (probably) use your current working directory as its default location. If you use your computer's start menu, it may want to save files in your desktop or documents directory instead. You can change this by navigating to another directory the first time you "Save As..."

Let's type in a few lines of text, then use Control-X to write our data to disk and exit it:

|nano_1|

nano doesn't leave any output on the screen after it exits, but ``ls`` now shows that we have created a file called ``draft.txt``:

.. code-block :: bash

	$ ls 
	draft.txt

Let's tidy up by running rm draft.txt:

.. code-block :: bash

	$ rm draft.txt

This command removes files ("rm" is short for "remove"). If we run ``ls`` again, its output is empty once more, which tells us that our file is gone:

.. warning ::

	**Deleting Is Forever**. The Unix shell doesn't have a trash bin that we can recover deleted files from (though most graphical interfaces to Unix do). Instead, when we delete files, they are unhooked from the file system so that their storage space on disk can be recycled. Tools for finding and recovering deleted files do exist, but there's no guarantee they'll work in any particular situation, since the computer may recycle the file's disk space right away.

So in order to avoid this situation make sure you ask Unix to prompt for you. For example

.. code-block :: bash

	$ rm -i draft.txt
	remove draft.txt? 

Now you can enter either ``y`` or ``n``

What if we want to remove the entire ``thesis`` directory?

If we try to remove the entire thesis directory using ``rm thesis``, we get an error message:

.. code-block :: bash

	$ cd ..
	$ rm thesis
	rm: thesis: is a directory

This happens because rm only works on files, not directories. The right command is ``rmdir``, which is short for "remove directory". It doesn't work yet either, though, because the directory we're trying to remove isn't empty:

.. code-block :: bash
	
	$ rmdir thesis
	rmdir: thesis: Directory not empty

This little safety feature can save you a lot of grief, particularly if you are a bad typist. To really get rid of thesis we must first delete the file draft.txt:

.. code-block :: bash

	$ rm thesis/draft.txt

The directory is now empty, so rmdir can delete it:

.. code-block :: bash

	$ rmdir thesis

However this is tedious. Imagine you have several files in that directories. Instead we can use ``rm`` with the ``-r`` flag (which stands for "recursive")

.. code-block :: bash

	$ rm -r thesis

.. warning ::

	This removes everything in the directory, then the directory itself. If the directory contains sub-directories, rm -r does the same thing to them, and so on. It's very handy, but can do a lot of damage if used without care.

Let's create that directory and file one more time. 

.. Note :: 

	This time we're running nano with the path ``thesis/draft.txt``, rather than going into the thesis directory and running nano on draft.txt there.

.. code-block :: bash

	$ mkdir thesis
	$ nano thesis/draft.txt
	$ ls thesis
	draft.txt

``draft.txt`` isn't a particularly informative name, so let's change the file's name using ``mv``, which is short for "move":

.. code-block :: bash
	
	$ mv thesis/draft.txt thesis/quotes.txt

The first parameter tells mv what we're "moving", while the second is where it's to go. In this case, we're moving ``thesis/draft.txt`` to ``thesis/quotes.txt``, which has the same effect as renaming the file. Sure enough, ls shows us that thesis now contains one file called ``quotes.txt``

Just for the sake of inconsistency, mv also works on directories --- there is no separate mvdir command.

.. code-block :: bash

	$ mv thesis/quotes.txt .

The ``cp`` command works very much like mv, except it copies a file instead of moving it.

.. code-block :: bash

	$ cp quotes.txt thesis/quotations.txt

- Exercise

1. Suppose that you created a .txt file in your current directory to contain a list of the statistical tests you will need to do to analyze your data, and named it: statstics.txt

After creating and saving this file you realize you misspelled the filename! You want to correct the mistake, which of the following commands could you use to do so?

1. ``cp statstics.txt statistics.txt``
2. ``mv statstics.txt statistics.txt``
3. ``mv statstics.txt .``
4. ``cp statstics.txt .``

2. What is the output of the closing ls command in the sequence shown below?

.. code-block :: bash

	$ pwd
	/home/jamie/data
	$ ls
	proteins.dat
	$ mkdir recombine
	$ mv proteins.dat recombine
	$ cp recombine/proteins.dat ../proteins-saved.dat
	$ ls

1. ``proteins-saved.dat recombine``
2. ``recombine``
3. ``proteins.dat recombine``
4. ``proteins-saved.dat``

4. Pipes and Filters
====================

Now that we know a few basic commands, we can finally look at the shell's most powerful feature: the ease with which it lets us combine existing programs in new ways. We'll start with a directory called ``molecules`` that contains six files describing some simple organic molecules. The ``.pdb`` extension indicates that these files are in Protein Data Bank format, a simple text format that specifies the type and position of each atom in the molecule.

.. code-block :: bash

	$ ls molecules
	cubane.pdb	ethane.pdb	methane.pdb	octane.pdb	pentane.pdb	propane.pdb

Let's ``cd`` into that directory and run the command ``wc *.pdb``. ``wc`` is the "word count" command: it counts the number of lines, words, and characters in files. The ``*`` in ``*.pdb`` matches zero or more characters, so the shell turns ``*.pdb`` into a complete list of .pdb files:

.. code-block :: bash

	$ wc *.pdb
      20     156    1158 cubane.pdb
      12      84     622 ethane.pdb
       9      57     422 methane.pdb
      30     246    1828 octane.pdb
      21     165    1226 pentane.pdb
      15     111     825 propane.pdb
     107     819    6081 total

.. important ::

	Wildcards:

	``*`` is a wildcard. It matches zero or more characters, so ``*.pdb`` matches ethane.pdb, propane.pdb, and so on. On the other hand, ``p*.pdb`` only matches pentane.pdb and ``propane.pdb``, because the 'p' at the front only matches itself.

	``?`` is also a wildcard, but it only matches a single character. This means that ``p?.pdb`` matches ``pi.pdb`` or ``p5.pdb``, but not ``propane.pdb``. We can use any number of wildcards at a time: for example, ``p*.p?*`` matches anything that starts with a 'p' and ends with '.', 'p', and at least one more character (since the '?' has to match one character, and the final '*' can match any number of characters). Thus, p*.p?* would match preferred.practice, and even p.pi (since the first '*' can match no characters at all), but not quality.practice (doesn't start with 'p') or preferred.p (there isn't at least one character after the '.p').

	When the shell sees a wildcard, it expands the wildcard to create a list of matching filenames before running the command that was asked for. As an exception, if a wildcard expression does not match any file, Bash will pass the expression as a parameter to the command as it is. For example typing ls *.pdf in the molecules directory (which contains only files with names ending with .pdb) results in an error message that there is no file called *.pdf. However, generally commands like wc and ls see the lists of file names matching these expressions, but not the wildcards themselves. It is the shell, not the other programs, that deals with expanding wildcards, and this another example of orthogonal design.

If we run wc -l instead of just wc, the output shows only the number of lines per file:

.. code-block :: bash

	$ wc -l *.pdb
      20 cubane.pdb
      12 ethane.pdb
       9 methane.pdb
      30 octane.pdb
      21 pentane.pdb
      15 propane.pdb
     107 total

Similarly we can also use ``-w`` to get only the number of words, or ``-c`` to get only the number of characters.

Which of these files is shortest? It's an easy question to answer when there are only six files, but what if there were 6000? Our first step toward a solution is to run the command:

.. code-block :: bash

	$ wc -l *.pdb > lengths.txt

The greater than symbol, ``>``, tells the shell to redirect the command's output to a file instead of printing it to the screen. The shell will create the file if it doesn't exist, or overwrite the contents of that file if it does. (This is why there is no screen output: everything that wc would have printed has gone into the file ``lengths.txt`` instead.)

We can now send the content of lengths.txt to the screen using cat lengths.txt. cat stands for "concatenate": it prints the contents of files one after another. There's only one file in this case, so ``cat`` just shows us what it contains:

.. code-block :: bash

	$ cat lengths.txt
	20  cubane.pdb
	12  ethane.pdb
	9  methane.pdb
	30  octane.pdb
	21  pentane.pdb
	15  propane.pdb
	107  total

Now let's use the ``sort`` command to sort its contents. We will also use the ``-n`` flag to specify that the sort is numerical instead of alphabetical. This does not change the file; instead, it sends the sorted result to the screen:

.. code-block :: bash

	$ sort -n lengths.txt
	9  methane.pdb
	12  ethane.pdb
	15  propane.pdb
	20  cubane.pdb
	21  pentane.pdb
	30  octane.pdb
	107  total

Now if you run ``$ sort -n lengths.txt | head -1`` it will tell you the first line of the file. Using the parameter ``-1`` with ``head`` tells it that we only want the first line of the file. The vertical bar between the two commands is called a pipe. It tells the shell that we want to use the output of the command on the left as the input to the command on the right. The computer might create a temporary file if it needs to, or copy data from one program to the other in memory, or something else entirely; we don't have to know or care.

.. code-block :: bash

	$ sort -n lengths.txt | head -1
	9  methane.pdb

Instead of creating an intermediate file ``lengths.txt`` we can use another pipe to send the output of ``wc`` directly to ``sort``, which then sends its output to head:

.. code-block :: bash

	$ wc -l *.pdb | sort -n | head -1
	9  methane.pdb

- Exercises

1. What does ``sort -n`` do?

If we run sort on this file:

.. code-block :: bash

	10
	2
	19
	22
	6

the output is:

.. code-block :: bash

	10
	19
	2
	22
	6

If we run ``sort -n`` on the same input, we get this instead:

.. code-block :: bash

	2
	6
	10
	19
	22

2. Explain why -n has this effect.

In our current directory, we want to find the 3 files which have the least number of lines. Which command listed below would work?

1. ``wc -l * > sort -n > head -3``
2. ``wc -l * | sort -n | head 1-3``
3. ``wc -l * | head -3 | sort -n``
4. ``wc -l * | sort -n | head -3``

5. Finding things
=================

You can guess someone's age by how they talk about search: young people use "Google" as a verb, while crusty old Unix programmers use "grep". The word is a contraction of "global/regular expression/print", a common sequence of operations in early Unix text editors. It is also the name of a very useful command-line program.

``grep`` finds and prints lines in files that match a pattern. For our examples, we will use a file that contains three haikus taken from a 1998 competition in Salon magazine. For this set of examples we're going to be working in the writing subdirectory:

.. code-block :: bash

	$ cd
	$ cd writing
	$ cat haiku.txt
	The Tao that is seen
	Is not the true Tao, until
	You bring fresh toner.

	With searching comes loss
	and the presence of absence:
	"My Thesis" not found.

	Yesterday it worked
	Today it is not working
	Software is like that.

Let's find lines that contain the word "not":

.. code-block :: bash

	$ grep not haiku.txt
	Is not the true Tao, until
	"My Thesis" not found
	Today it is not working

Here, ``not`` is the pattern we're searching for. It's pretty simple: every alphanumeric character matches against itself. After the pattern comes the name or names of the files we're searching in. The output is the three lines in the file that contain the letters "not".

Let's try a different pattern: "day".

.. code-block :: bash

	$ grep day haiku.txt
	Yesterday it worked
	Today it is not working

This time, two lines that include the letters "day" are outputted. However, these letters are contained within larger words. To restrict matches to lines containing the word "day" on its own, we can give ``grep`` with the ``-w`` flag. This will limit matches to word boundaries.

.. code-block :: bash

	$ grep -w day haiku.txt

In this case, there aren't any, so grep's output is empty.

Another useful option is ``-n``, which numbers the lines that match:

.. code-block :: bash

	$ grep -n it haiku.txt
	5:With searching comes loss
	9:Yesterday it worked
	10:Today it is not working

Here, we can see that lines 5, 9, and 10 contain the letters "it".

We can combine flags as we do with other Unix commands. For example, since ``-i`` makes matching case-insensitive and ``-v`` inverts the match, using them both only prints lines that don't match the pattern in any mix of upper and lower case:

.. code-block :: bash

	$ grep -i -v the haiku.txt
	You bring fresh toner.

	With searching comes loss

	Yesterday it worked
	Today it is not working
	Software is like that.

``grep`` has lots of other options. To find out what they are, we can type ``man grep``. ``man`` is the Unix "manual" command: it prints a description of a command and its options, and (if you're lucky) provides a few examples of how to use it.

``grep's`` real power doesn't come from its options, though; it comes from the fact that patterns can include wildcards. (The technical name for these is regular expressions, which is what the "re" in "grep" stands for.) Regular expressions are both complex and powerful; if you want to do complex searches. For example, we can find lines that have an 'o' in the second position like this:

.. code-block :: bash

	$ grep '^.o' haiku.txt
	You bring fresh toner.
	Today it is not working
	Software is like that.

The ``^`` in the pattern anchors the match to the start of the line. The ``.`` matches a single character (just like ``?`` in the shell), while the ``o`` matches an actual ``o`` letter.

- Exercise

1. From the ``haiku.txt`` file, which command would result in the following output: ``and the presence of absence``

1. ``grep of haiku.txt``
2. ``grep -E of haiku.txt``
3. ``grep -w of haiku.txt``
4. ``grep -i of haiku.txt``

6. Transferring Files and Accessing Remote Server
=================================================

The ``wget`` utility is the best option to download files from the internet. It can pretty much handle all complex download situations including large file downloads, recursive downloads, non-interactive downloads, multiple file downloads etc. It retrieves files from World Wide Web (WWW) using widely used protocols like HTTP, HTTPS and FTP, and is designed in such way so that it works in slow or unstable network connections. Wget can automatically re-start a download where it was left off in case of network problem. Also downloads file recursively and will keep trying until file has be retrieved completely.

The command ``wget`` will download a single file and stores it in the current directory. It shows download progress, size, date and time while downloading.

We have seen one use of ``wget`` already. Let's take a look at another example

.. code-block :: bash

	$ wget http://hgdownload.soe.ucsc.edu/goldenPath/hg38/database/ccdsGene.txt.gz
	--2018-03-22 17:32:56--  http://wget/
	Resolving wget (wget)... failed: nodename nor servname provided, or not known.
	wget: unable to resolve host address ‘wget’
	--2018-03-22 17:32:56--  http://hgdownload.soe.ucsc.edu/goldenPath/hg38/database/ccdsGene.txt.gz
	Resolving hgdownload.soe.ucsc.edu (hgdownload.soe.ucsc.edu)... 128.114.119.163
	Connecting to hgdownload.soe.ucsc.edu (hgdownload.soe.ucsc.edu)|128.114.119.163|:80... connected.
	HTTP request sent, awaiting response... 200 OK
	Length: 2187289 (2.1M) [application/x-gzip]
	Saving to: ‘ccdsGene.txt.gz’

	ccdsGene.txt.gz                                      100%[======================================================================================================================>]   2.09M  4.00MB/s    in 0.5s    

	2018-03-22 17:32:57 (4.00 MB/s) - ‘ccdsGene.txt.gz’ saved [2187289/2187289]

	FINISHED --2018-03-22 17:32:57--
	Total wall clock time: 1.1s
	Downloaded: 1 files, 2.1M in 0.5s (4.00 MB/s)

The downloaded file is compressed to save space and contains the Consensus Coding DNA Sequence (CCDS) Genes for Human (GRCh38/hg38).

Unless you specify otherwise, the file created in your current directory will have the same name as the file you are downloading. Using ``-O`` (uppercase letter ``O``) option creates a file with a specified name. Here we have given mm10_geneid.txt.gz file name as show below.

.. code-block :: bash

	$ wget -O mm10_ccdsGene.txt.gz http://hgdownload.soe.ucsc.edu/goldenPath/mm10/database/ccdsGene.txt.gz

.. Tip ::

	It is possible to continue an incomplete download using wget -c. This is very helpful when you have initiated a very big file download which got interrupted in the middle. Instead of starting the whole download again, you can start the download from where it got interrupted using the option ``-c``.

Here is an example of downloading a file which got interrupted manually by using Ctrl-C command on the keyboard.

.. code-block :: bash

	$ wget http://hgdownload.soe.ucsc.edu/goldenPath/hg38/database/ccdsGene.txt.gz 
	--2018-03-22 17:50:06--  http://hgdownload.soe.ucsc.edu/goldenPath/hg38/database/ccdsGene.txt.gz
	Resolving hgdownload.soe.ucsc.edu (hgdownload.soe.ucsc.edu)... 128.114.119.163
	Connecting to hgdownload.soe.ucsc.edu (hgdownload.soe.ucsc.edu)|128.114.119.163|:80... connected.
	HTTP request sent, awaiting response... 200 OK
	Length: 2187289 (2.1M) [application/x-gzip]
	Saving to: ‘ccdsGene.txt.gz’

	ccdsGene.txt.gz                                       11%[============>                                                                                                          ] 238.74K  1.02MB/s               ^C

.. code-block :: bash

	$ wget -c http://hgdownload.soe.ucsc.edu/goldenPath/hg38/database/ccdsGene.txt.gz 
	--2018-03-22 17:50:20--  http://hgdownload.soe.ucsc.edu/goldenPath/hg38/database/ccdsGene.txt.gz
	Resolving hgdownload.soe.ucsc.edu (hgdownload.soe.ucsc.edu)... 128.114.119.163
	Connecting to hgdownload.soe.ucsc.edu (hgdownload.soe.ucsc.edu)|128.114.119.163|:80... connected.
	HTTP request sent, awaiting response... 206 Partial Content
	Length: 2187289 (2.1M), 1852513 (1.8M) remaining [application/x-gzip]
	Saving to: ‘ccdsGene.txt.gz’

	ccdsGene.txt.gz                                      100%[++++++++++++++++++====================================================================================================>]   2.09M  3.55MB/s    in 0.5s    

	2018-03-22 17:50:21 (3.55 MB/s) - ‘ccdsGene.txt.gz’ saved [2187289/2187289]

Here we see how to download multiple files using the FTP protocol and wget. It is the recommended method when downloading a large file or multiple files.

.. code-block :: bash

	$ wget ftp://hgdownload.soe.ucsc.edu/goldenPath/mm10/database/ccds*.txt.gz

6.1 Accessing Remote Server
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

``ssh`` (Secure Shell) is a network protocol that allows a secure access over an encrypted connection. Through an SSH connection you can easily manage your files and folders, modify their permissions, edit files directly on the server, configure and install your scripts, etc. ssh is used to securely login to a Linux / UNIX host running the sshd daemon on a reachable network.

We will be accessing a training server, which has some IP address, using the ``ssh`` command.

.. code-block :: bash

	$ ssh <username>@ipaddress


7. Loops
========


.. |file_system| image:: ../img/file_system.png
  :width: 550
  :height: 500

.. |file_system2| image:: ../img/file_system2.png
  :width: 550
  :height: 500

.. |nano_1| image:: ../img/nano_1.png
  :width: 550
  :height: 500  
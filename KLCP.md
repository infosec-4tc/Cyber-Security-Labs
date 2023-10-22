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

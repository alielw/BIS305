# BIS305

# Introduction to the HPC and NGS data

The aim of this practical is to get you started using the HPC 

## Useful links

UNIX tutorial: https://swcarpentry.github.io/shell-novice/

## 1. Logging in and getting started
We will be working on windows machines, which means that you need to use a program (ssh client) to access the cluster. We will be using MobXterm. Start by opening the program, if you have used it before to connect to Bessemer you may find "bessemer.sheff.ac.uk" under "User sessions", in which case you can just double click on this to launch an ssh session on bessemer. If not, click on "Session">"New session">"SSH" and enter
```
bessemer.shef.ac.uk
```
Specify your username (port should always be 22).

Access a worker node:
```bash
srun --pty bash -l
```
You should always start by doing this. No work should ever be done on the head node! If you are on a head node you will see someting like this in your command line prompt:
```
[bo1nn@bessemer-login1 ~]$
```
This node is just a gateway to the worker nodes. If you are on a worker node you will see the name of the node, eg.
```
[bo1nn@bessemer-node004 ~]$
```

## 2. Getting to grips with Linux and setting up your bash profile to access the software repository
First lets get used to finding your way around. So where are you now in the file system? 
```bash
pwd
```
Every Unix operating system has a root folder simply called ```/```. Let’s see what’s in it using the command to list information about files.
```bash
ls /
```
Try pressing the up arrow key. What does this do?

List the files in the current directory, i. e. your home directory: 
```bash
ls
```
Your home directory might look empty, but is it? 
```bash
ls -a
```
The ```-a``` switch makes ```ls``` show hidden files, which start with a dot in their file name.
You might notice that the contents of the directory you are currently in are also displayed on the right hand panel in MobaXterm and you can use the icons and address bar to navigate the directories in bessemer. 

We are going to edit the file ```.bash_profile``` to configure your account so that you have access to the Genomics Software Repository that we will be using. The Genomics Software Repository is basically a collection of ready-to-use programs for NGS and population genetic/genomic analysis in a shared folder. Its main advantage is that it removes the necessity for the user to install commonly used programs in their home folder.

You can have access by adding the following to the end of your bash profile. The .bash_profile is a configuration file for configuring user environments e.g. it contains all the startup configuration and preferences for your command line interface.

```
if [[ -e '/usr/local/extras/Genomics' ]]; 
then
    source /usr/local/extras/Genomics/.bashrc
fi
```
To do this we will use the program ```nano```, which is a simple text editor that can be used from the command line
```bash
nano .bash_profile
```
You will see something like
```
# .bash_profile

# Get the aliases and functions
if [ -f ~/.bashrc ]; then
        . ~/.bashrc
fi

# User specific environment and startup programs

PATH=$PATH:$HOME/bin

```
Copy the text you want to insert from above and paste it at the end. You will need to use the arrow buttons to move the cursor within the file (the mouse doesn't work here) and the right mouse button can be used to paste to the command line (^V doesn't work in Linux). Usefully, you will see there is information at the bottom of the screen that tells you how to save the file (ctrl o, save it with the same name) and exit (ctrl x).

Another way of viewing the content of a text file is with ```less```. Unlike ```nano``` less is just a viewer, not an editor. It is particularly useful for viewing very large files, because it only shows them a few lines at a time. To check that your edit has worked and your ```.bash_profile``` file looks OK type in
```bash
less .bash_profile
```
Check that the Genomics Software Repository path is there in the file (you may need to use the arrow keys to move to the end of the file). It should look something like this
```
# .bash_profile

# Get the aliases and functions
if [ -f ~/.bashrc ]; then
        . ~/.bashrc
fi

# User specific environment and startup programs

PATH=$PATH:$HOME/bin

if [[ -e '/usr/local/extras/Genomics' ]];
then
    source /usr/local/extras/Genomics/.bashrc
fi
```
Type ```q``` to quit less.
There are many options that can be used with ```less``` in particular to control how many, and which, lines are shown and for searching the text. You can see what these are using
```bash
man less
```
Adding ```man``` before most Linux commands will show you the manual page. The manual itself is opened using ```less``` so you can try out some of the options while you're there. 
What does ```z``` do?  

#### Table of useful ```less``` options

| Keyboard | What it does |
| ------- | ---- | 
| up arrow | one line up |
| down arrow | one line down |
| f or Space | one screen size down |
| b | one screen size up |
| d | half a screen size down |
| u | half a screen size up |
| G | jump to end of file |
| g | jump to beginning of file |
| h | get help |
| q | exit help |
| q | exit less |

To check that the setup worked, we will need to log out of the hpc and then log in again. Log out of the working node first by typing ```logout``` and then ```logout``` again to exit bessemer. 

## 3. Navigating, creating directories and moving files
Log in again (starting a new ssh session) and start a new interactive session (```srun --pty bash -l```). You should then see
```
  Your account is set up to use the Genomics Software Repository
```
You should now see this every time you log in and start a new interactive session.

We are going to create a working directory in the /fastdata directory on bessemer for you to work within during this practical. The fastdata directory is useful because there are no limits to the amount of data you can put there and data there can also be accessed faster (by the machine) than elsewhere on the cluster. However, it is not meant for long term storage of your data and everything on fastdata is automatically deleted after 3 months. It is also good practice for you to delete any data you no longer need, so as not to clog up fastdata for everyone else. If you are working with large data sets for your research project, your supervisor will probably be able to give you access to their group storage area (in ```/shared```) and you also have ```/data``` directory with a file limit of 100GB. Read more about filestores here:
https://docs.hpc.shef.ac.uk/en/latest/hpc/filestore.html

Move to the fastdata directory:
```bash
cd /fastdata
```
Why is the ```/``` there? What happens if you put ```cd fastdata``` instead? Why is this? What happens if you enter ```cd /fast``` and then press Tab? This is called tab completion and is extremely useful, particularly for long file or folder names!

Create a new directory here that is named your username (ie. boxxx, replacing the xxx)
```bash
mkdir boXXX
```
## 4. Familiarise yourself with UNIX

Make a new folder in the new directory you made (HINT: mkdir)
Move into that new folder (HINT: cd)
Find your current path (HINT: pwd)
Make a new file (HINT: nano)
Move back a folder (HINT: cd ..)

Try to run a program (e.g PLINK) (HINT: you need to be interactive mode to do this (srun --pty bash -i)



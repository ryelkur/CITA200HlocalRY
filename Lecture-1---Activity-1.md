[Unix terminal command line cheat sheet ](http://www.pixelbeat.org/cmdline.html)

[//]: # ([http://cli.learncodethehardway.org/bash_cheat_sheet.pdf])

## Gaussian 2D

> Hi,

> I have a C++ code that generates a 2-d array with Gaussian
distribution in my home directory /home/cta200 (recall that my user name is cta200).
There's a Python script
that generates the plot from an output file. Please copy the project
into your `/mnt/scratch-lustre` space and run it with different
parameters. I compiled with gcc/5.4.0, but other versions should work
too. You can change the geometry and deviation. Run it with "-help" to
get the options.

> If you are going to modify the code, please put it in a git repository.

> Chris T.A.

### Navigation

- What is directory, what's special about home directory?
- Locate this project in /home/cta200.
    - `cd`
    - `cd ..`
    - `ls`
    - hint `find -name '*auss*'`
    - Relative vs absolute paths?
- Common practice: implement the core of a program in C or Fortran, then
plot with a Python script.
- What is my `/mnt/scratch-lustre` space and how should I organize it?
Consider where to put the following:
    - my own projects
        - Suggest: `mkdir /mnt/scratch-lustre/$USER/gauss2d`
    - downloaded source code for building programs and libraries
        - `src` by convention, "source"
    - programs and libraries built from source
        - `opt` by convention, "optional"
        - or `bin` for binaries (executibles)
        - and `lib` for libraries
- Copy to your `gauss2d` directory
    - hint: `cp -av /home/cta200/Research/gauss2d
/mnt/scratch-lustre/$USER/gauss2d`

### Source code: compilation and execution

- Have a look at the source files
    - `less gauss2d.cc`
    - `cat Makefile`
    - `vim plot.py`
    - `gedit plot.py`
- About compilers
    - GCC, the GNU Compiler Collection: `gcc` for C, `g++` for C++,
`gfortran` for Fortran
    - Intel compilers: `icc` for C, `icpc` for C++, `ifort` for Fortran
    - Forward compatibility
    - Module system
        - `module avail`
        - `module avail gcc`
        - `module load gcc/5.4.0`
- Compile the C code
    - Suggestion: First by hand then with Makefile
    - Minimal example: `g++ gauss2d.cc -o gauss2d`
    - The absolute minimal example: `g++ gauss2d.cc`
         - If the resultant executible is not obvious, run `ls
-lt` to find the most recently generated file
- Execute, hoping the program is functional and has set default parameters.
- Output redirection:
    - Save the output into a file `./gauss2d > data.txt`

### Plotting

- Usual ways to run a python script
   - load python module `module load python/2.7.12`
    - `./script.py`
    - `python script.py`
    - Check the first line of this script with `head -1 plot.py`
        - `"#!/usr/bin/env python"` is present, execute as
`./script.py`.
- Usual ways to take input
    - `./script.py < data.txt`
    - `./script.py data.txt`
- Notice code `"argparse.FileType('r')"` in `plot.py` -- this
program takes file as an argument.
    - What is "argument"?
    - Try `./plot.py data.txt`
    - About permission
        - `chmod u+x plot.py`
- Pipe the output
    - Workflow without pipe: `./gauss2d > data.txt; ./plot.py data.txt`
    - With pipe: `./gauss2d | ./plot.py`
- Notice you can rotate the plot.

### Options

- What is "option"? How to "Run it with '-help' to get the options"?
    - Try `./gauss2d -help`
- Find the default setting for the options in the code
    - Look for assignment statements. Hint: `grep "dim\s*=\s*[0-9]" *.cc` and `grep "sigma\s*=\s*[0-9]" *.cc`
- "change the geometry" means changing number of rows and columns, which
don't have to equal. Because the program sets defaults, we don't have to
specify all options:
    - Try `./gauss2d -xdim 100 -ydim 50 | ./plot.py`
    - `./gauss2d -xsigma 30 | ./plot.py`
    - Have a look at the program, the number of points is `xdim * ydim`. Even `xdim = 1000, ydim = 1000` gives one million points to plot in Python, this takes a lot of resources.
        - Process management: `top`, `Ctrl-z`, `bg`, `fg`, `ps aux`, `kill -9 [pid]`

### Source code: editing and git repository

- What is git and what is a git repository?
- Set up two repositories, one local and one "remote", on different file systems. Procedure below
- `.git` -- `.*` hidden directories, try `ls -la ~`.
- Do some minor editing, commit and push the changes
    - Add a description to the C code `/* This program .... */`
    - Add a description to the Python script `""" This script ... """`
    - Change "xsigma" and "yxigma" to "xdev" and "ydev" with search replace in vim or with sed.

Some global settings for git.

```bash
git config --global user.name "Claire"
git config --global user.email myemail@utoronto.ca
```

Set up a central location to host remote git repositories for all projects. We'll have it in the home directory.

```bash
cd ~
mkdir -p repos/gauss2d.git
cd repos/gauss2d.git
git init --bare
```

Set up a git repository in the project directory.

```bash
cd /mnt/scratch-lustre/$USER/gauss2d
git init
echo "*.o" > .gitignore
```

Add source code files to keep track of. First local commit.

```bash
git add gauss2d.cc Makefile plot.py .gitignore
git status
git commit -m "Working 2D Gaussian array generation code and plotting script"
git log
```

Specify remote repository then confirm in the config file

```bash
git remote add origin /home/$USER/repos/gauss2d.git
cat .git/config
```

The first push.

`git push --set-upstream origin master`


Next task: Edit the C and Python source code files. Add a program description to both files.

```bash
vim gauss2d.cc
vim plot.py
```

The usual workflow to add and commit changes

```bash
git status
git diff
git add -u
git status
git commit -m "Added program description. Renamed sigma to dev[iation]"
```

Often during development we do not push to the remote repo until a big chunk of work is done. Here we hold off the push until the next edit is finished.

Next task: In the C code, replace all occasions of "sigma" to "dev" (deviation). We will first make the changes in `vim`. Then restore to the original version of file with git. Then modify it again with `sed`.

Open the file with vim. Make sure you are in the command mode -- press "Esc" when in doubt. Type exactly

`:%s/sigma/dev/gc`

Press 'y' twice to see what it does, then abort the command by pressing "Esc" twice. Now finish the rest of the search and replace with the command without the trailing "c"

`:%s/sigma/dev/g`

To turn off highlight at any time, type the no-highlight command

`:noh`

Save the file and exit. We can compare the new version of the source code with the latest committed version:

`git diff`

We did not do `git add` yet, so this change is "unstaged". To discard all changes and revert to the latest committed version, run

`git checkout -- *`

*The dash dash `--` is not necessary in this case.

If you have already staged the change with `git add`, revert with the following

```bash
git checkout -f master
git clean -fd
```

*The `git clean` command is not necessary in this case, but good to remember.

Next, we accomplish the same search replace with `sed`. First a dry-run where the original file is not modified.

`sed 's/sigma/dev/g' gauss2d.cc | less`

Inside `less`, search for "sigma" by typing `/sigma` to confirm its absence; then search for "dev".

Confirm the file has not been changed.

`git status`

Now modify the file with an "in-place" `sed` operation.

`sed -i 's/sigma/dev/g' gauss2d.cc`

Commit the changes.

```bash
git diff
git add -u
git status
git commit -m "Renamed sigma to dev[iation]"
```

Push recent commits to central repo.

```bash
git push
```

Format the git log

```bash
git log --stat --pretty=fuller --decorate
```

GUI to view repo history

```bash
gitk
```

### Extra: Sync working directories on home and work computers via bare remote repository

The same procedure applies if the project is shared among collaborators.

To set up a working directory on home computer first [[set up ssh to use gateway as proxy | access git repo at CITA]] then clone the repo from a CITA server

`git clone USERNAME@trinity.cita.utoronto.ca:repos/gauss2d.git`

A directory is created with the identical content as `/mnt/scratch-lustre/$USER/gauss2d`.

Work flow for working with multiple working directories

```bash
# First sync with the remote branches
git fetch
git diff master origin/master
git merge origin/master
# alternatively, if you know exactly what was modified and are sure there is no conflict
git pull

# Edit then commit
git add .
# or
git add -u
git commit
git push
```

Suggestion: Learn about git branches
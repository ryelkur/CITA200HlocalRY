## Basics: Remote access with ssh, and basic operations

### Remote access through gateway:

```bash
# Lines starting with the sharp sign, like this one, are comments.
# Execute all commands one by one.

# replace YOUR_USERNAME with your actual username, such as course05
ssh YOUR_USERNAME@gw2.cita.utoronto.ca
# You are on gw2 now

# replace X with 1,2,3 or 4, eg. cosmo2
ssh cosmoX
# You are on cosmoX now
```

### Command execution:

`/cita/local/bin/passwd`

To terminate the command execution and abort password change, press Ctrl-C.

### Directory and file manipulation, man page

```bash
# Print working directory
pwd

# List files in current directory
ls

# Change directory
cd /mnt/scratch-lustre/$USER

# Make directory
mkdir test
# Here 'test' is the relative path
# This command is equivalent to
# mkdir /mnt/scratch-lustre/$USER/test

# Make directory containing subdirectory
mkdir -p tmp/test

# Check manpage to learn about the -p, --parents option
man mkdir
# Navigate manual with arrow-up, arrow-down, pgUp, and PgDn
# Search by typing /-p

# Navigate into directory 'test'
ls
cd tmp/test  # Try tab completion.

# Navigate out, then back in
cd ../..
pwd
cd -

# Experiment with directory deletion
# Directory "a" is empty and "b" is non-empty
mkdir a b
touch b/file-0
ls a
ls b
rmdir a
rmdir b  # rmdir does not delete non-empty directory
# Double check before executing the following command
rm -rf b
# Read the man page to learn what -r and -f stand for
# Search with /-r and /-f
# Jump to the next or previous search result by pressing n or N
man rm

# Copy, rename, and remove files
mkdir Pictures
cd Pictures
cp /mnt/scratch-lustre/cta200/2016/Pictures/Montreal_City_720x480.jpg .
ls
mv Montreal_City_720x480.jpg Montreal.jpg
ls
mv Montreal{,_City}.jpg
ls
rm Montreal_City.jpg

# Copy 'Toronto' directory, including the directory itself. Note: no trailing slash.
rsync -avP /mnt/scratch-lustre/cta200/2016/Pictures/Toronto .
ls
ls Toronto
# Copy the entire content of 'Pictures'. Note: trailing slash after 'Pictures'.
# If trailing slash is omitted, it will be copied as `Pictures/Pictures` instead.
rsync -avP /mnt/scratch-lustre/cta200/2016/Pictures/ .
ls
```

### Command, option, and argument:

```bash
cd ~
ls
ls -l
ls -l tmp
```

## Basics: File editing

### File editing without editor

```bash
# Create file without content
touch file-1
cat file-1

# Standard output ("stdout") redirection
echo 'Hello' > file-2
cat file-2

# ">>" append
# ">" overwrite
echo 'World!' >> file-2
cat file-2
echo 'Astronomy' > file-2
cat file-2
```

Generate data file with a for-loop directly on command line

```bash
for x in {a..z}
do
echo $x >> file-x
done
```

The equivalent one-liner

`for x in {a..z}; do echo $x >> file-x; done`

Write a bash script with "here document"

```bash
cat <<EOT >> genFileN.sh
#! /bin/bash
rm -f file-n
for n in {1..100}
  do
    printf "\$n\t\$((n+1))\n" >> file-n
  done
EOT
```

Make script executible, then execute it.


```bash
chmod u+x genFileN.sh
./genFileN.sh
```

View a long file with "less"

```bash
less file-x  #Press 'q' to exit
less file-n
```

### File editing with vim

Copy the vim cheatsheet

`scp lobster:/scratch/cta200/GSVimCheatsheet.png
/mnt/scratch-lustre/$USER`

Oops, "Permission denied"! Tell your instructor to give this file group
read permission then attempt again.

That is, the instructor needs to run on lobster `chmod g+r
/scratch/cta200/GSVimCheatsheet.png`
# CTA200 2019 Computing Information Sheet

Welcome to the CITA Computing Course 2019! If you do not already have a CITA account, a course account is assigned to you and a sheet with your username and password should accompany this instruction. Below is some information to get you started with the CITA computing resources.

For more information, please visit the CITA Wiki at [http://wiki.cita.utoronto.ca/]()

## Access CITA Computing System from a Computer in MP257

A server is assigned to you based on where you are seated according to this diagram:

            ----------
            | podium |
            ----------
    ---------------------------
    |   cosmo1   |   cosmo2   |
    ---------------------------
    |   cosmo4   |   cosmo3   |
    ---------------------------
            ----------
            |  door  |
            ----------


1. Open a "**Cygwin64 Terminal**" and enter the following, replacing [server] and [username] with your assigned server -- **cosmo1**, **cosmo2**, **cosmo3** or **cosmo4** and username.

    `ssh -g -L5912:[server]:5912 [username]@gw2.cita.utoronto.ca`

    - If prompt "Are you sure you want to continue connecting (yes/no)?", type "yes".
    - **NB**: This terminal needs to remain open in order to maintain connection to the CITA system.
2. Open "**TigerVNC Viewer**", enter the following then click "Connect".

    `localhost:12`
3. A new window with graphic desktop should pop up. Enter your CITA or course username and password to log in.
4. Press **F8** to toggle full screen mode.
5. Make sure you **log out** and **kill the ssh session** (type "exit" in the Cygwin prompt) when you leave the
computer.


The same commands also work on your personal computer. You just need to install a vnc client, for example TigerVNC or RealVNC for Mac and OpenVNC for Linux.

## Change password

On the `cosmoN` desktop open a terminal and do the following:

```
/cita/local/bin/passwd
# enter old password
# enter new password and confirm
exit
```

**Please destroy the sheet of paper with username and password after password change.**

## Course Material

The course homepage is [https://github.com/CITA/CTA200H/wiki]().  
Material for the first lecture, Scientific computing workflow in Linux, can be accessed from the sidebar. Material for the rest of the course is available online at [https://github.com/ttricco/cta200h](). To follow the exercises you should copy the material to your computer with

`git clone https://github.com/CITA/CTA200H.wiki.git`

## Software Environment

CITA servers run Linux CentOS 6 and come with the usual compilers (gcc, gfortran, icc, ifort), python, scientific
software including Matlab, Mathematica (limited number of licenses), IDL, and libraries such as OpenMPI, fftw, gsl and much more. Multiple versions of most libraries exist according to need and are activated using the **modules** environment. For example, to view the available modules type:

`module avail`

and to load a particular set of modules type e.g.,

`module load gcc/5.4.0 openmpi/2.0.0-gcc-5.4.0`

This would load version 5.4.0 of the gnu compilers along with the OpenMPI libraries and compilation wrappers for parallel programmes. Type `module` alone to see the various options available with the module command.

For **Python**, the current latest versions on our system are 2.7.14 and 3.6.4. New python programs should be developed with the latest Python interpreter and Python modules to keep up with bug-fixes. However, we may use an older module in this course for compatibility reason.

`module load gcc/5.4.0 python/2.7.12`

Please refer to article "[Using and Developing with Python](http://wiki.cita.utoronto.ca/mediawiki/index.php/Using_and_Developing_with_Python)" in the CITA wiki for instructions on installing Python modules on your own.
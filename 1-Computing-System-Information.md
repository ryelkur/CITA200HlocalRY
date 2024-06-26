# CTA200 2021 Computing Information Sheet

Welcome to the CITA Computing Course 2023! A course account is assigned to you and an instruction has been emailed to you. Below is some information to get you started with the CITA computing resources.

For more information, please visit the CITA Wiki at [http://wiki.cita.utoronto.ca](https://wiki.cita.utoronto.ca/index.php/Welcome_to_the_CITA_Wiki).

You will need your CITA login credentials to access the wiki.

## Remote Access with Two-factor Authentication
Remote ssh logins must go through the CITA gateway machine `gw.cita.utoronto.ca`. The gateway
requires your username and password along with a 6-digit verication code to login. The Google Authenticator (GAuth) app provides a code that changes every 30 seconds. You will need to install GAuth in a
browser or on your smartphone to generate these codes.

**Browser Instructions**
1. Open a browser at this URL: `https://gauth.cita.utoronto.ca`
2. Click on the pencil icon in the upper right and then the `+Add` button. Enter CITA Account name and type in or cut and paste your Secret key. Your Secret key can be found in the Account info sheet that has been emailed to you.
3. You can delete the EXAMPLE key if you wish.

**Smartphone Instructions**
1. Install the Google Authenticator app on your smartphone (search Google Play or the App Store).
2. Add you Secret key by taking a picture of the QR code or type it in.

Once you have logged into the gateway, you can then ssh login from there to other CITA servers and the cluster to conduct your research.


## Password Change
Open a terminal to log in to the CITA gateway `gw.cita.utoronto.ca` and change your password to something private immediately following these steps:

```
ssh username@gw.cita.utoronto.ca
/cita/local/bin/passwd
# enter old password
# enter new password and confirm
exit
```
On Windows computers, the PowerShell includes an ssh client so use that for your terminal. On Linux and Mac computers, open a terminal app.

## Remote Access with CITA VPN
CITA provides a virtual private network (VPN) connection which simplies remote access to CITA computers and services. Once set up on your remote computer, you can login directly to CITA computers without using the gateway, copy data with scp, sftp or rsync and access the software license server. It is the best way to gain access to CITA remotely.

Read here to learn how to set it up: [http://wiki.cita.utoronto.ca/index.php/CITA_Remote_Access](http://wiki.cita.utoronto.ca/index.php/CITA_Remote_Access).


## Access CITA Computing System remotely from your home computer

A server is assigned to you based on your birthday:
```
cosmo1.cita.utoronto.ca:6 (Jan, Feb, Mar)
cosmo2.cita.utoronto.ca:6 (Apr, May, Jun)
cosmo3.cita.utoronto.ca:6 (Jul, Aug, Sep)
cosmo4.cita.utoronto.ca:6 (Oct, Nov, Dec)
```
1. You will need to set up a Virtual Network Computing (VNC) connecting to cosmo servers. VNC works with Windows, Macs and Linux computers or laptops. The detailed instructions for setting up a VNC desktop are available here: [http://wiki.cita.utoronto.ca/index.php/VNC_Remote_Desktop](http://wiki.cita.utoronto.ca/index.php/VNC_Remote_Desktop).


2. After setting up VNC, you can connect to the remote desktop on one of the cosmo servers from your home computer. You will have to install a VNC client, for example TigerVNC or RealVNC for Mac and OpenVNC for Linux.


**Please destroy the sheet of paper with username and password after password change.**

## Course Material

The course homepage is [https://github.com/CITA/CTA200H/wiki]().  
Material for the first lecture, Scientific computing workflow in Linux, can be accessed from the sidebar. Material for the rest of the course is available online at [https://github.com/CITA/CTA200H](). To follow the exercises you should copy the material to your computer with

`git clone https://github.com/CITA/CTA200H.wiki.git`

## Software Environment

CITA servers run Linux CentOS 6 and 7 and come with the usual compilers (gcc, gfortran, icc, ifort), python, scientific software including Matlab, Mathematica (limited number of licenses), IDL, and libraries such as OpenMPI, fftw, gsl and much more. Multiple versions of most libraries exist according to need and are activated using the **modules** environment. For example, to view the available modules type:

`module avail`

and to load a particular set of modules type e.g.,

`module load gcc/5.4.0 openmpi/2.0.0-gcc-5.4.0`

This would load version 5.4.0 of the gnu compilers along with the OpenMPI libraries and compilation wrappers for parallel programmes. Type `module` alone to see the various options available with the module command.

For **Python**, the current latest versions on our system are 2.7.14 and 3.6.4. New python programs should be developed with the latest Python interpreter and Python modules to keep up with bug-fixes. However, we may use an older module in this course for compatibility reason.

`module load gcc/5.4.0 python/2.7.12`

Please refer to article "[Using and Developing with Python](https://wiki.cita.utoronto.ca/index.php/Using_and_Developing_with_Python)" in the CITA wiki for instructions on installing Python modules on your own.
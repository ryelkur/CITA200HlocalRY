# Install QFITS library

> Hi,

> Please install your own copy of the qfits library. The one on the system is too old.

> Christ T.A.

This is a typical task involving

```bash
./configure --prefix=...
make
make install
```

Find the webpage of the library with a web search

https://www.eso.org/sci/software/eclipse/qfits/

According to the description, qfits is a C library for FITS files.

Decide on the build and installation path:

- Build path: `/mnt/scratch-lustre/$USER/src`
- Installation path: `/mnt/scratch-lustre/$USER/opt/qfits/6.2.0`

Download the latest source and extract.

```bash
cd /mnt/scratch-lustre/$USER
cd src
wget ftp://ftp.eso.org/pub/qfits/qfits-6.2.0.tar.gz
tar -zxf qfits-6.2.0.tar.gz
```

Navigate into source and read installation notes

```bash
cd qfits-6.2.0
ls
less README
```

README contains no installation information; and INSTALL file is not
present. So go back to webpage to read the library's
[online-documentation](https://www.eso.org/sci/software/eclipse/qfits/html/index.html).
The installation follows the standard procedure `./configure
--prefix=install_dir ; make ; make install`.

Step by step:

```bash
mkdir -p /mnt/scratch-lustre/$USER/opt/qfits/6.2.0
./configure --prefix=/mnt/scratch-lustre/$USER/opt/qfits/6.2.0
make -j 2
make install
```

Installation finishes. Navigate to the installation path to confirm

```bash
cd ../../opt/qfits/6.2.0/
ls
ls lib
ls bin
```

The system can't find the installation yet

`which dfits`

Based on installed directories, decide what environment variables to modify:

- `bin` -- `$PATH` for executibles.
- `include` -- header files; it's a C library so `$CPATH`.
- `lib` -- `$LIBRARY_PATH`, and also `$LD_LIBRARY_PATH` to allow dynamic
linking to '*.so`.
- `man` -- `$MANPATH` for man page.

Add the following to `~/.bashrc`

```bash
# /home/#USER/.bashrc
export QFITS="/mnt/scratch-lustre/$USER/opt/qfits/6.2.0/"
export PATH="$QFITS/bin:$PATH"
export CPATH="$QFITS/include:$CPATH"
export LIBRARY_PATH="$QFITS/lib:$LIBRARY_PATH"
export LD_LIBRARY_PATH="$QFITS/lib:$LD_LIBRARY_PATH"
export MANPATH="$QFITS/man:$MANPATH"
```

Put the new path definition into effect. Now the system can locate the
installation

```bash
. ~/.bashrc
# or equivalently "source ~/.bashrc"
which dfits
```

Remove the installation files but leave the source tar ball.

`rm -rf /mnt/scratch-lustre/$USER/src/qfits-6.2.0`

Suggestion: Instead of defining various paths in `.bashrc`, define your own environment module following the instruction on the CITA wiki http://wiki.cita.utoronto.ca/mediawiki/index.php/Personal_Environment_Modules
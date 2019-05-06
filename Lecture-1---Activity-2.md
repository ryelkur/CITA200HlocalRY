## Eigenmvn from github

> Hi,

> We talked about multivariate normal distribution sampling the other day. I saw an implementation on github. See if you can get the test case to run. Maybe we can incorporate it in our own code.
https://github.com/beniz/eigenmvn

> Chris T.A.

Goal: follow the instruction "Usage" and successfully generate the plot in readme.

### Obtain the source code from github

```bash
cd /mnt/scratch-lustre/$USER/
git clone https://github.com/beniz/eigenmvn
ls
cd eigenmvn
```

### Read the README..md file

### Prepare for compilation

Breakdown of the compilation command:

```bash
g++ -I/usr/include -I/usr/include/eigen3 -g -std=c++11 test_eigenmvn.cc
-o te
```

- `g++`: use the gnu C++ compiler
    - We should load a gcc module.

```bash
module avail gcc
module load gcc/4.9.2
```

- `-I/usr/include`: link to the system header files
    - Headers in this directory is automatically included by compiler.
This option is not needed.
    - Check source code to see if non-standard header files are needed.
- `-I/usr/include/eigen3`: link to `eigen3` headers
    - Check `/usr/include` directory to see if eigen3 is present.
    - If not, install eigen3 first.

```bash
head test_eigenmvn.cc
```

In output, `<fstream>` and `<iostream>` are standard. Is `eigenmvn.h`
available?

`ls /usr/include | grep eigen3` returns nothing. It needs to be
installed.

- `-g`: related to debugging
- `-std=c++11`: use the C++ 11 standard
- `test_eigenmvn.cc`: source code to be compiled
- `-o te` output to executible `te`
    - We will change the output to "test_eigenmvn" instead, the base
name of the source code.

### Install Eigen3

Find the Eigen3 homepage

http://eigen.tuxfamily.org/index.php?title=Main_Page

Decide on the build and installation path:

- Build path: `/mnt/scratch-lustre/$USER/src`
- Installation path: `/mnt/scratch-lustre/$USER/opt/eigen3`

Download the latest stable release and extract

```bash
cd /mnt/scratch-lustre/$USER/src
wget http://bitbucket.org/eigen/eigen/get/3.2.8.tar.gz
tar -zxf 3.2.8.tar.gz  # -z unzip "gz", -x "extract", -f specify "file"
```

Navigate into the source directory and learn how to install

```bash
cd eigen-eigen-07105f7124f9
less INSTALL
```

Follow this insturction:

> "You can use right away the headers in the Eigen/ subdirectory. In order
to install, just copy this Eigen/ subdirectory to your favorite location."

```bash
mkdir -p /mnt/scratch-lustre/$USER/opt/eigen3
# Do not append a trailing  slash after "Eigen" in the command below
rsync -avP Eigen /mnt/scratch-lustre/$USER/opt/eigen3
ls /mnt/scratch-lustre/$USER/opt/eigen3/Eigen
```

Clean up. Remove the uncompressed directory and leave the tar ball.

`cd ..; rm -rf eigen-eigen-07105f7124f9`

### Compile, run, and plot test case for eigenmvn

Back to the `eigenmvn` directory. Now we can compile, run and plot. Edit
the `eigen3` path to our installation path.

```bash
cd /mnt/scratch-lustre/$USER/eigenmvn
g++ -I/mnt/scratch-lustre/$USER/opt/eigen3 -g -std=c++11
test_eigenmvn.cc -o test_eigenmvn
./test_eigenmvn
gnuplot
plot 'samples_solver.txt', 'samples_cholesky.txt'
```
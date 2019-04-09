## Set up a Python virtual environment

> Hi,

> Please set up a virtual environment for you next Python project. 

> Chris T.A.

If your research heavily uses python code and depends on many python
modules, using virtual environment is highly recommended as without it
module dependencies tend to become unmanageable as the project grows and
ages.

Here we will set up a virtual environment using python version 2.7.13.

First, find out which version of gcc it depends on by looking for 'prereq' in the output of

`module show python/2.7.13`.

Procedure to set up the virtual environment.

```bash
module purge
cd /mnt/scratch-lustre/$USER
module load gcc/5.4.0 python/2.7.13
virtualenv --no-site-packages venv-2.7.13
module unload python
source venv-2.7.13/bin/activate
```

Virtual environment is ready to use. To go back to the system python, type

`deactivate`

We create the virtual environment with `--no-site-packages` so that the
python modules installed on the system will not taint our environment.
The downside is that we need to install all frequently used modules
ourselves, such as matplotlib, numpy and astropy. But that's easy, just
`pip install` away.

Try `pip install matplotlib`

`--user` option is not needed because files are written to your
`/mnt/scratch-lustre/$USER/venv-2.7.13`, ie. not a system location.

In the future you always have to load that specific `gcc` module and run
the `source` command to use this environment. To save some typing,
define an alias in `~/.bashrc`.

```bash
# /home/$USER/.bashrc
alias venv="module load gcc/4.9.2; source /mnt/scratch-lustre/$USER/venv-2.7.13/bin/activate"
```

Source it to put the alias into effect

`. ~/.bashrc`

Try it out

```bash
venv
python --version
deactivate
python --version
```

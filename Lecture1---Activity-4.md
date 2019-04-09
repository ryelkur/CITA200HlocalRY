# Install python module pygrace

> Hi,

> I have an old code that needs the python/2.7.3 module to work. Please make sure you have pygrace installed.

> Chris T.A.

- Why does an old code need an old version of python?
    - About python modules
    - The dependency / backward [in]compatibility problem of python
- About python environment modules

Just load the module and see if you can import pygrace.

```bash
module load python/2.7.3
ipython
import pygrace
```

You encounter "ImportError: No module named pygrace". Pygrace is not installed. Listing all modules installed for python/2.7.3 and search for pygrace should return nothing.

```bash
pip freeze | grep pygrace
```

Install pygrace with `pip`. Specify the `--user` option to do a user local install. This does not write file to system location such as `/usr/lib`, therefore does not require root privilege.

```bash
pip install --user pygrace
```

Confirm

```bash
pip freeze | grep pygrace
```

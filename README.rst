==================
README for cyipopt
==================

Ipopt_ (Interior Point OPTimizer, pronounced eye-pea-opt) is a software package
for large-scale nonlinear optimization. Ipopt is available from the COIN-OR_
initiative, under the Eclipse Public License (EPL).

**cyipopt** is a Python wrapper around Ipopt. It enables using Ipopt from the
comfort of the Python programming language.

.. _Ipopt: https://projects.coin-or.org/Ipopt
.. _COIN-OR: https://projects.coin-or.org/

Status
======

.. list-table::

   * - Anaconda
     - .. image:: https://anaconda.org/conda-forge/cyipopt/badges/version.svg
          :target: https://anaconda.org/conda-forge/cyipopt
       .. image:: https://anaconda.org/conda-forge/cyipopt/badges/downloads.svg
          :target: https://anaconda.org/conda-forge/cyipopt
   * - PyPI
     - .. image:: https://badge.fury.io/py/cyipopt.svg
          :target: https://pypi.org/project/cyipopt
       .. image:: https://pepy.tech/badge/cyipopt
          :target: https://pypi.org/project/cyipopt
   * - Read the Docs
     - .. image:: https://readthedocs.org/projects/cyipopt/badge/?version=latest
          :target: https://cyipopt.readthedocs.io/en/latest/?badge=latest
          :alt: Documentation Status

History
=======

**This repository was forked in 2016 from https://bitbucket.org/amitibo/cyipopt
and is now considered the primary repository.** The fork includes a SciPy-style
interface and ability to handle exceptions in the callback functions.

As of version 1.1.0 (2021-09-07), the distribution is released under the name
"cyipopt" on PyPi (https://pypi.org/project/cyipopt). Before version 1.1.0, it
was released under the name "ipopt" (https://pypi.org/project/ipopt).

Installation
============

We recommend using conda to install cyipopt on Linux, Mac, and Windows::

   conda install -c conda-forge cyipopt

Other `installation options`_ are present in the documentation.

.. _installation options: https://github.com/mechmotum/cyipopt/blob/master/docs/source/install.rst


Building `manylinux` wheels
===========================

manylinux wheels can be built for a tagged version (GIT_TAG below) of cyipopt via docker by running (while in the root of this repo)::

   docker run -v $(pwd):/wheels --rm --platform=linux/amd64 quay.io/pypa/manylinux_2_28_x86_64 bash /wheels/build_manylinux_wheels.sh GIT_TAG

for linux/amd64 and::

   docker run -v $(pwd):/wheels --rm --platform=linux/aarch64 quay.io/pypa/manylinux_2_28_aarch64 bash /wheels/build_manylinux_wheels.sh GIT_TAG

for linux/aarch64 platforms. Built wheels appear at the folder the command was executed from.

.. warning::
    Docker supports emulating non-native platforms to e.g. produce ARM binaries from an AMD64 host. However this can be quite slow (~1h for our case).

Using in Pyodide (browser/WASM)
================================

cyipopt can run in the browser via `Pyodide <https://pyodide.org>`_, with Ipopt
compiled to WebAssembly. Pre-built wheels are available from
`GitHub releases <https://github.com/mechmotum/cyipopt/releases>`_.

Install with micropip in a Pyodide environment:

.. code-block:: python

   import micropip
   await micropip.install(
       "https://github.com/mechmotum/cyipopt/releases/download/VERSION/cyipopt-VERSION-cp312-cp312-pyodide_2024_0_wasm32.whl"
   )

Then use it normally:

.. code-block:: python

   import numpy as np
   from cyipopt import minimize_ipopt
   from scipy.optimize import rosen, rosen_der

   x0 = np.array([1.3, 0.7, 0.8, 1.9, 1.2])
   res = minimize_ipopt(rosen, x0, jac=rosen_der)
   print(res.x)

**Full example**: see the `grecov calculator <https://louisabraham.github.io/grecov/>`_
for a working web app that uses cyipopt in Pyodide to solve nonlinear optimization
problems entirely in the browser.

License
=======

cyipopt is open-source code released under the EPL_ license, see the
``LICENSE`` file.

.. _EPL: https://www.eclipse.org/legal/epl-2.0/

Contributing
============

For bug reports, feature requests, comments, patches use the GitHub issue
tracker and/or pull request system.

This project does not accept code produced from generative AI tools due to the
indeterminate copyright license of such code. Generative AI use in
contributions must be fully disclosed and will be rejected unless there are no
copyright concerns. Contributions that make use of generative AI for
communication with the developers of this project will be rejected.

Contributors (made with `contrib.rocks <https://contrib.rocks>`_):

.. image:: https://contrib.rocks/image?repo=mechmotum/cyipopt
   :target: https://github.com/mechmotum/cyipopt/graphs/contributors

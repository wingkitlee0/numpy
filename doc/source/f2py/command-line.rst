.. _f2py-command-line:

======================
Command-Line Interface
======================

F2PY provides a command-line interface for compiling Fortran code into Python extension modules. This guide covers the available options and common usage patterns.

Basic Usage
-----------

F2PY can be invoked in two ways:

.. code-block:: bash

   # Using the f2py command (if available in your system)
   f2py [options] <fortran-files>

   # Using Python's module execution (recommended, works on all systems)
   python -m numpy.f2py [options] <fortran-files>

For consistency, we'll use the second form throughout this documentation.

Common Command-Line Options
---------------------------

Building Extension Modules
^^^^^^^^^^^^^^^^^^^^^^^^^^

``-c``
  Compile Fortran code and build an extension module.

``-m <modulename>``
  Specify the name of the extension module to be created.

Example:

.. code-block:: bash

   python -m numpy.f2py -c -m example example.f90

This compiles ``example.f90`` and creates a Python extension module named ``example``.

Working with Signature Files
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

``-h <filename.pyf>``
  Generate a signature file from Fortran source.

Example:

.. code-block:: bash

   python -m numpy.f2py example.f90 -h example.pyf

This creates a signature file ``example.pyf`` from ``example.f90``.

To build an extension module using a signature file:

.. code-block:: bash

   python -m numpy.f2py -c example.pyf example.f90

Compiler Options
^^^^^^^^^^^^^^^^

``--fcompiler=<compiler>``
  Specify the Fortran compiler to use (e.g., ``gnu95``, ``intel``, ``pg``).

``--f77exec=<executable>``
  Specify the F77 compiler executable.

``--f90exec=<executable>``
  Specify the F90 compiler executable.

``--f77flags=<flags>``
  Specify F77 compiler flags.

``--f90flags=<flags>``
  Specify F90 compiler flags.

Example:

.. code-block:: bash

   python -m numpy.f2py -c --fcompiler=gnu95 --f90flags="-O3" -m example example.f90

This uses the GNU Fortran compiler with optimization level 3.

Debugging Options
^^^^^^^^^^^^^^^^^

``--debug-capi``
  Add debugging information to the extension module.

``-v``
  Be verbose.

``--no-lower``
  Do not lower case the Fortran code.

Example:

.. code-block:: bash

   python -m numpy.f2py -c -m example example.f90 --debug-capi -v

This builds the extension with debugging information and verbose output.

Advanced Options
----------------

Selecting the build system backend
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

It is possible to the build system backend explicitly using the
``--backend`` option. For Python up to 3.11 and Numpy 1.x, the
default option is ``distutils``, which is set to be deprecated.
The new backend ``meson`` is supported since NumPy 1.26 and is
recommended for new projects. See :ref:`distutils-status-migration`
for more information.

Handling Multiple Files
^^^^^^^^^^^^^^^^^^^^^^^

You can compile multiple Fortran files into a single extension module:

.. code-block:: bash

   python -m numpy.f2py -c -m example file1.f90 file2.f90 file3.f

Including C Libraries
^^^^^^^^^^^^^^^^^^^^^

``--link-<resource>``
  Link extension module with <resource> (e.g., lapack, blas).

Example:

.. code-block:: bash

   python -m numpy.f2py -c -m example example.f90 --link-lapack

This links the extension module with the LAPACK library.

Getting Help
------------

For more information on the options, run:

.. code-block:: bash

   python -m numpy.f2py --help

For help on linking options:

.. code-block:: bash

   python -m numpy.f2py --help-link

For Different Approaches to Wrapping
----------------------------------

For detailed information on the different approaches to wrapping Fortran code
(direct compilation, using signature files, or using F2PY directives),
please see :doc:`wrapping_methods`.

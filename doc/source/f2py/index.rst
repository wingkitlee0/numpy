.. _f2py:

=======================
F2PY: Fortran to Python
=======================

F2PY (Fortran to Python interface generator) is a tool that provides
a connection between Python and Fortran languages by creating and
building . It was originally created by
Pearu Peterson, and older changelogs are in the `historical reference`_.

What F2PY does
--------------

* Creates `Python C/API extension modules`_ from Fortran sources
* Allows calling Fortran 77/90/95 routines from Python
* Enables access to Fortran 77 COMMON blocks and Fortran 90/95 module data
* Supports calling Python functions from Fortran (callbacks)
* Automatically handles data type conversions


Getting Started
---------------

If you're new to F2PY, start with the :ref:`f2py-quickstart` guide.

For more detailed information, explore the User Guide:

* :ref:`f2py-cli-usage` - Command-line usage
* :ref:`f2py-getting-started` - Different approaches to wrapping Fortran code
* :ref:`f2py-signature-files` - Working with signature files
* :ref:`f2py-build-systems` - Using F2PY with build systems
* :ref:`userguide/f2py-examples` - Examples

Advanced Topics
---------------

* :doc:`advanced/signature_syntax` - Detailed signature file syntax
* :doc:`advanced/attributes` - F2PY attributes reference
* :doc:`advanced/callbacks` - Working with callbacks

.. toctree::
   :maxdepth: 1

   quickstart
   userguide/command_line
   userguide/wrapping_methods
   userguide/signature_files
   userguide/build_systems
   advanced/signature_syntax
   advanced/attributes
   advanced/callbacks

.. toctree::
   :maxdepth: 3

   f2py-user
   f2py-reference
   windows/index
   buildtools/distutils-to-meson

F2PY can be used either as a command line tool ``f2py`` or as a Python
module ``numpy.f2py``. While we try to provide the command line tool as part
of the numpy setup, some platforms like Windows make it difficult to
reliably put the executables on the ``PATH``. If the ``f2py`` command is not
available in your system, you may have to run it as a module::

   python -m numpy.f2py

Using the ``python -m`` invocation is also good practice if you have multiple
Python installs with NumPy in your system (outside of virtual environments) and
you want to ensure you pick up a particular version of Python/F2PY.

If you run ``f2py`` with no arguments, and the line ``numpy Version`` at the
end matches the NumPy version printed from ``python -m numpy.f2py``, then you
can use the shorter version. If not, or if you cannot run ``f2py``, you should
replace all calls to ``f2py`` mentioned in this guide with the longer version.

.. _Python: https://www.python.org/
.. _NumPy: https://www.numpy.org/
.. _`historical reference`: https://web.archive.org/web/20140822061353/http://cens.ioc.ee/projects/f2py2e
.. _Python C/API extension modules: https://docs.python.org/3/extending/extending.html#extending-python-with-c-or-c
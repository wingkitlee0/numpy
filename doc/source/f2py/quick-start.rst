.. f2py-quickstart:

===========
Quick Start
===========

This guide will help you quickly get started with F2PY to wrap a simple Fortran subroutine.

Prerequisites
-------------

* Python with NumPy installed
* A Fortran compiler (gfortran, ifort, etc.)

Basic Example
-------------

Let's create a simple Fortran 77 subroutine that calculates Fibonacci numbers:

.. code-block:: fortran
   :caption: fib.f

   C     FILE: FIB.F
         SUBROUTINE FIB(A,N)
   C
   C     CALCULATE FIRST N FIBONACCI NUMBERS
   C
         INTEGER N
         REAL*8 A(N)
         DO I=1,N
            IF (I.EQ.1) THEN
               A(I) = 0.0D0
            ELSEIF (I.EQ.2) THEN
               A(I) = 1.0D0
            ELSE
               A(I) = A(I-1) + A(I-2)
            ENDIF
         ENDDO
         END

One-Step Wrapping
-----------------

The quickest way to wrap this Fortran subroutine is:

.. code-block:: bash

   python -m numpy.f2py -c fib.f -m fib

This command:

1. Compiles the Fortran file ``fib.f``
2. Creates a Python extension module named ``fib``

Using the Module
----------------

Now you can use the wrapped function in Python:

.. code-block:: python

   import numpy as np
   import fib

   # Create an array to hold the results
   a = np.zeros(8, 'd')

   # Call the Fortran subroutine
   fib.fib(a)

   print(a)  # [0. 1. 1. 2. 3. 5. 8. 13.]

Next Steps
----------

This is just the beginning! F2PY offers many more features:

* Creating signature files for more control
* Adding intent specifications
* Working with callbacks
* And much more

Continue to :doc:`user_guide/wrapping_methods` to learn about different approaches to wrapping Fortran code.
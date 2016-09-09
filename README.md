# Basic CMake Setup for a new Fortran Project

The idea is that you can fork this project into your own system, and you immediately have
a structure and a surrounding CMake environment to compile and test.

## Basic usage

After you have cloned this repo, go into its main directory and type the following:

    mkdir bld
    cd bld
    cmake ..
    make -j
    make install

This should build a tiny library `lib/static/liblib1.a` with a single funtion `is_two(n)`
which returns `.T.` if and only if the only parameter is indeed 2, and `.F.` otherwise,
and a single program `bin/exe1` that will write "Hello World" and check for each number in 1..5 whether
this number is indeed 2.

If you have pFUnit installed, it should also manage to write a unit test `test/test1` that tests the library.

## Writing your own libraries / modules

1. Create a new subdirectory under `libraries`.
2. Change the `libraries/CMakeLists.txt` to include your new subdirectory.
3. Copy the `libraries/lib1/CMakeLists.txt` into your new subdirectory and change the
project name.

## Writing your own executables

1. Create a new subdirectory under `executables`.
2. Modify `executables/CMakeLists.txt` to include your new subdirectory.
3. Copy `executables/exe1/CMakeLists.txt` into your new subdirectory and change
the project name. (Also, you might want to remove the dependency to `lib1`.)

## Writing your own tests

1. Create a new subdirectory under `tests`.
2. Modify `tests/CMakeLists.txt` to include your new subdirectory.
3. Copy `tests/test1/CMakeLists.txt` into your new subdirectory and change
the project name.
4. Ensure that you add a dependency to the library you want to test.
5. Write your `pFUnit` compliant tests into files with the extension `.pf`
6. Add the file name of all test files (without the `.pf`) to the `_tests` section
of `tests/<yourtest>/CMakeLists.txt`
7. Add an `add_test()` line to the `CMakeLists.txt` file in the root directory.

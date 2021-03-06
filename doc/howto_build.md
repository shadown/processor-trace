Building the Intel(R) Processor Trace (Intel PT) Decoder Library and Samples {#build}
============================================================================

<!---
 ! Copyright (c) 2013-2015, Intel Corporation
 !
 ! Redistribution and use in source and binary forms, with or without
 ! modification, are permitted provided that the following conditions are met:
 !
 !  * Redistributions of source code must retain the above copyright notice,
 !    this list of conditions and the following disclaimer.
 !  * Redistributions in binary form must reproduce the above copyright notice,
 !    this list of conditions and the following disclaimer in the documentation
 !    and/or other materials provided with the distribution.
 !  * Neither the name of Intel Corporation nor the names of its contributors
 !    may be used to endorse or promote products derived from this software
 !    without specific prior written permission.
 !
 ! THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS "AS IS"
 ! AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE
 ! IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE
 ! ARE DISCLAIMED. IN NO EVENT SHALL THE COPYRIGHT OWNER OR CONTRIBUTORS BE
 ! LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR
 ! CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF
 ! SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR PROFITS; OR BUSINESS
 ! INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER IN
 ! CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE)
 ! ARISING IN ANY WAY OUT OF THE USE OF THIS SOFTWARE, EVEN IF ADVISED OF THE
 ! POSSIBILITY OF SUCH DAMAGE.
 !-->

This chapter gives step-by-step instructions for building the library and the
sample tools using cmake.  For detailed information on cmake, see
http://www.cmake.org.


## Configuration

Besides the standard cmake options of build type and install directory, you will
find project-specific options for enabling optional features, optional
components, or optional build variants.


### Optional Features

Features are enabled by setting the respective FEATURE_<name> cmake variable.
This causes the FEATURE_<name> pre-processor macro to be defined and may also
cause additional source files to be compiled and additional libraries to be
linked.

The following features are supported:

    FEATURE_MMAP        Support for mapping files into memory.

                        This feature is not available on Windows.


### Build Variants

Some build variants depend on libraries or header files that may not be
available on all supported platforms.

    GCOV                Support for code coverage using libgcov.

                        This build variant requires libgcov and is not availble
                        on Windows.


    DEVBUILD            Enable compiler warnings and turn them into errors.


### Version Settings

The major and minor version numbers are set in the sources and must be changed
there.  You can set the build number and an arbitrary extension string.
build.

    PT_VERSION_BUILD    The build number.

                        Defaults to zero.


    PT_VERSION_EXT      An arbitrary version extension string.

                        Defaults to the empty string.


## Building on Linux``*`` and OS X``*``

We recommend out-of-tree builds.  Start by creating the destination directory
and navigating into it:

    $ mkdir -p /path/to/dest
    $ cd /path/to/dest


From here, call cmake with the top-level source directory as argument.  You may
already pass some or all of the cmake variables as arguments to cmake.  Without
arguments, cmake uses default values.

    $ cmake /path/to/src


To change the configuration use:

    $ make edit_cache


After configuring the cmake cache, you can build either specific targets or
everything using one of:

    $ make <target>
    $ make


Use the help make target to learn about available make targets:

    $ make help



## Building on Windows``*``

We recommend using the cmake GUI.  After starting the cmake GUI, fill in the
following fields:

    Where is the source code:       Path to the top-level source directory.

    Where to build the binaries:    Path to the destination directory.


We recommend out-of-tree builds, so the build directory should not be the same
as or below the source directory.  After this first configuration step, press
the

    Configure

button and select the builder you want to use.

Cmake will now populate the remainder of the window with configuration options.
After completing the configuration, press the

    Generate

button.  If you selected a Visual Studio generator in the first step, cmake will
now generate a Visual Studio solution.  You can repeat this step if you want to
change the configuration later on.  Beware that you always need to press the
Generate button after changing the configuration.

In the case of a Visual Studio generator, you may now open the generated Visual
Studio solution and build the library and samples.

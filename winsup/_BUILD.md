# How do I build Cygwin on my own?

First, you need to make sure you have the necessary build tools installed;
you at least need gcc-g++, make, perl, cocom, gettext-devel, libiconv-devel and zlib-devel.

Building for 32-bit Cygwin also requires mingw64-x86_64-gcc-core (for building the cyglsa64 DLL for WoW64),
mingw64-i686-gcc-g++ and mingw64-i686-zlib.

Building for 64-bit Cygwin also requires mingw64-x86_64-gcc-g++ and mingw64-x86_64-zlib.

If you want to run the tests, dejagnu is also required. Normally, building ignores any errors in building the documentation,
which requires the dblatex, docbook2X, docbook-xml45, docbook-xsl, and xmlto packages.

For more information on building the documentation, see the README included in the cygwin-doc package.

Next, get the Cygwin source. Ideally, you should check out what you need from Git (https://cygwin.com/git.html).
This is the preferred method for acquiring the sources. Otherwise, if you are trying to duplicate a cygwin release
then you should download the corresponding source package (cygwin-x.y.z-n-src.tar.bz2).

You must build cygwin in a separate directory from the source, so create something like a build/ directory.
Assuming you checked out the source in /oss/src/, and you also want to install to the temporary location install:

    mkdir /oss/build
    mkdir /oss/install 
    cd build
    (/oss/src/configure --prefix=/oss/install -v; make) >& make.out
    make install > install.log 2>&1

If the build works, install everything except the dll (if you can).
Then, close down all cygwin programs (including bash windows, inetd, etc.),
save your old dll, and copy the new dll to the correct place.
Then start up a bash window, or run a cygwin program from the Windows command prompt, and see what happens.

If you get the error "shared region is corrupted" it means that two different versions of cygwin1.dll
are running on your machine at the same time. Remove all but one.

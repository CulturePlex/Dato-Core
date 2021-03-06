Dato Core
=========

Introduction
------------
Dato Core is the open source piece of GraphLab Create, a Python-based machine
learning platform that enables data scientists and app developers to easily
create intelligent apps at scale: from prototype to production. 
 
For more details on the GraphLab Create see http://dato.com, including
documentation, tutorials, etc.

The Dato Open Source project provides the complete implementation for 
 - SFrame v1 and v2 format reader and writers
 - SFrame query evaluator
 - SGraph 
 - Graph Analytics implementations 
 - The implementations of the C++ SDK surface area (gl_sframe, gl_sarray,
     gl_sgraph)

Included within the release are also a large number of utility code such as:
 - Sketch implementations
 - Serialization
 - flexible_type (efficient runtime typed object)
 - C++ interprocess communication library (used for C++ <--> Python
     communication)
 - PowerGraph's RPC implementation

License
-------
GNU Affero General Public License. See [license](LICENSE).

Open Source Commitment
----------------------
We will keep the open sourced components up to date with the latest released
version of GraphLab Create by issuing a large "version update" pull request
with every new version of GraphLab Create.

Source Stability
----------------
The utility code is generally stable and will not change significantly over
time. The SFrame v1 and v2 formats are considered stable. A v3 format is in
the works to introduce greater compression and performance. The query evaluator
is in the midst of a complete rearchitecting. 

Dependencies
------------
GraphLab Create now automatically satisfied most dependencies. 
There are however, a few dependencies which we cannot easily satisfy:

* On OS X: Apple XCode 6 Command Line Tools [Required]
  +  Required for compiling GraphLab Create.

* On Linux: g++ (>= 4.8) or clang (>= 3.4) [Required]
  +  Required for compiling GraphLab Create.

* *nix build tools: patch, make [Required]
   +  Should come with most Mac/Linux systems by default. Recent Ubuntu version
   will require to install the build-essential package.

* cython [Required]
   +  For compilation of GraphLab Create

* zlib [Required]
   +   Comes with most Mac/Linux systems by default. Recent Ubuntu version will
   require the zlib1g-dev package.

* JDK 6 or greater [Optional]
   + Required for HDFS support 

* Open MPI or MPICH2 [Optional]
   + Required only for the RPC library inherited from PowerGraph

### Satisfying Dependencies on Mac OS X

Install XCode 6 with the command line tools.


### Satisfying Dependencies on Ubuntu

In Ubuntu >= 12.10, you can satisfy the dependencies with:
All the dependencies can be satisfied from the repository:

    sudo apt-get install gcc g++ build-essential libopenmpi-dev default-jdk cmake zlib1g-dev 

For Ubuntu versions prior to 12.10, you will need to install a newer version of gcc

    sudo add-apt-repository ppa:ubuntu-toolchain-r/test
    sudo apt-get update
    sudo apt-get install gcc-4.8 g++-4.8 build-essential libopenmpi-dev default-jdk cmake zlib1g-dev
    #redirect gcc to point to gcc-4.8
    sudo rm /usr/bin/gcc
    sudo ln -s /usr/bin/gcc-4.8 /usr/bin/gcc
    #redirect g++ to point to g++-4.8
    sudo rm /usr/bin/g++
    sudo ln -s /usr/bin/g++-4.8 /usr/bin/g++

    
Compiling
---------

    ./configure

Running configure will create two sub-directories, release/ and debug/ . cd
into src/unity/ under either of these directories and running make will build
the release or the debug versions respectively. 

We recommend using make's parallel build feature to accelerate the compilation
process. For instance:

    make -j 4

will perform up to 4 build tasks in parallel. When building in release/ mode,
GraphLab Create does require a large amount of memory to compile with the
heaviest toolkit requiring 1GB of RAM. Where K is the amount of memory you
have on your machine in GB, we recommend not exceeding make -j K

To generate the python, cd one directory further into the python directory and
run make again.

To use your dev build export these environment variables:
export PYTHONPATH="<repo root>/debug/src/unity/python/"
export GRAPHLAB_UNITY="<repo root>/debug/src/unity/server/unity_server"
where <repo root> is replace with the absolute path to the root of your repository.

Running Unit Tests
------------------

### Running Python unit tests
From the repo root:

    cd debug/src/unity/python/graphlab/test
    nosetests


### Running C++ units
From the repo root:

    cd debug/test
    make
    ctest

  
Writing Your Own Apps
---------------------

See: https://github.com/dato-code/GraphLab-Create-SDK


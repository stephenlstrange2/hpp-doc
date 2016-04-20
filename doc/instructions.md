##Installation on ubuntu-14.04 64 bit with ros-indigo

To install all the packages on ubuntu 14.04 LTS 64 bit, you should do the following steps:

  1. install ROS-indigo: follow steps 1.1 to 1.3 of the [ROS installation website](http://wiki.ros.org/indigo/Installation/Ubuntu).

  2. install by apt-get
    - autoconf
    - g++
    - cmake
    - libboost-dev
    - liburdfdom-dev
    - libassimp-dev
    - ros-indigo-xacro
    - ros-indigo-kdl-parser
    - ros-indigo-common-msgs
    - ros-indigo-tf
    - ros-indigo-tf-conversions
    - ros-indigo-libccd
    - ros-indigo-octomap
    - ros-indigo-resource-retriever
    - ros-indigo-urdfdom-py
    - ros-indigo-srdfdom
    - ros-indigo-pr2-robot
    - flex
    - bison
    - asciidoc
    - source-highlight
    - git
    - libomniorb4-dev
    - omniorb-nameserver
    - omniidl
    - omniidl-python
    - libltdl-dev
    - python-matplotlib
    - libtinyxml2-dev
    - liblog4cxx10-dev
    - libltdl-dev
    - qt4-dev-tools
    - libqt4-opengl-dev
    - libqtgui4
    - oxygen-icon-theme
    - subversion
    - graphviz-dev

    ```bash
sudo apt-get install autoconf g++ cmake libboost-dev liburdfdom-dev libassimp-dev ros-indigo-xacro ros-indigo-kdl-parser ros-indigo-common-msgs ros-indigo-tf ros-indigo-tf-conversions ros-indigo-libccd ros-indigo-octomap ros-indigo-resource-retriever ros-indigo-srdfdom ros-indigo-pr2-robot flex bison asciidoc source-highlight git libomniorb4-dev omniorb-nameserver omniidl omniidl-python libltdl-dev python-matplotlib libtinyxml2-dev liblog4cxx10-dev libltdl-dev qt4-dev-tools libqt4-opengl-dev libqtgui4 oxygen-icon-theme subversion graphviz-dev
    ```

  2. install dependencies of openscenegraph:

    ```bash
sudo apt-get build-dep openscenegraph
    ```

  3. Choose a directory on you file system and define the environment
     variable `DEVEL_DIR` with the full path to this directory.
     - the packages will be cloned into `$DEVEL_DIR/src`,
     - the packages will be installed in `$DEVEL_DIR/install`.
     It is recommanded to set variable `DEVEL_DIR` in your `.bashrc` for future use.

  4. Copy Config and Makefile

    ```bash
wget -O $DEVEL_DIR/config.sh https://raw.githubusercontent.com/humanoid-path-planner/hpp-doc/euroc-c1/doc/config.sh
wget -O $DEVEL_DIR/src/Makefile https://raw.githubusercontent.com/humanoid-path-planner/hpp-doc/euroc-c1/doc/Makefile
    ```

  5. cd into `$DEVEL_DIR` and type

    ```bash
cd $DEVEL_DIR
source config.sh
    ```

  6. cd into `$DEVEL_DIR/src` and type

    ```bash
cd $DEVEL_DIR/src
make robot_state_chain_publisher.install;
source ../config.sh;
make all
    ```

  Note that all packages are built in RELEASE mode as default. In order to efficiently
  debug individual packages, go into the `build/` directory of any given package and type

    ```bash
ccmake ..
    ```

  Change the `CMAKE_BUILD_TYPE` flag from RELEASE to DEBUG, and configure the change.
  Building the package will now be done in DEBUG mode. Please note that running
  packages that have been built in DEBUG mode may drastically increase computational
  time.


##Documentation

  Open `$DEVEL_DIR/install/share/doc/hpp-doc/index.html` in a web brower and you
  will have access to the documentation of most packages.

  Click on tutotial in the left panel to start learning about the software.

##Trouble Shooting

  Here are a few common issues and solutions to solve them

  1. At configuration, the following message appears:

    ```bash
CMake Error at CMakeLists.txt:25 (INCLUDE):
include could not find load file:
  cmake/base.cmake
    ```

    *Solution*: Each package comes with a git submodule checked out in a directory
    called `cmake` at the root of the package. The `--recursive` directive of
    `git clone` is meant to check out this submodule. For some network
    configurations however, the cmake module is not checked out. One solution
    is to request git to use https protocol by typing the following command:

    ```bash
git config --global url."https://".insteadOf git://
    ```
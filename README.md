# Jetson setup

This repository helps setup your Jetson TK1 to to make great things with maximum power. First you need to flash Jetson with the newest Jetpack software. After a boot, we need to provide the system with some packages:

```sh
$ sudo apt-add-repository universe
$ sudo apt-get update
$ sudo apt-get upgrade
$ sudo apt-get install bash-completion command-not-found git nano cmake cmake-curses-gui autoconf libtool libconfig-dev ncurses-dev qtcreator linux-firmware build-essential gnome-devel libgtk-3-dev 
```

To fix qtcreator bug:

```sh
$ sudo apt-get remove appmenu-qt5
```

Setup the locales by first adding those lines to ~/.bashrc file:

```sh
# LOCALES
export LANGUAGE=en_US.UTF-8
export LANG=en_US.UTF-8
export LC_ALL=en_US.UTF-8
```

And then updating the locales:

```sh
$ locale-gen en_US.UTF-8
$ dpkg-reconfigure locales
```

Next, install ROS indigo (bare bones). The precompiled versions of the ROS image_pipeline and vision_opencv packages from the deb repo are built against standard Ubuntu versions of OpenCV, and can't (or shouldn't) be used with CV for Tegra. So in the top level ros workspace you should build vision_opencv, image_pipeline and image_common from source:

```sh
mkdir -p pioneer_ws/src
cd pioneer_ws/src
catkin_init_workspace
git clone https://github.com/ros-perception/vision_opencv
cd vision_opencv
git checkout indigo
cd ..
git clone https://github.com/ros-perception/image_pipeline
cd image_pipeline
git checkout indigo
cd ..
git clone https://github.com/ros-perception/image_common
cd ..
catkin_make
```

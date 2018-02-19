COLMAP SFM LIBRARY ON JETSON TX2
=================================
This repository allows to compile the COLMAP SFM Library on a Jetson TX2. Modifications to the source code have been done to be able to be able to sucucessfully compile the library on the Jetson Nvidia.


About
-----

COLMAP is a general-purpose Structure-from-Motion (SfM) and Multi-View Stereo
(MVS) pipeline with a graphical and command-line interface. It offers a wide
range of features for reconstruction of ordered and unordered image collections.
The software is licensed under the GNU General Public License. If you use this
project for your research, please cite:

    @inproceedings{schoenberger2016sfm,
        author = {Sch\"{o}nberger, Johannes Lutz and Frahm, Jan-Michael},
        title = {Structure-from-Motion Revisited},
        booktitle={IEEE Conference on Computer Vision and Pattern Recognition (CVPR)},
        year={2016},
    }

    @inproceedings{schoenberger2016mvs,
        author = {Sch\"{o}nberger, Johannes Lutz and Zheng, Enliang and Pollefeys, Marc and Frahm, Jan-Michael},
        title = {Pixelwise View Selection for Unstructured Multi-View Stereo},
        booktitle={European Conference on Computer Vision (ECCV)},
        year={2016},
    }
Installation on Jetson TX2
--------------------------
Jetson TX2 needs to be flashed 
Install latest JetPack to flash the Jetson TX2 https://developer.nvidia.com/embedded/jetpack

Install Dependencies from default Ubuntu repositories:

sudo apt-get install \
    cmake \
    build-essential \
    libboost-all-dev \
    libeigen3-dev \
    libsuitesparse-dev \
    libfreeimage-dev \
    libgoogle-glog-dev \
    libgflags-dev \
    libglew-dev \
    qtbase5-dev \
    libqt5opengl5-dev
    
Install Ceres Solver
---------------------
sudo apt-get install libatlas-base-dev libsuitesparse-dev

git clone https://ceres-solver.googlesource.com/ceres-solver

cd ceres-solver

mkdir build

cd build

cmake .. -DBUILD_TESTING=OFF -DBUILD_EXAMPLES=OFF

make

sudo make install

Configure and compile COLMAP
-----------------------------
cd path/to/colmap

mkdir build

cd build

cmake ..

make

sudo make install

Run COLMAP:

colmap -h

colmap gui


Results on Jetson TX2
---------------------

Results obtained when processing COLMAP on the KITTI benchmark dataset on Jetson TX2

[//]: # (Image References)
[image_0]: ./Results/kitti_result.png

![alt text][image_0] 

License
-------

The software is licensed under the GNU General Public License v3 or later. If
you are interested in licensing the software for commercial purposes, without
disclosing your modifications, please contact the authors.

    COLMAP - Structure-from-Motion and Multi-View Stereo.
    Copyright (C) 2017  Johannes L. Schoenberger <jsch at inf.ethz.ch>

    This program is free software: you can redistribute it and/or modify
    it under the terms of the GNU General Public License as published by
    the Free Software Foundation, either version 3 of the License, or
    (at your option) any later version.

    This program is distributed in the hope that it will be useful,
    but WITHOUT ANY WARRANTY; without even the implied warranty of
    MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
    GNU General Public License for more details.

    You should have received a copy of the GNU General Public License
    along with this program.  If not, see <http://www.gnu.org/licenses/>.

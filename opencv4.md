
CentOS 7

sudo yum install epel-release git gcc gcc-c++ cmake3 qt5-qtbase-devel python python-devel python-pip cmake

sudo yum install python-devel numpy python34-numpy gtk2-devel libpng-devel jasper-devel openexr-devel libwebp-devel

sudo yum install libjpeg-turbo-devel libtiff-devel  libdc1394-devel tbb-devel eigen3-devel gstreamer-plugins-base-devel

sudo yum install freeglut-devel mesa-libGL mesa-libGL-devel  boost boost-thread boost-devel libv4l-devel

Download opencv, opencv_contrib, opencv_extra

cd ~/opencv_build/opencv && mkdir build && cd build

cmake3 -DCMAKE_BUILD_TYPE=RELEASE \
    -DCMAKE_INSTALL_PREFIX=/usr/local \
    -DINSTALL_C_EXAMPLES=ON \
    -DINSTALL_PYTHON_EXAMPLES=ON \
    -DOPENCV_GENERATE_PKGCONFIG=ON \
    -DOPENCV_TEST_DATA_PATH=~/opencv_build/opencv_extra/testdata \
    -DBUILD_EXAMPLES=ON \
    -DBUILD_DOCS=ON  \
    ..


cmake3 -DCMAKE_BUILD_TYPE=RELEASE \
    -DCMAKE_INSTALL_PREFIX=/usr/local \
    -DINSTALL_C_EXAMPLES=ON \
    -DINSTALL_PYTHON_EXAMPLES=ON \
    -DOPENCV_GENERATE_PKGCONFIG=ON \
    -DOPENCV_EXTRA_MODULES_PATH=~/opencv_build/opencv_contrib/modules \
    -DOPENCV_TEST_DATA_PATH=~/opencv_build/opencv_extra/testdata \
    -DBUILD_EXAMPLES=ON \
    -DBUILD_DOCS=ON  \
    -DWITH_IPP=OFF \
    ..

cmake -DBUILD_DOCS=ON -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX=/usr/local ..

make -j8
make -j$(nproc)
sudo make install


sudo ln -s /usr/local/lib/python2.7/site-packages/cv2  /usr/lib/python2.7/site-packages/
sudo ln -s /usr/local/lib64/pkgconfig/opencv4.pc /usr/share/pkgconfig/
sudo ldconfig

pkg-config --modversion opencv4
pkg-config --cflags opencv4
pkg-config --libs opencv

ipython
import cv2
print(cv2.__version__)



mkdir foo 
CMakeLists.txt
cmake_minimum_required(VERSION 2.8)
project( DisplayImage )
find_package( OpenCV REQUIRED )
include_directories( ${OpenCV_INCLUDE_DIRS} )
add_executable( DisplayImage helloworld.cxx )
target_link_libraries( DisplayImage ${OpenCV_LIBS} )

helloworld.cxx
#include <opencv2/opencv.hpp>
using namespace cv;
int main ( int argc, char **argv )
{
  Mat img(480, 640, CV_8U);
  putText(img, "Hello World!", Point( 200, 400 ), FONT_HERSHEY_SIMPLEX | FONT_ITALIC, 1.0, Scalar( 255, 255, 0 ));
  imshow("My Window", img);
  waitKey();
  return 0;
}


mkdir build
cmake -DCMAKE_BUILD_TYPE=DEBUG -DCMAKE_CXX_FLAGS="-std=c++11" ../foo


IDE import cmake-project(~/build), Linux GCC
C++ General/Paths/includes/ add /usr/local/include/opencv4
Debug




$ sudo alternatives --install /usr/local/bin/cmake cmake /usr/bin/cmake 10 \
--slave /usr/local/bin/ctest ctest /usr/bin/ctest \
--slave /usr/local/bin/cpack cpack /usr/bin/cpack \
--slave /usr/local/bin/ccmake ccmake /usr/bin/ccmake \
--family cmake

$ sudo alternatives --install /usr/local/bin/cmake cmake /usr/bin/cmake3 20 \
--slave /usr/local/bin/ctest ctest /usr/bin/ctest3 \
--slave /usr/local/bin/cpack cpack /usr/bin/cpack3 \
--slave /usr/local/bin/ccmake ccmake /usr/bin/ccmake3 \
--family cmake

$ sudo alternatives --install /usr/local/bin/cmake-gui cmake-gui /usr/bin/cmake-gui 10 \
--family cmake-gui

$ sudo alternatives --install /usr/local/bin/cmake-gui cmake-gui /usr/bin/cmake3-gui 20 \
--family cmake-gui

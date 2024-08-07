# ROS wrapper CMake project for these MRPT libraries:
# mrpt-obs, mrpt-topography

cmake_minimum_required(VERSION 3.5)
project(mrpt_obs)

include(ExternalProject)

ExternalProject_Add(
  mrpt
  PREFIX ${CMAKE_BINARY_DIR}/mrpt-build
  SOURCE_DIR ${CMAKE_CURRENT_SOURCE_DIR}/../upstream/
  CMAKE_ARGS 
    # Main settings:
    -DCMAKE_INSTALL_PREFIX=${CMAKE_INSTALL_PREFIX}
    -DCMAKE_BUILD_TYPE=${CMAKE_BUILD_TYPE}
    # Disabled stuff:
    -DDISABLE_JSONCPP=ON
    -DMRPT_INSTALL_EXAMPLES=OFF
    -DMRPT_INSTALL_SHARE_DIRS=OFF
    -DMRPT_BUILD_MANPAGES=OFF
    -DMRPT_INSTALL_CONFIG_HEADERS=OFF
    -DDISABLE_ROS=ON # save cmake configure time
    # Granular builds for each ROS package:
    -DMRPT_BUILD_APPLICATIONS=OFF
    -DMRPT_DISABLE_PYTHON_BINDINGS=ON
    -DMRPT_WITH_ROBOPEAK_LIDAR=OFF
    -DMRPT_BUILD_wxThings=OFF
    -DMRPT_BUILD_rplidar_sdk=OFF
    -DMRPT_BUILD_xsens=OFF
    -DMRPT_BUILD_nanogui=OFF
    # Libs:
    -DBUILD_mrpt-apps=OFF
    -DBUILD_mrpt-bayes=OFF
    -DBUILD_mrpt-comms=OFF
    -DBUILD_mrpt-config=OFF
    -DBUILD_mrpt-containers=OFF
    -DBUILD_mrpt-core=OFF
    -DBUILD_mrpt-expr=OFF
    -DBUILD_mrpt-graphs=OFF
    -DBUILD_mrpt-graphslam=OFF
    -DBUILD_mrpt-gui=OFF
    -DBUILD_mrpt-hwdrivers=OFF
    -DBUILD_mrpt-img=OFF
    -DBUILD_mrpt-io=OFF
    -DBUILD_mrpt-kinematics=OFF
    -DBUILD_mrpt-maps=OFF
    -DBUILD_mrpt-math=OFF
    -DBUILD_mrpt-nav=OFF
    -DBUILD_mrpt-obs=ON
    -DBUILD_mrpt-opengl=OFF
    -DBUILD_mrpt-poses=OFF
    -DBUILD_mrpt-random=OFF
#    -DBUILD_mrpt-ros2bridge=OFF
    -DBUILD_mrpt-rtti=OFF
    -DBUILD_mrpt-serialization=OFF
    -DBUILD_mrpt-slam=OFF
    -DBUILD_mrpt-system=OFF
    -DBUILD_mrpt-tclap=OFF
    -DBUILD_mrpt-tfest=OFF
    -DBUILD_mrpt-topography=ON
    -DBUILD_mrpt-typemeta=OFF
    -DBUILD_mrpt-vision=OFF
  # no install during build
  INSTALL_COMMAND ""
)

# Actual "install":
install(CODE "execute_process(COMMAND ${CMAKE_COMMAND} --build ${CMAKE_BINARY_DIR}/mrpt-build/src/mrpt-build --target install)")

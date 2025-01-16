##########################################################################################
# Dockerfile for building mysql-server-timeseries on Oracle Linux 9
##########################################################################################

FROM library/oraclelinux:9

LABEL org.opencontainers.image.authors="bplougonven@infovista.com"
LABEL org.opencontainers.image.description="Builder image for MySQL / Sparrow based on Oracle Linux 9 latest version"

RUN echo INSTALLING 64 BITS TOOLS AND LIBRARIES; \
    yum install -q -y gcc gcc-c++.x86_64 glibc-devel.x86_64; \
    yum install -q -y libaio-devel libudev-devel ncurses-devel.x86_64 bison.x86_64; \
    yum install -q -y gcc-toolset-12-gcc gcc-toolset-12-gcc-c++ gcc-toolset-12-binutils gcc-toolset-12-annobin-annocheck gcc-toolset-12-annobin-plugin-gcc; \
    echo INSTALLING RPCGEN; \
    yum install -q -y rpcgen; \
    echo INSTALLING WGET, ZIP, UNZIP AND TAR; \
    yum install -q -y wget tar zip unzip; \
    yum install -q -y make; \
    echo INSTALLING MISC TOOLS; \
    yum install -q -y dos2unix which file hostname; \
    echo INSTALLING PERL; \
    yum install -q -y perl; \
    echo INSTALLING CMAKE; \
    cd /tmp;  \
    wget -O /tmp/cmake.sh  -nv  https://github.com/Kitware/CMake/releases/download/v3.23.1/cmake-3.23.1-linux-x86_64.sh; \
    chmod a+x cmake.sh; \
    mkdir -p /opt/cmake; \
    ./cmake.sh --skip-license --prefix=/opt/cmake; \
    rm -f cmake-3.23.1-linux-x86_64.sh; \
    echo INSTALLING LATEST PYTHON 3.X REQUIRED FOR CONAN; \
    yum install -q -y python3 python3-pip; \
    echo INSTALLING CONAN; \
    pip3 install conan==1.65.0; \
    echo CONFIGURING CONAN VERSION `conan --version`; \
    mkdir -p /data/conan/packages; \
    conan config set storage.path=/data/conan/packages; \
    conan profile new default --detect; \
    conan profile update settings.compiler.libcxx=libstdc++11 default; \
    yum -q clean all; \
    echo PREPARING SHARED VOLUMES; \
    mkdir -p /data/source;

# Set timezone
ENV TZ Europe/Paris

ENV CMAKE_HOME=/opt/cmake
ENV PATH=$PATH:${CMAKE_HOME}/bin

ENTRYPOINT ["bash"]

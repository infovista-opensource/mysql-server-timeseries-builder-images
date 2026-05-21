##########################################################################################
# Dockerfile for building mysql-server-timeseries 8.4 on Oracle Linux 9
##########################################################################################

FROM library/oraclelinux:9

LABEL org.opencontainers.image.authors="bplougonven@infovista.com"
LABEL org.opencontainers.image.description="Builder image for MySQL Timeseries Server 8.4 based on Oracle Linux 9 latest version"

RUN echo INSTALLING 64 BITS TOOLS AND LIBRARIES; \
    yum install -q -y gcc gcc-c++.x86_64 glibc-devel.x86_64; \
    yum install -q -y libaio-devel libudev-devel ncurses-devel.x86_64 bison.x86_64; \
    yum install -q -y gcc-toolset-12-gcc gcc-toolset-12-gcc-c++ gcc-toolset-12-binutils gcc-toolset-12-annobin-annocheck gcc-toolset-12-annobin-plugin-gcc; \
    echo INSTALLING libtirpc-devel; \
    dnf --enablerepo=ol9_codeready_builder install libtirpc-devel; \
    echo INSTALLING RPCGEN; \
    yum install -q -y rpcgen; \
    echo INSTALLING WGET, ZIP, UNZIP AND TAR; \
    yum install -q -y wget tar zip unzip; \
    yum install -q -y make; \
    echo INSTALLING OPENSSL DEVELOPMENT PACKAGE; \
    yum install -q -y openssl-devel; \
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
    yum -q clean all; \
    echo PREPARING SHARED VOLUMES; \
    mkdir -p /data/source;

# Set timezone
ENV TZ Europe/Paris

ENV CMAKE_HOME=/opt/cmake
ENV PATH=$PATH:${CMAKE_HOME}/bin

ENTRYPOINT ["bash"]

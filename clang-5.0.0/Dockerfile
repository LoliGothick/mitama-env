FROM ubuntu:bionic

RUN buildDeps='gpg-agent wget xz-utils subversion' && \
    apt-get update -y && \
    apt-get -qq install -y --no-install-recommends gcc g++ make ca-certificates build-essential libtool libstdc++5 $buildDeps && \
    apt-get install -y --reinstall binutils && \
    wget https://github.com/Kitware/CMake/releases/download/v3.13.3/cmake-3.13.3.tar.gz && \
    tar xvf ./cmake-3.13.3.tar.gz && \
    cd cmake-3.13.3 && ./bootstrap && make && make install && cd .. && \
    wget http://releases.llvm.org/5.0.0/clang+llvm-5.0.0-linux-x86_64-ubuntu16.04.tar.xz && \
    tar xvf ./clang+llvm-5.0.0-linux-x86_64-ubuntu16.04.tar.xz && \
    cp -r clang+llvm-5.0.0-linux-x86_64-ubuntu16.04/*/ /usr/ && \
    wget https://dl.bintray.com/boostorg/release/1.67.0/source/boost_1_67_0.tar.gz && \
    tar xvf ./boost_1_67_0.tar.gz && \
    cd boost_1_67_0 && \
    ./bootstrap.sh && \
    ./b2 install -j5 --cxxflags='-std=c++17 -stdlib=libc++' && cd .. && \
    rm ./boost_1_67_0.tar.gz ./clang+llvm-5.0.0-x86_64-linux-gnu-ubuntu-16.04.tar.xz ./cmake-3.13.3.tar.gz && \
    rm -rf clang+llvm-5.0.0-x86_64-linux-gnu-ubuntu-16.04 cmake-3.13.3 boost_1_67_0 && \
    apt-get remove $buildDeps -y && \
    apt-get -qq purge --auto-remove -y git && \
    rm -rf /var/lib/apt/lists/*

ENV CC='clang' \
    CXX='clang++'

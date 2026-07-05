FROM pytorch/manylinux2_28_aarch64-builder:cpu-aarch64-v2.13.0-rc15

RUN wget https://cmake.org/files/v3.28/cmake-3.28.6-linux-aarch64.tar.gz

RUN tar zxf /cmake-3.28.6-linux-aarch64.tar.gz

ARG VERSION

RUN git clone -b v$VERSION https://github.com/grpc/grpc

WORKDIR /grpc
RUN git submodule update --init

RUN sed -i '/add_subdirectory/iset(BUILD_SHARED_LIBS OFF)' cmake/abseil-cpp.cmake
RUN sed -i '/add_subdirectory/aset(BUILD_SHARED_LIBS ON)' cmake/abseil-cpp.cmake
RUN sed -i '/add_library(address_sorting/aSTATIC' CMakeLists.txt
RUN sed -i '/add_library(upb/aSTATIC' CMakeLists.txt
RUN sed -i '/add_library(upb_base_lib/aSTATIC' CMakeLists.txt
RUN sed -i '/add_library(upb_json_lib/aSTATIC' CMakeLists.txt
RUN sed -i '/add_library(upb_mem_lib/aSTATIC' CMakeLists.txt
RUN sed -i '/add_library(upb_message_lib/aSTATIC' CMakeLists.txt
RUN sed -i '/add_library(upb_textformat_lib/aSTATIC' CMakeLists.txt
RUN sed -i '/add_library(utf8_range_lib/aSTATIC' CMakeLists.txt

RUN mkdir -p /grpc/build
WORKDIR /grpc/build
RUN /cmake-3.28.6-linux-aarch64/bin/cmake -DBUILD_SHARED_LIBS=ON -DgRPC_SSL_PROVIDER=package -DgRPC_ZLIB_PROVIDER=package -DCMAKE_BUILD_TYPE=Release -DgRPC_BUILD_TESTS=OFF ..
RUN make install
WORKDIR /
RUN rm -rf /grpc
RUN rm -rf /cmake-3.28.6-linux-aarch64.tar.gz
RUN rm -rf /cmake-3.28.6-linux-aarch64

FROM pytorch/manylinux2_28_aarch64-builder:cpu-aarch64-v2.13.0-rc15

ARG VERSION

RUN git clone -b v$VERSION https://github.com/grpc/grpc

WORKDIR /grpc
RUN git submodule update --init

RUN mkdir -p /grpc/build
WORKDIR /grpc/build
RUN cmake -DBUILD_SHARED_LIBS=ON -DgRPC_SSL_PROVIDER=package -DgRPC_ZLIB_PROVIDER=package -DCMAKE_BUILD_TYPE=Release -DgRPC_BUILD_TESTS=OFF ..
RUN make install
WORKDIR /
RUN rm -rf /grpc

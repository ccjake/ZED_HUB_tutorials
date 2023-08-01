ARG BUILD_IMAGE
ARG RUNTIME_IMAGE
FROM ${BUILD_IMAGE} as builder

## Compilation of the app
COPY ./sources/src /home/src
COPY ./sources/CMakeLists.txt /home

WORKDIR /home
RUN mkdir build
WORKDIR /home/build
RUN cmake -DCMAKE_LIBRARY_PATH="/usr/local/cuda/lib64/stubs;/usr/local/cuda/lib64/stubs_" -DCMAKE_CXX_FLAGS="-Wl,--allow-shlib-undefined" .. && \
make -j8 && mv ZED_Hub_Tutorial_2 /
WORKDIR /

## Output part -- send files out of docker context
ARG RUNTIME_IMAGE
FROM ${RUNTIME_IMAGE}

#Copy your binary
COPY --from=builder /ZED_Hub_Tutorial_2 ./

CMD ["/ZED_Hub_Tutorial_2"]

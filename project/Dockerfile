#This dockerfile for production
FROM gcc:latest

#set environment variables
ARG CMAKE_VERSION

#install cmake required version
RUN apt-get update && apt-get install -y cmake vim
COPY ./scripts/reinstall-cmake.sh /tmp/
RUN if [ "${CMAKE_VERSION}" != "none" ]; then \
    chmod +x /tmp/reinstall-cmake.sh && /tmp/reinstall-cmake.sh ${CMAKE_VERSION}; \
    fi \
    && rm -f /tmp/reinstall-cmake.sh

COPY project /root/code

#install cpp extensions
# RUN apt-get install -y clangd, lldb
# RUN ln -s /usr/lib/llvm-14/lib/python3.11/dist-packages/lldb/* /usr/lib/python3/dist-packages/lldb/

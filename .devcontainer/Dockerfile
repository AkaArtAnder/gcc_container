FROM gcc:13.2.0

#set environment variables
ARG CMAKE_VERSION
ARG UID
ARG GID
ARG USER_PASSWORD
ARG USER_NAME
ARG DEV_FOLDER
ARG SSH_HOST
ARG SSH_KEY_NAME

#install cmake required version
RUN apt-get update && apt-get install -y cmake vim sudo bash-completion tmux pipx ninja-build
COPY .devcontainer/scripts/reinstall-cmake.sh /tmp/
RUN if [ "${CMAKE_VERSION}" != "none" ]; then \
  chmod +x /tmp/reinstall-cmake.sh && /tmp/reinstall-cmake.sh ${CMAKE_VERSION}; \
  fi \
  && rm -f /tmp/reinstall-cmake.sh

#install cpp extensions
RUN apt-get install -y lsb-release wget software-properties-common gnupg
RUN apt-add-repository 'deb http://apt.llvm.org/bookworm/ llvm-toolchain-bookworm-17 main'
RUN apt-add-repository 'deb-src http://apt.llvm.org/bookworm/ llvm-toolchain-bookworm-17 main'
WORKDIR /root
RUN wget https://apt.llvm.org/llvm.sh && chmod +x llvm.sh && ./llvm.sh all


#Up ssh server if not used vscode
RUN sudo apt-get install -y openssh-server
RUN sed -i 's/#Port 22/Port 22/' /etc/ssh/sshd_config
COPY .devcontainer/scripts/run.sh .
RUN chmod +x run.sh


#make user and set own id
RUN groupadd -r ${USER_NAME} && useradd -m -s /bin/bash -g ${USER_NAME} ${USER_NAME} -G adm,cdrom,sudo
RUN echo ${USER_NAME}:${USER_PASSWORD} | chpasswd
RUN usermod -u ${UID} ${USER_NAME} \
  && groupmod -g ${GID} ${USER_NAME}

USER ${USER_NAME}

#Installing conan
RUN pipx install conan

WORKDIR /home/${USER_NAME}
RUN mkdir ${DEV_FOLDER}

COPY . ${DEV_FOLDER}

# Set git ssh key into container
# WORKDIR /home/${USER_NAME}
# RUN mkdir .ssh
# COPY .devcontainer/ssh_keys/${SSH_KEY_NAME} .ssh/id_ed25519
# USER root
# RUN chmod 777 /home/${USER_NAME}/.ssh && \
#   chmod 777 /home/${USER_NAME}/.ssh/id_ed25519 && \
#   ssh-keyscan -f /home/${USER_NAME}/.ssh/id_ed25519 -t rsa ${SSH_HOST} > /home/${USER_NAME}/.ssh/known_hosts \
#   chmod 777 /home/${USER_NAME}/.ssh/known_hosts
# end

USER root
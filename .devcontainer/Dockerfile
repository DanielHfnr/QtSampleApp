FROM qt_6_5_2:latest


ARG USERNAME=developer
ARG USER_UID=1000
ARG USER_GID=$USER_UID

RUN apt-get update
# [Optional] Add sudo support. Omit if you don't need to install software after connecting.
RUN apt-get install -y sudo

# Create the user
RUN groupadd --gid $USER_GID $USERNAME 
RUN useradd --uid $USER_UID --gid $USER_GID -m $USERNAME 
RUN echo $USERNAME ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/$USERNAME && chmod 0440 /etc/sudoers.d/$USERNAME

# Install clang-format and clang-tidy
RUN apt-get install -y clang-format clang-tidy

# [Optional] Set the default user. Omit if you want to keep the default as root.
USER $USERNAME

FROM ubuntu:22.04

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update
RUN apt-get upgrade -y

# Install some tools and qt dependencies
RUN apt-get install -y locales wget cmake git bison build-essential clang flex gperf \
			libatspi2.0-dev libbluetooth-dev libclang-dev libcups2-dev libdrm-dev \
			libegl1-mesa-dev libfontconfig1-dev libfreetype6-dev \
			libgstreamer1.0-dev libhunspell-dev libnss3-dev libopengl-dev \
			libpulse-dev libssl-dev libts-dev libx11-dev libx11-xcb-dev \
			libxcb-glx0-dev libxcb-icccm4-dev libxcb-image0-dev \
			libxcb-keysyms1-dev libxcb-randr0-dev libxcb-render-util0-dev \
			libxcb-shape0-dev libxcb-shm0-dev libxcb-sync-dev libxcb-util-dev \
			libxcb-xfixes0-dev libxcb-xinerama0-dev libxcb-xkb-dev libxcb1-dev \
			libxcomposite-dev libxcursor-dev libxdamage-dev libxext-dev \
			libxfixes-dev libxi-dev libxkbcommon-dev libxkbcommon-x11-dev \
			libxkbfile-dev libxrandr-dev libxrender-dev libxshmfence-dev \
			libxshmfence1 llvm ninja-build nodejs python-is-python3 python3\
			freeglut3-dev gdb iputils-ping libgl1-mesa-dev \
			libglu1-mesa-dev libjpeg-dev libmysqlclient-dev libopus-dev \
			libpng-dev libsqlite3-dev libxcb-xkb-dev libxml2-dev \
			libxslt-dev lzip mesa-common-dev nano perl valgrind zlib1g-dev \
			'^libxcb.*-dev' libwayland-dev libicu-dev libxslt-dev ruby \
			libxtst-dev libxss-dev libdbus-1-dev libevent-dev \
			libcap-dev libudev-dev libpci-dev libasound2-dev \
			libasound2-dev libgstreamer-plugins-base1.0-dev \
			libgstreamer-plugins-good1.0-dev libgstreamer-plugins-bad1.0-dev \
			libavformat58 libavcodec58 libavutil56 libswresample3 libswscale5 libavdevice58 \
			libmng2 libxcb-xinput0 libwebpmux3

# Reconfigure locale
RUN locale-gen en_US.UTF-8 && dpkg-reconfigure locales

# Build qt from source version 6.5.2
ENV QT_VERSION_A=6.5
ENV QT_VERSION_B=6.5.2

RUN wget https://download.qt.io/official_releases/qt/${QT_VERSION_A}/${QT_VERSION_B}/single/qt-everywhere-src-${QT_VERSION_B}.tar.xz
RUN tar xf qt-everywhere-src-${QT_VERSION_B}.tar.xz && rm qt-everywhere-src-${QT_VERSION_B}.tar.xz

# Set the working dir. All following commands will be executed from here
WORKDIR "/qt-everywhere-src-${QT_VERSION_B}"
# Configure build
RUN ./configure
# Build - this can take some time
RUN cmake --build .
# Install
RUN cmake --install .
# Build documentation
RUN cmake --build . --target docs
# Install the docs
RUN cmake --build . --target install_docs

RUN apt-get install -y qtcreator

ENV CMAKE_PREFIX_PATH=/usr/local/Qt-6.5.2

FROM registry.access.redhat.com/ubi9/python-39:1-117.1684741281

# By default, listen on port 8081
EXPOSE 8081/tcp
ENV FLASK_PORT=8081

# Set the working directory in the container
WORKDIR /projects

# Copy the content of the local src directory to the working directory
COPY . .

USER root

RUN INSTALL_PKGS="\
  bash-completion \
  bc \
  bind-utils \
  blktrace \
  crash \
  e2fsprogs \
  ethtool \
  file \
  git \
  glibc-utils \
  hwloc \
  iotop \
  iproute \
  iputils \
  less \
  ltrace \
  mailx \
  net-tools \
  netsniff-ng \
  nmap-ncat \
  numactl \
  numactl-devel \
  parted \
  pciutils \
  psmisc \
  screen \
  strace \
  sysstat \
  tcpdump \
  vim-enhanced \
  xfsprogs \
  " && yum -y install $INSTALL_PKGS && rpm -V --nosize --nofiledigest --nomtime --nomode $INSTALL_PKGS

# Install any dependencies
RUN \
  if [ -f requirements.txt ]; \
    then pip install -r requirements.txt; \
  elif [ `ls -1q *.txt | wc -l` == 1 ]; \
    then pip install -r *.txt; \
  fi

# Specify the command to run on container start
CMD [ "python", "./app.py" ]

dnf update -y
dnf upgrade -y

dnf groupinstall -y "Development Tools"

dnf install -y \
    wget \
    curl \
    git \
    vim \
    nano \
    tar \
    unzip \
    bzip2 \
    gzip \
    make \
    cmake \
    gcc \
    gcc-c++ \
    perl \
    openssl \
    openssl-devel \
    zlib-devel

    python3 \
    python3-pip \


 ### librerias de red

 dnf install -y \
    net-tools \
    openssh-server \
    openssh-clients \
    tcpdump \
    nmap \
    traceroute


    # Hadoop
$HADOOP_HOME/sbin/start-dfs.sh
$HADOOP_HOME/sbin/start-yarn.sh

# ZooKeeper
$ZK_HOME/bin/zkServer.sh start

# Spark (standalone mode)
$SPARK_HOME/sbin/start-all.sh

# Zeppelin
$ZEPPELIN_HOME/bin/zeppelin-daemon.sh start

# Hue
hue runserver

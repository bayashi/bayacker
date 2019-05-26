# 1. Container should be ephemeral.
# 2. Don't install unnecessary packages.
# 3. Each container should have only one application.
# 4. Sorting multi-line arguments alphanumerically.

FROM centos:centos6.7

MAINTAINER bayashi

ENTRYPOINT ["/bin/bash"]

WORKDIR /setup

#----- yum packages
RUN rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-6
RUN yum -y update && yum clean all

#----- yum reinstall
RUN yum reinstall -y \
    glibc-common \
&& yum clean all

#----- yum uninstall
RUN yum remove -y \
    cvs \
    hicolor-icon-theme \
&& yum clean all

#----- etc packages
RUN yum install -y \
    gcc \
    perl-core \
    tar \
    wget \
    yum-plugin-ovl \
&& yum clean all

#----- git
ENV GIT_VERSION 2.9.5
RUN yum install -y \
    curl-devel \
    expat-devel \
    gettext-devel \
    openssl-devel \
    zlib-devel \
&& yum clean all
RUN wget https://mirrors.edge.kernel.org/pub/software/scm/git/git-$GIT_VERSION.tar.gz \
&& tar zxvf git-$GIT_VERSION.tar.gz \
&& cd git-$GIT_VERSION \
&& ./configure \
&& make \
&& make install

#----- utils
RUN yum install -y \
    crontabs \
    iptables-devel \
    jq \
    jwhois \
    libxml2-devel \
    libxslt \
    libyaml \
    libyaml-devel \
    logrotate \
    lsof \
    ntp \
    ntpdate \
    patch \
    pcre-devel \
    rpm-build \
    rsync \
    screen \
    strace \
    sudo \
    tcpdump \
    telnet \
    time \
    traceroute \
    tree \
    which \
&& yum clean all

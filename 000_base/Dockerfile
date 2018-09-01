# 1. Container should be ephemeral.
# 2. Don't install unnecessary packages.
# 3. Each container should have only one application.
# 4. Sorting multi-line arguments alphanumerically.
# 5. Installing something, show version immediately

FROM centos:centos6.7

MAINTAINER bayashi

ENTRYPOINT ["/bin/bash"]

#----- show SELinux status
RUN getenforce

#----- default UTC
RUN date

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

#----- perl
RUN yum install -y \
    perl-core \
&& yum clean all
RUN perl -V

#----- etc packages
RUN yum install -y \
    gcc \
    tar \
    wget \
&& yum clean all
RUN gcc --version && tar --version && wget --version

#----- git
ENV GIT_VERSION 2.9.5
RUN yum install -y \
    curl-devel \
    expat-devel \
    gettext-devel \
    openssl-devel \
    zlib-devel \
&& yum clean all
RUN curl --version && openssl version
RUN wget https://mirrors.edge.kernel.org/pub/software/scm/git/git-$GIT_VERSION.tar.gz \
&& tar zxvf git-$GIT_VERSION.tar.gz \
&& cd git-$GIT_VERSION \
&& ./configure \
&& make \
&& make install
RUN git --version

#----- utils
RUN yum install -y \
    sudo \
    patch \
    which \
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
    pcre-devel \
    rpm-build \
    rsync \
    screen \
    strace \
    tcpdump \
    telnet \
    time \
    traceroute \
    tree \
&& yum clean all
RUN tree --version
RUN whois --version

RUN vi --version

#----- bayashi user
ENV MY_USER bayashi
RUN useradd $MY_USER \
&& echo "$MY_USER:" | chpasswd \
&& mkdir /home/$MY_USER/.ssh \
&& chmod 700 /home/$MY_USER/.ssh \
&& chown -R $MY_USER:$MY_USER /home/$MY_USER/.ssh
RUN echo "$MY_USER ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers.d/$MY_USER

RUN mkdir /home/$MY_USER/bin \
&& chown $MY_USER:$MY_USER /home/$MY_USER/bin
ENV PATH /home/$MY_USER/bin:$PATH

ENV HOME /home/$MY_USER
WORKDIR /home/$MY_USER
USER $MY_USER


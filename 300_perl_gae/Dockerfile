# 1. Container should be ephemeral.
# 2. Don't install unnecessary packages.
# 3. Each container should have only one application.
# 4. Sorting multi-line arguments alphanumerically.

FROM centos:centos6.7

MAINTAINER bayashi

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
&& make install \
&& rm -f git-$GIT_VERSION.tar.gz

#----- utils
RUN yum install -y \
    crontabs \
    freetype \
    giflib-devel \
    libjpeg-turbo-devel \
    libpng-devel \
    libxml2-devel \
    libxslt \
    libyaml \
    libyaml-devel \
    ntp \
    ntpdate \
    patch \
    pcre-devel \
    rsync \
    strace \
    time \
    which \
&& yum clean all

#----- Perl
ENV PERL_DIR /perl5
ENV PERL_VERSION 5.28.1

WORKDIR /perl5

RUN mkdir bin

ENV PATH bin:$PATH

RUN curl -sL https://raw.githubusercontent.com/tokuhirom/Perl-Build/master/perl-build > bin/perl-build
RUN perl -pi -e 's%^#!/usr/bin/env perl%#!/usr/bin/perl%g' bin/perl-build
RUN chmod +x bin/perl-build
RUN mkdir ${PERL_DIR}-${PERL_VERSION}

RUN perl-build $PERL_VERSION ${PERL_DIR}-${PERL_VERSION}
RUN curl -sL http://cpanmin.us/ | ${PERL_DIR}-${PERL_VERSION}/bin/perl - --notest App::cpanminus Carton Plack Gazelle

ENV PATH ${PERL_DIR}-${PERL_VERSION}/bin:$PATH

RUN ["cpanm", "--notest", "https://raw.githubusercontent.com/bayashi/j/master/tarballs/j-0.01.tar.gz"]

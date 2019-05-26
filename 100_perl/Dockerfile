# 1. Container should be ephemeral.
# 2. Don't install unnecessary packages.
# 3. Each container should have only one application.
# 4. Sorting multi-line arguments alphanumerically.
# 5. Installing something, show version immediately

FROM bayashi/bayacker:0.08

MAINTAINER bayashi

ENV PERL_DIR /perl5
ENV PERL_VERSION 5.28.1
ENV PATH bin:$PATH

WORKDIR /perl5

# Perl
RUN mkdir bin
RUN curl -sL https://raw.githubusercontent.com/tokuhirom/Perl-Build/master/perl-build > bin/perl-build
RUN perl -pi -e 's%^#!/usr/bin/env perl%#!/usr/bin/perl%g' bin/perl-build
RUN chmod +x bin/perl-build
RUN mkdir ${PERL_DIR}-${PERL_VERSION}
RUN perl-build $PERL_VERSION ${PERL_DIR}-${PERL_VERSION}
RUN curl -sL http://cpanmin.us/ | ${PERL_DIR}-${PERL_VERSION}/bin/perl - --notest App::cpanminus Carton Plack Gazelle

ENV PATH ${PERL_DIR}-${PERL_VERSION}/bin:$PATH

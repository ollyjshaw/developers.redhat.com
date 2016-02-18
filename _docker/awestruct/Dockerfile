FROM jruby:9
MAINTAINER Jason Porter <jporter@redhat.com>

# Prevent encoding errors
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US.UTF-8
ENV LC_ALL en_US.UTF-8

RUN apt-get update
RUN apt-get install -y \
    optipng \
    pngquant \
    git \
    autoconf \
    bison \
    build-essential \
    libssl-dev \
    libyaml-dev \
    libreadline6-dev \
    zlib1g-dev \
    libncurses5-dev \
    libffi-dev \
    libgdbm3 \
    libgdbm-dev

#WORKDIR /tmp
#RUN wget http://prdownloads.sourceforge.net/optipng/optipng-0.7.5.tar.gz?download && \
  #mv optipng* optipng.tar.gz && \
  #tar -xvzf optipng.tar.gz

#WORKDIR /tmp/optipng-0.7.5
#RUN chmod u+x configure
#RUN ./configure && make && make install

WORKDIR /home/awestruct

## Build setup
# Build the current gemset (user will only need to build the difference
COPY Gemfile Gemfile
COPY Gemfile.lock Gemfile.lock
COPY gemrc /home/awestruct/.gemrc

#parallel install of gems
RUN bundle install -j 10

WORKDIR /home/awestruct/developer.redhat.com

EXPOSE 4242

ENTRYPOINT [ "/bin/bash", "-l", "-c" ]
CMD [ "rake", "git_setup clean gen[docker]"]

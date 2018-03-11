FROM debian:jessie

RUN apt-get update && \
    DEBIAN_FRONTEND=noninteractive apt-get install -q -y \
    libsqlite3-dev \
    ruby \
    ruby-dev \
    build-essential && \
    gem install --no-ri --no-rdoc mailcatcher && \
    apt-get remove -y build-essential && \
    apt-get autoremove -y && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists

RUN echo Europe/Kiev > /etc/timezone && dpkg-reconfigure --frontend noninteractive tzdata

EXPOSE 1080 1025

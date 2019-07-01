FROM redis:5.0.5

LABEL maintainer="Danushka Fernando <wdfdo1986@gmail.com>"

# Some Environment Variables
ENV HOME /root
ENV DEBIAN_FRONTEND noninteractive

# Install system dependencies
RUN apt-get update -qq && \
    apt-get install --no-install-recommends -yqq \
      net-tools supervisor ruby rubygems locales gettext-base wget telnet vim && \
    apt-get clean -yqq

# # Ensure UTF-8 lang and locale
RUN locale-gen en_US.UTF-8
ENV LANG       en_US.UTF-8
ENV LC_ALL     en_US.UTF-8

# Necessary for gem installs due to SHA1 being weak and old cert being revoked
ENV SSL_CERT_FILE=/usr/local/etc/openssl/cert.pem

RUN gem install redis -v 4.0.2

RUN apt-get install -y gcc make g++ build-essential libc6-dev tcl git supervisor ruby

COPY PORT.conf /PORT.conf

# Add startup script
COPY docker-entrypoint.sh /docker-entrypoint.sh

RUN chmod 755 /docker-entrypoint.sh

EXPOSE $PORT:7000

ENTRYPOINT ["/docker-entrypoint.sh"]

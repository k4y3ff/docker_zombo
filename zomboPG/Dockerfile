#
# Postgres with ZomboDB
#

# Pull base image.
FROM postgres:9.3

# Fetch wget
RUN apt-get update && apt-get install -y --no-install-recommends ca-certificates wget && rm -rf /var/lib/apt/lists/*

# Make and friends
RUN apt-get update && apt-get install -y --no-install-recommends \
    make \
    automake \
    gcc \
    build-essential \
    g++ \
    cpp \
    libc6-dev \
    man-db \
    autoconf \
    pkg-config

# Install zombo
RUN \
  cd / && \
  mkdir zombodb && \
  cd zombodb && \
  wget https://github.com/zombodb/zombodb/releases/download/v2.1.38/zombodb_trusty_pg93-2.1.38_amd64.deb

RUN \
  cd zombodb && \
  dpkg -i zombodb_trusty_pg93-2.1.38_amd64.deb

#Install pg_partman
RUN \
  cd / && \
  mkdir pg_partman && \
  cd pg_partman && \
  wget https://github.com/keithf4/pg_partman/archive/v1.8.7.tar.gz

RUN \
  cd pg_partman && \
  tar -xvf v1.8.7.tar.gz && \
  cd pg_partman-1.8.7 && \
  make install

COPY zombo-entrypoint.sh /

RUN chmod +x /zombo-entrypoint.sh

ENTRYPOINT ["/zombo-entrypoint.sh"]

CMD ["postgres"]
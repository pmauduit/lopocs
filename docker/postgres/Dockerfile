FROM postgres:latest

RUN apt update && apt -y install build-essential git ca-certificates cmake \
  libgdal-dev g++ postgresql-server-dev-12 postgresql-12-postgis-3      && \
  rm -fr /var/lib/apt/lists/* /tmp/* /var/tmp/*

#git clone https://github.com/PDAL/PDAL.git --depth 1 -b  2.0.1 /usr/src/PDAL
#git clone https://github.com/PDAL/PDAL.git --depth 1 -b  2.0.1 /usr/src/PDAL

RUN git clone https://github.com/verma/laz-perf.git --depth 1 -b1.3.0 /usr/src/lazperf
# Need to checkout master, because it won't compile in v1.2.0 with postgresql 12
RUN git clone https://github.com/pgpointcloud/pointcloud.git /usr/src/pointcloud
RUN git clone https://github.com/Oslandia/pgmorton.git --depth 1 /usr/src/pgmorton

WORKDIR /usr/src/lazperf
RUN cmake . && make && make install

WORKDIR /usr/src/pointcloud
RUN autoconf && ./configure --with-lazperf=/usr/local && make && make install

WORKDIR /usr/src/pgmorton
RUN cmake . && make && make install

COPY 00-create-extensions.sql /docker-entrypoint-initdb.d/

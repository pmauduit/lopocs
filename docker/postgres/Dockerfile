FROM mdillon/postgis

apt update && apt -y install build-essential git ca-certificates cmake libgdal-dev

git clone https://github.com/PDAL/PDAL.git --depth 1 -b  2.0.1 /usr/src/PDAL

WORKDIR /usr/src/PDAL
RUN cmake . && make && make install


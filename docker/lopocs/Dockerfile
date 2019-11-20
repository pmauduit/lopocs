
FROM python:3.6

RUN apt update && apt install -y libgdal-dev cmake && \
   rm -fr /var/lib/apt/lists/* /tmp/* /var/tmp/*

# LASZIP
RUN git clone  https://github.com/LASzip/LASzip.git--depth 1 /usr/src/LASzip
WORKDIR /usr/src/LASzip
RUN cmake . && make && make install

# LAZperf
RUN git clone https://github.com/verma/laz-perf.git --depth 1 -b1.3.0 /usr/src/lazperf
WORKDIR /usr/src/lazperf
RUN cmake . && make && make install

RUN git clone https://github.com/PDAL/PDAL.git --depth 1 -b  2.0.1 /usr/src/PDAL
WORKDIR /usr/src/PDAL
RUN cmake -DWITH_LAZPERF=ON -DLAZPERF_INCLUDE_DIR=/usr/local  \
          -DWITH_LASZIP=ON                                .   \
    && make && make install

RUN mkdir -p /home/app
RUN git clone https://github.com/Oslandia/lopocs.git /home/app/lopocs
WORKDIR /home/app/lopocs

ENV LOPOCS_SETTINGS /etc/lopocs/lopocs.yml

RUN pip install 'numpy==1.14.3' &&  pip install -e .

CMD [ "lopocs", "serve", "--host=0.0.0.0", "--port=5000" ]

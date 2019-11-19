
FROM python:3.4

RUN apt update && apt install -y libgdal-dev && \
   rm -fr /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN mkdir -p /home/app
RUN git clone https://github.com/Oslandia/lopocs.git /home/app/lopocs
WORKDIR /home/app/lopocs

ENV LOPOCS_SETTINGS /etc/lopocs/lopocs.yml

RUN pip install 'numpy==1.14.3' &&  pip install -e .

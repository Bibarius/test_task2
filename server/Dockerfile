FROM ubuntu:20.04

RUN apt-get update
RUN apt-get install -y apt-utils -y liblapack3 -y build-essential \
                    -y python3-dev -y python3-setuptools \
                    -y python3-pip \
                    -y supervisor \
                    -y nmap

RUN apt-get -y install vim

# RUN apt-get update && apt-get install -y supervisor
RUN mkdir -p /var/log/supervisor
COPY supervisord.conf /etc/supervisor/conf.d/supervisord.conf

WORKDIR /usr/src/server
RUN python3 -m pip install --upgrade pip
COPY ./requirements.txt .
COPY templates .
ENV FLASK_DEBUG=1
RUN python3 -m pip install -r requirements.txt

COPY . .

CMD ["/usr/bin/supervisord"]
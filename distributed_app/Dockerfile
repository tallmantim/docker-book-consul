FROM ubuntu:18.04
LABEL maintainer="james@example.com"
ENV REFRESHED_AT 2019-01-07

RUN apt-get -qq update
RUN apt-get -qq install ruby-dev git libcurl4-openssl-dev curl build-essential python uwsgi uwsgi-dev
RUN gem install --no-ri --no-rdoc sinatra

RUN mkdir -p /opt/distributed_app
WORKDIR /opt/distributed_app
RUN uwsgi --build-plugin https://github.com/unbit/uwsgi-consul

ADD uwsgi-consul.ini /opt/distributed_app/
ADD config.ru /opt/distributed_app/

ENTRYPOINT [ "uwsgi", "--ini", "uwsgi-consul.ini", "--ini", "uwsgi-consul.ini:server1", "--ini", "uwsgi-consul.ini:server2" ]
CMD []


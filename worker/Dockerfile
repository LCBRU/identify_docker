FROM python:3.7

RUN mkdir -p /usr/src/app
WORKDIR /usr/src/app

RUN apt-get update && \
    apt-get -y upgrade && \
    DEBIAN_FRONTEND=noninteractive apt-get -y install \
        default-mysql-client \
        libldap2-dev \
        libsasl2-dev && \
    apt-get clean

RUN svn export --force https://github.com/LCBRU/identity/trunk/ /usr/src/app/

RUN pip install --no-cache-dir -r requirements.txt
FROM python:3.7

RUN mkdir -p /usr/src/app
WORKDIR /usr/src/app

RUN apt-get update && \
    apt-get -y upgrade && \
    DEBIAN_FRONTEND=noninteractive apt-get -y install \
        default-mysql-client \
        unixodbc-dev \
        libldap2-dev \
        libsasl2-dev && \
    apt-get clean

RUN svn export --force https://github.com/LCBRU/identity/trunk/ /usr/src/app/
ADD gunicorn.conf /usr/src/app/gunicorn.conf

RUN pip install --no-cache-dir gunicorn
RUN pip install --no-cache-dir -r requirements.txt

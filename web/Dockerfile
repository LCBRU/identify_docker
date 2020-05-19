FROM python:3.7

RUN mkdir -p /usr/src/app
WORKDIR /usr/src/app

RUN apt-get update \
&& apt-get install -y \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg \
&& curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add - \
&& curl https://packages.microsoft.com/config/debian/9/prod.list  > /etc/apt/sources.list.d/mssql-release.list \
&& apt-get update \
&& ACCEPT_EULA=Y apt-get -y install --no-install-recommends \
    default-mysql-client \
    libldap2-dev \
    libsasl2-dev \
&& ACCEPT_EULA=Y apt-get -y install --no-install-recommends \
    msodbcsql17 \
    mssql-tools \
    unixodbc-dev \
&& apt-get clean

RUN echo "2010-05-19 B"

RUN svn export --force https://github.com/LCBRU/identity/trunk/ /usr/src/app/
ADD gunicorn.conf /usr/src/app/gunicorn.conf

RUN pip install --no-cache-dir gunicorn
RUN pip install --no-cache-dir -r requirements.txt

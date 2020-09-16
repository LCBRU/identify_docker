FROM python:3.8

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

# Only needed to connect to SQL 2008
RUN apt-get update -yqq \
    && apt-get install -y --no-install-recommends openssl \ 
    && sed -i 's,^\(MinProtocol[ ]*=\).*,\1'TLSv1.0',g' /etc/ssl/openssl.cnf \
    && sed -i 's,^\(CipherString[ ]*=\).*,\1'DEFAULT@SECLEVEL=1',g' /etc/ssl/openssl.cnf\
    && rm -rf /var/lib/apt/lists/*

RUN echo "2010-09-16 A"

RUN svn export --force https://github.com/LCBRU/identity/trunk/ /usr/src/app/
ADD gunicorn.conf /usr/src/app/gunicorn.conf

RUN pip install --no-cache-dir gunicorn
RUN pip install --no-cache-dir -r requirements.txt

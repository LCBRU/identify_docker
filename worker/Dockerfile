FROM python:3.10-bookworm

ARG version

RUN mkdir -p /usr/src/app
WORKDIR /usr/src/app

RUN apt-get update \
&& apt-get install -y \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg \
    git \
&& curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add - \
&& curl https://packages.microsoft.com/config/debian/12/prod.list > /etc/apt/sources.list.d/mssql-release.list \
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

RUN echo "$version"

RUN git clone https://github.com/LCBRU/identity.git /usr/src/app/

RUN pip install --no-cache-dir -r requirements.txt
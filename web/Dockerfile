FROM python:3.10-bookworm

ARG version

RUN mkdir -p /usr/src/app
WORKDIR /usr/src/app

RUN apt-get update
RUN apt-get install -y \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg \
    git
RUN curl -fsSL https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor -o /usr/share/keyrings/microsoft-prod.gpg
RUN curl https://packages.microsoft.com/config/debian/12/prod.list > /etc/apt/sources.list.d/mssql-release.list
RUN apt-get update
RUN ACCEPT_EULA=Y apt-get -y install --no-install-recommends \
    mariadb-client \
    libldap2-dev \
    libsasl2-dev
RUN ACCEPT_EULA=Y apt-get -y install --no-install-recommends \
    msodbcsql17 \
    mssql-tools \
    unixodbc-dev
RUN apt-get clean

RUN echo "$version"

RUN git clone https://github.com/LCBRU/identity.git /usr/src/app/
ADD gunicorn.conf /usr/src/app/gunicorn.conf

RUN pip install --no-cache-dir gunicorn
RUN pip install --no-cache-dir -r requirements.txt

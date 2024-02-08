# identity Docker

Docker container for the BRC identity application.

## Installation and Running

1. Download the code from github

```bash
git clone https://github.com/LCBRU/identity_docker.git
```

2. Create the development environment:

Copy the file `example.env` to `.env` and edit it with the
correct details.

3. Run the application

From the `identity_docker` directory type the command:

```bash
docker-compose build
docker-compose up
```

## Debugging
### Dev Rabbit MQ
To bring up a dev Rabbit MQ for testing use the following command:
```bash
sudo docker run -d --hostname my-rabbit --name some-rabbit -e RABBITMQ_DEFAULT_USER=user -e RABBITMQ_DEFAULT_PASS=password -p 8080:15672 -p 5672:5672 rabbitmq:3-management
```

You then need to change the `.env` file details for Celery:
```bash
export BROKER_URL=pyamqp://richard:ct*i0*t*0@localhost:5672/identity
export CELERY_RESULT_BACKEND=rpc://
export CELERY_RATE_LIMIT=1
export CELERY_REDIRECT_STDOUTS_LEVEL=INFO
```
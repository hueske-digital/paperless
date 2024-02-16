# Paperless-ngx

This repository contains a Paperless-ngx instance with a ready-to-use configured [Apache Tika](https://tika.apache.org/) and [Gotenberg](https://gotenberg.dev/) to OCR your documents as well as a Postgres database for fast storage.

## Requirements

Make sure that the [nginx reverse proxy](https://gitlab.com/hueske-digital/services/proxy) is already set up and started.

## Setup instructions

Clone the code to your server:<br>
```
git clone git@gitlab.com:hueske-digital/services/paperless-ngx.git ~/services/paperless-ngx
```

Create environment file and fill up with your values:<br>
```
cd ~/services/paperless-ngx && cp .env.example .env && vim .env
```

Pull images and start the docker compose file:<br>
```
docker compose up -d
```

Create a superuser in Paperless-ngx:<br>
```
docker-compose run --rm app createsuperuser
```

Create a host in your nginx proxy manager which points to `paperless-ngx-app-1` with port `8000` and websockets enabled.

## Other information

Update all container images and recreate them if new images are available:<br>
```
docker compose pull && docker compose up -d
```

Restart a single container:<br>
```
docker compose restart app
```

Shutdown all container of this compose file:<br>
```
docker compose down
```

Show and follow logs:<br>
```
docker compose logs -ft
```

Additional configuration:<br>
You can include any other docker config by using an additional [compose file](https://docs.docker.com/compose/extends/).


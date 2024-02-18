# Paperless

Paperless is a digital document management solution designed to help you manage your documents in a Docker environment. This stack leverages Docker-Compose to simplify deployment and management.

## Requirements

Before you start, ensure you have the following installed on your system:

- Docker: https://docs.docker.com/get-docker/
- Docker-Compose: https://docs.docker.com/compose/install/
- Caddy Proxy: https://github.com/hueske-digital/caddy

## Installation Steps

**1. Prepare the services directory:**<br>
Ensure all your services, including Paperless, are organized in the `$HOME/services` directory for easy management.
```
mkdir -p $HOME/services
cd $HOME/services
```
**2. Clone the repository:**<br>
```
git clone https://github.com/hueske-digital/paperless.git
cd paperless
```
**3. Create a `.env` file:**<br>
Copy the `.env.example` file to `.env` and adjust the environment variables according to your setup. This usually includes paths and port configurations.
```
cp .env.example .env
vim .env
```
**4. Start the stack:**<br>
Use Docker-Compose to start the paperless stack. This command will pull the necessary Docker images and start the services defined in your `docker-compose.yml` file.
```
docker-compose up -d --pull=always
```

## Specific Configurations
This section covers configurations specific to Paperless that aren't part of the standard installation process. These may include adjustments for performance, security, or functionality.
- **Create first user:**<br>
The following command will prompt you to set a username, an optional e-mail address and finally a password (at least 8 characters).
```
docker compose run --rm app createsuperuser
```
- **Set up the import of encrypted PDF files:**<br>
To do this, you must adapt the `.env` file by adapting the `PAPERLESS_DECRYPT_PASSWORD` variable with the passwords for decryption.
```
# Passwords for decryption (split multiple passwords with whitespaces)
PAPERLESS_DECRYPT_PASSWORD="test test123"
```

## Lifecycle Management

- **Update the entire stack:**<br>
```
git pull
docker compose up -d --pull=always --remove-orphans
```

- **Recreate the stack (e.g. when changing `.env` file):**<br>
```
docker compose up -d --force-recreate
```

- **Shutdown the entire stack:**<br>
```
docker compose down
```

- **Restart a single container:**<br>
```
docker compose restart app
```

- **Show logs:**<br>
```
docker compose logs -ft
```

## Questions, Comments or Suggestions for Changes

We welcome your curiosity, feedback, and contributions! If you have any questions, comments, or suggestions for changes, please feel free to open an issue or submit a pull request on GitHub. Your input is invaluable in making this project better for everyone.

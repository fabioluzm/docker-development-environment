# Docker Development Environment

### This repository contains docker-based infrastructures:

- PostgreSQL database environment
- MySQL database environment
- Wordpress project on isolated environment

## Folder Structure

```
repository
  ├── postgres/
  │    ├── docker-compose-postgres.yml
  ├── mysql/
  │    ├── docker-compose-mysql.yml
  ├── wordpress-project/
  │    ├── .env.example
  │    ├── docker-compose-db-init.yml
  │    ├── docker-compose-wordpress.yml
  │    ├── docker-compose-override.yml
  │    ├── dump.sql (for test purposes)
  │    ├── Makefile
  │    └── wp-config.php
  └── README.md
```

## PostgreSQL

- Create `.env` with desired variables

```bash
make up        # start postgres + pgadmin
make ps        # see containers
make logs      # tail logs
make down      # stop (keep data)
make nuke      # stop + DELETE data volumes
make save-images / load-images  # offline kit
```

```
postgres
  ├── user: `set on .env`
  ├── password: `set on .env`
  └── port: `set on .env`
```

## MySQL

- Run `docker compose -f docker-compose-mysql.yml`
- Access phpMyAdmin on `localhost:8080`

```
mysql
  ├── port: 3306
phpmyadmin
  ├── port: 8080
  ├── user: root
  └── root_password: root
```

## WordPress Project Environment

WordPress project uses `Makerfile` to create and run the environment

- Run `make` to:
  - Create and import the database
  - Remove the initiator container
  - Create a isolated container based on `Dockerfile`
  - Call wordpress image if no `Dockerfile` is found
  - Mount/bind local code to docker container

---

## Notes

- Use `host.docker.internal` as `DB_HOST` to connect from project containers to the MySQL container on Windows/Mac.
- Ensure consistent MySQL user permissions to isolate databases.
- Each project mounts its code locally for live updates.
- You can customize PHP/Apache versions per project if needed.

---

## How to Use

1. PostgreSQL environment (once):

    - Create `.env` with desired variables
    
    ```bash
    make up        # start postgres + pgadmin
    make ps        # see containers
    make logs      # tail logs
    make down      # stop (keep data)
    make nuke      # stop + DELETE data volumes
    make save-images / load-images  # offline kit
    ```

2. MySQL environment (once):

   ```bash
   docker compose -f docker-compose-mysql.yml up -d
   ```

3. For each WordPress project:

   - Add your code and `.env`
   - Run the project with: `make`

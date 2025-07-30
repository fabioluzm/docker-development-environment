# Makefile for WordPress project setup

# File paths
INIT_COMPOSE_FILE=docker-compose-db-init.yml
WORDPRESS_COMPOSE_FILE=docker-compose-wordpress.yml
WORDPRESS_COMPOSE_OVERRIDE_FILE=docker-compose-override.yml

# Targets
.PHONY: all init clean-init up down stop

# Default target: run everything
all: init up

# Run DB init and remove container
init:
	docker compose -f $(INIT_COMPOSE_FILE) run --rm db-init

# Start WordPress environment
up:
ifeq ("$(wildcard Dockerfile)","Dockerfile")
	docker compose -f $(WORDPRESS_COMPOSE_OVERRIDE_FILE) up -d
else
	docker compose -f $(WORDPRESS_COMPOSE_FILE) up -d
endif

# Stop all containers
stop:
	docker compose -f $(WORDPRESS_COMPOSE_FILE) stop

# Stop and remove all containers
down:
	docker compose -f $(WORDPRESS_COMPOSE_FILE) down

# Clean only the init container (just in case it's left behind)
clean-init:
	-docker rm -f db-init-1 || true

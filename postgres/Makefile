SHELL := /bin/sh
ENV ?= .env
COMPOSE := docker compose --env-file $(ENV) -f docker-compose.yml

.PHONY: up down restart ps logs load-images save-images clean nuke

up:
	$(COMPOSE) up -d
	@echo "pgAdmin → http://localhost:$$(grep ^PGADMIN_PORT $(ENV) | cut -d= -f2)"
	@echo "Postgres port → $$(grep ^PG_PORT $(ENV) | cut -d= -f2)"

down:
	$(COMPOSE) down

restart: down up

ps:
	$(COMPOSE) ps

logs:
	$(COMPOSE) logs -f

save-images:
	mkdir -p images
	docker pull postgres:15
	docker pull dpage/pgadmin4:latest
	docker save -o images/postgres15.tar postgres:15
	docker save -o images/pgadmin4.tar dpage/pgadmin4:latest

load-images:
	docker load -i images/postgres15.tar
	docker load -i images/pgadmin4.tar

clean:
	$(COMPOSE) down --remove-orphans

# DANGER: deletes volumes (all data)
nuke:
	$(COMPOSE) down -v --remove-orphans

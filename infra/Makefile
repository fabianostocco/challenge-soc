all: create

create:
	docker-compose up -d --build

delete:
	docker-compose down
	docker system prune --all -f
	docker volume prune -f

recreate: delete create
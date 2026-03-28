FRONT_END_BINARY=frontApp
BROKER_BINARY=brokerApp
AUTH_BINARY=authApp

## Detect OS
ifeq ($(OS),Windows_NT)
    FRONT_END_BINARY := frontApp.exe
endif

## up: starts all containers in the background
up:
	@echo "Starting Docker containers..."
	docker-compose up -d
	@echo "Done!"

## up_build: rebuild and start containers
up_build: 
	@echo "Stopping containers (if running)..."
	docker-compose down
	@echo "Building and starting containers..."
	docker-compose up --build -d
	@echo "Done!"

## down: stop docker compose
down:
	@echo "Stopping docker compose..."
	docker-compose down
	@echo "Done!"

## build_broker: builds broker binary for Linux
build_broker:
	@echo "Building broker..."
	cd ../broker-service && GOOS=linux GOARCH=amd64 CGO_ENABLED=0 go build -o $(BROKER_BINARY) ./cmd/api
	@echo "Done!"

## build_auth: builds auth binary for Linux
build_auth:
	@echo "Building auth..."
	cd ../authentication-service && GOOS=linux GOARCH=amd64 CGO_ENABLED=0 go build -o $(AUTH_BINARY) ./cmd/api
	@echo "Done!"

## build_front: builds frontend
build_front:
	@echo "Building frontend..."
	cd ../front-end && CGO_ENABLED=0 go build -o $(FRONT_END_BINARY) ./cmd/web
	@echo "Done!"

## start: starts frontend
start: build_front
	@echo "Starting frontend..."
ifeq ($(OS),Windows_NT)
	cd ../front-end && $(FRONT_END_BINARY)
else
	cd ../front-end && ./$(FRONT_END_BINARY) &
endif

## stop: stops frontend
stop:
	@echo "Stopping frontend..."
ifeq ($(OS),Windows_NT)
	taskkill /F /IM $(FRONT_END_BINARY) || true
else
	pkill $(FRONT_END_BINARY) || true
endif
	@echo "Stopped!"
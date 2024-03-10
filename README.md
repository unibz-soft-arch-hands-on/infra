# Requirements

- Caddy server

```bash
brew install caddy
```

- Http Server

```bash
npm -g install http-server
```

- docker (https://docs.docker.com/desktop/install/mac-install/)
- docker compose (https://docs.docker.com/compose/install/)


# Running

1. Run the docker infrastructure

    ```bash
    # terminal 1
    cd /path/to/project/infra
    docker compose up -d
    ```

    > this will run a RabbitMQ server, and two instances of PostgreSQL

2. Launch the backend applications

    **IMPORTANT** make sure you made available the variables in the `.env` (i.e. set them up and exported them to the environment)

    ```bash
    # terminal 2
    cd /path/to/project/creator
    ./gradlew bootRun

    # terminal 3
    cd /path/to/project/querier
    ./gradlew bootRun
    ```

    > this will run two SpringBoot servers, on ports 8080 and 8081

3. Run the frontend server

    ```bash
    # terminal 4
    cd /path/to/project/front
    http-server . -p 8082
    ```

    > this will run an HTTP server on port 8082

4. Run a reverse proxy for the entire project

    ```bash
    # terminal 5
    cd /path/to/project/infra
    caddy run
    ```

    > this will run a Caddy server placed in front of all other systems
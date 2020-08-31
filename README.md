# basic-microservices

Project consists of two services:

* spring-boot-app
* node-app

## Usage

Clone directory and move to it:

```bash
git clone git@github.com:kibrovic/basic-microservices.git
cd basic-microservices
```

Build images using `docker-compose`:

```bash
docker-compose build && docker-compose up -d
```

After build is complete, `docker-compose up -d` will start containers in detached mode. Testing with `bash ./health_check.sh` should return:

```bash
kenan:~/Private/basic-microservices(master)$ bash ./health_check.sh
Response from 'spring service' java/api/v1/status API [OK]
Response from 'spring service' java/api/v1/node API [OK]
Response from 'node service' node/api/v1/result API [OK]

All checks passed. Congrats!
```

If changes are to be made, stop and remove containers using:

```bash
docker-container rm -sf
```

Then bring them back up using previous commands:

```bash
docker-compose build && docker-compose up -d
```

## Details

`spring-boot-app` requires PostgreSQL instance to work properly. Postgres database is defined in `docker-compose.yml` file as `dbpostgresql` mapped to port `5432`. Database, username and password are defined as environmental variables in `.env` file. Custom app configs are placed in `spring-boot-app/my-conf.yml` where URLs are set to match service names (`node-app` and `dbpostgresql`)

`node-app` is fairly simple and doesn't require any modifications.

Each `Dockerfile` clones [kkenan/basic-microservices](https://github.com/kkenan/basic-microservices) repo during every build. Long term, it would make more sense to clone it on host and mount needed volumes.


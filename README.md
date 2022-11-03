# Dictionary Back-End
____

## About:
Dictionary as telegram bot, with your words, where you can add and learn new words in another language. 
You don't need to download app or open special site, you just need telegram.
___

## Plugins:
Dillinger is currently extended with the following plugins.
Instructions on how to use them in your own application are linked below.

| Plugin | README |
| ------ | ------ |
| Mypy | https://mypy.readthedocs.io/en/stable/introduction.html |
| Black | https://github.com/psf/black |
| Flake8 | https://flake8.pycqa.org/en/latest/ |
| Isort | https://github.com/PyCQA/isort |
___

## Features:
 - Full **Docker** integration (Docker based).
 - **Docker Compose** integration and optimization.
 - **Deploing ready** Python web server using Uvicorn and Gunicorn.
 - Python [FastAPI](https://github.com/tiangolo/fastapi) backend:
    - **Fast**: Very high performance.
    - **Intuitive**: Great editor support. Completion everywhere. Less time debugging.
    - **Easy**: Designed to be easy to use.
    - **Short**: Minimum code duplication.
    - **Robust**: Production-ready code. With interactive documentation.
    - **Standards-based**: Based on (and fully compatible with) the open standards for APIs: [OpenAPI](https://github.com/OAI/OpenAPI-Specification)
     and [JSON Schema](http://json-schema.org/).
    - [Many other features](https://fastapi.tiangolo.com/features/) including automatic validation, serialization, interactive documentation, authentication with OAuth2 JWT tokens, etc.
 - **Secure password** hashing by default.
 - **JWT token** authentication.
 - **SQLAlchemy** models.
 - **Alembic** migrations.
 - **CORS** (Cross Origin Resource Sharing).
 - **Celery** worker that can perform pending or scheduled tasks.
 - REST backend tests based on asynchronous **Pytest**, integrated with Docker, so you can test the full API interaction, independent on the database. As it runs in Docker, it can build a new data store from scratch each time.
 - **JWT Authentication** handling.
 - Docker multi-stage building, so your project will have the less size.
___

## Project setup:
 To start project machine must have:

* [docker](https://docs.docker.com/engine/install/) - The virtual environment to set up project
* [docker-compose](https://docs.docker.com/compose/install/) - The additional util to manipulate of all services inside

### Project setup steps:
1) Open directory with `docker-compose` and `.env` file

2) Open `.env` file and change values

3) Write commands:

   3.1 Build containers:
   ```
   docker-compose -f docker-compose.yml build
   ```
   
   3.2 Run project:
   ```
   docker-compose -f docker-compose.yml up -d
   ```

### The .env file
The `.env` file is the one that contains all your configurations, generated keys and passwords, etc.

Depending on your workflow, you could want to exclude it from Git, for example if your project is public. In that case, you would have to make sure to set up a way for your CI tools to obtain it while building or deploying your project.

One way to do it could be to add each environment variable to your CI/CD system, and updating the docker-compose.yml file to read that specific env var instead of reading the `.env` file.

### Enviroments:
 - **DOMAIN** - Project domain name
 - **INSTALL_DEV** - Boolean value for permission to install additional libraries
 - **DEBUGER_POST** - Port for debuger

#### Backend
 - **BACKEND_CORS_ORIGINS** - A list with HTTP headers that allow the server to specify any source (domain, schema, or port) other than its own, from which the browser can allow resources to be loaded.
 - **PROJECT_NAME** - Project's name 
 - **SECRET_KEY** - This key is used to encrypt all sensitive data and makes your project more secure. Кeep the secret key used in production secret!
 - **FIRST_SUPERUSER** - Default superuser email
 - **FIRST_SUPERUSER_PASSWORD** - Default superuser password
 - **FIRST_SUPERUSER_USERNAME** - Default superuser username
 - **FIRST_SUPERUSER_FIRST_NAME** - Default superuser firstname
 - **FIRST_SUPERUSER_LAST_NAME** - Default superuser lastname
 - **FIRST_SUPERUSER_AGE** - Default superuser age
 - **SMTP_TLS** - Boolean value for extension of the regular text exchange protocol that allows you to create an encrypted connection right on top of a regular TCP connection, instead of opening a separate port for the encrypted connection.
 - **SMTP_PORT** - SMTP port (Default 587)
 - **SMTP_HOST** - SMTP host (example: `smtp.gmail.com`)
 - **SMTP_USER** - user on this SMTP server. If use gmail SMTP server than user `username` and user `email` will be same (example: `username@gmail.com`)
 - **SMTP_PASSWORD** - user password 
 - **EMAILS_FROM_EMAIL** - user email (example: `username@gmail.com`)
 - **DEFAULT_TIME_ZONE** - That timezone will be used by default (example: `"Europe/Kiev"`)

### Live development with Python Jupyter Notebooks

If you know about Python [Jupyter Notebooks](http://jupyter.org/), you can take advantage of them during local development.

The `docker-compose.override.yml` file sends a variable `env` with a value `dev` to the build process of the Docker image (during local development) and the `Dockerfile` has steps to then install and configure Jupyter inside your Docker container.

So, you can enter into the running Docker container:

```bash
docker-compose exec server bash
```

And use the environment variable `$JUPYTER` to run a Jupyter Notebook with everything configured to listen on the public port (so that you can use it from your browser).

#### Postgres
 - **POSTGRES_SERVER** - Database server
 - **POSTGRES_USER** - Database user
 - **POSTGRES_PASSWORD** - Database user password
 - **POSTGRES_DB=** - Database name

 - **TEST_POSTGRES_DB** - Test database name

#### Traefik
 - **TRAEFIK_PUBLIC_NETWORK** - A network name that will be shared with Traefik and the containers that should be accessible from the outside
 - **TRAEFIK_PUBLIC_TAG** - This public Traefik will only use services with this tag
 - **STACK_NAME** - Project name 
 - **TRAEFIK_TAG** - Add a constraint to only use services with the label for this stack


### Project backend documentation
After project is start, frontent developers can use endpoints documentation: 
`domain_name.com`/redoc/
___

## Additional commands:
 Stop project:
```
   docker-compose -f docker-compose.yml stop
```

Down containers:
```
   docker-compose -f docker-compose.yml down
```

Down containers and delete database volumes (`all data from database will be deleted!`):
```
   docker-compose -f docker-compose.yml down --volume
```
___

## Bash scripts:
Format code style:
```
    docker-compose -f docker-compose.yml run --rm server ./scripts/format.sh 
```
Sort imports and remove unused imports:
```
    docker-compose -f docker-compose.yml run --rm server ./scripts/format-imports.sh
```
Find code style errors and prints them without files formatting:
```
    docker-compose -f docker-compose.yml run --rm server ./scripts/lint.sh
```
Run migrations, create initial data in DB and start project:
```
    docker-compose -f docker-compose.yml run --rm server ./scripts/start.sh
```
Start project in debugging mode:
```
    docker-compose -f docker-compose.yml run --rm server ./scripts/start-debug.sh
```
Start project with live reloading:
```
    docker-compose -f docker-compose.yml run --rm server ./scripts/start-reload.sh
```
Run project tests:
```
    docker-compose -f docker-compose.yml run --rm server ./scripts/test.sh
```
Run project tests and return response in HTML format:
```
    docker-compose -f docker-compose.yml run --rm server ./scripts/test-cov-html.sh
```
Check database awake and run project tests
```
    docker-compose -f docker-compose.yml run --rm server ./scripts/tests-start.sh
```
Run coverage and build badges for README:
```
    docker-compose -f docker-compose.yml run --rm server ./scripts/coverage-badge.sh
```
___

## Project technologies:
  - [docker](https://docs.docker.com/) - is an open platform for developing, shipping, and running applications. Docker enables you to separate your applications from your infrastructure so you can deliver software quickly. With Docker, you can manage your infrastructure in the same ways you manage your applications. By taking advantage of Docker’s methodologies for shipping, testing, and deploying code quickly, you can significantly reduce the delay between writing code and running it in production.

 - [docker-compose](https://docs.docker.com/compose/) - Compose is a tool for defining and running multi-container Docker applications. With Compose, you use a YAML file to configure your application’s services. Then, with a single command, you create and start all the services from your configuration. To learn more about all the features of Compose, see [the list of features](https://docs.docker.com/compose/#features).

 - [python 3.11](https://docs.python.org/3.11/) - is an easy to learn, powerful programming language. It has efficient high-level data structures and a simple but effective approach to object-oriented programming. Python’s elegant syntax and dynamic typing, together with its interpreted nature, make it an ideal language for scripting and rapid application development in many areas on most platforms.

 - [FastAPI](https://fastapi.tiangolo.com/) - is a modern, fast (high-performance), web framework for building APIs with Python 3.6+ based on standard Python type hints.
 
 
 - [adminer](https://www.adminer.org/) (formerly phpMinAdmin) -  is a full-featured database management tool written in PHP. Conversely to phpMyAdmin, it consist of a single file ready to deploy to the target server. Adminer is available for MySQL, MariaDB, PostgreSQL, SQLite, MS SQL, Oracle, Elasticsearch, MongoDB and others via plugin
 
 - [postgres](https://www.postgresql.org/docs/) - is an object-relational database management system (ORDBMS) based on POSTGRES, POSTGRES pioneered many concepts that only became available in some commercial database systems much later. 
___

## Microservices:
 ### docker-compose file:
 - **FastAPI** as a backend
 - **postgres** as a database
 - **adminer** as full-featured database management tool


# Full Stack FastAPI, React and PostgreSQL - Boilerplate Project Generator

[![Build Status](https://travis-ci.com/isakbosman/full-stack-fastapi-react-postgres-boilerplate.svg?branch=master)](https://travis-ci.com/isakbosman/full-stack-fastapi-react-postgres-boilerplate)

Generate a backend and frontend stack using Python, including interactive API documentation.

### Interactive API documentation

[![API docs](img/docs.png)](https://github.com/isakbosman/full-stack-fastapi-react-postgres-boilerplate)

### Alternative API documentation

[![API docs](img/redoc.png)](https://github.com/isakbosman/full-stack-fastapi-react-postgres-boilerplate)

### Dashboard Login

[![API docs](img/login.png)](https://github.com/isakbosman/full-stack-fastapi-react-postgres-boilerplate)

### Dashboard - Create User

[![API docs](img/dashboard.png)](https://github.com/isakbosman/full-stack-fastapi-react-postgres-boilerplate)

## Features

* Full **Docker** integration (Docker based).
* Docker Swarm Mode deployment.
* **Docker Compose** integration and optimization for local development.
* **Production ready** Python web server using Uvicorn and Gunicorn.
* Python <a href="https://github.com/tiangolo/fastapi" class="external-link" target="_blank">**FastAPI**</a> backend:
    * **Fast**: Very high performance, on par with **NodeJS** and **Go** (thanks to Starlette and Pydantic).
    * **Intuitive**: Great editor support. <abbr title="also known as auto-complete, autocompletion, IntelliSense">Completion</abbr> everywhere. Less time debugging.
    * **Easy**: Designed to be easy to use and learn. Less time reading docs.
    * **Short**: Minimize code duplication. Multiple features from each parameter declaration.
    * **Robust**: Get production-ready code. With automatic interactive documentation.
    * **Standards-based**: Based on (and fully compatible with) the open standards for APIs: <a href="https://github.com/OAI/OpenAPI-Specification" class="external-link" target="_blank">OpenAPI</a> and <a href="http://json-schema.org/" class="external-link" target="_blank">JSON Schema</a>.
    * <a href="https://fastapi.tiangolo.com/features/" class="external-link" target="_blank">**Many other features**</a> including automatic validation, serialization, interactive documentation, authentication with OAuth2 JWT tokens, etc.
* **Secure password** hashing by default.
* **JWT token** authentication.
* **SQLAlchemy** models (independent of Flask extensions, so they can be used with Celery workers directly).
* Basic starting models for users (modify and remove as you need).
* **Alembic** migrations.
* **CORS** (Cross Origin Resource Sharing).
* **Celery** worker that can import and use models and code from the rest of the backend selectively.
* REST backend tests based on **Pytest**, integrated with Docker, so you can test the full API interaction, independent on the database. As it runs in Docker, it can build a new data store from scratch each time (so you can use ElasticSearch, MongoDB, CouchDB, or whatever you want, and just test that the API works).
* Easy Python integration with **Jupyter Kernels** for remote or in-Docker development with extensions like Atom Hydrogen or Visual Studio Code Jupyter.
* **React/Redux/Saga/Ant** frontend:
    * Based on the popular React Boilerplate(https://github.com/gilbarbara/react-redux-saga-boilerplate).
    * **JWT Authentication** handling.
    * Login view.
    * After login, main dashboard view.
    * Main dashboard with user creation and edition.
    * Self user edition.
    * **React**.
    * **Reduct**.
    * **React Router**.
    * **Ant Design** for enterprise design components.
    * **Redux Saga**.
    * Docker server based on **Nginx**
    * Docker multi-stage building, so you don't need to save or commit compiled code.
    * Frontend tests ran at build time (can be disabled too).
    * Made as modular as possible, so it works out of the box.
    * It's also easy to remove it if you have an API-only app, check the instructions in the generated `README.md`.
* **PGAdmin** for PostgreSQL database, you can modify it to use PHPMyAdmin and MySQL easily.
* **Flower** for Celery jobs monitoring.
* Load balancing between frontend and backend with **Traefik**, so you can have both under the same domain, separated by path, but served by different containers.
* Traefik integration, including Let's Encrypt **HTTPS** certificates automatic generation.
* GitLab **CI** (continuous integration), including frontend and backend testing.

## How to use it

Go to the directory where you want to create your project and run:

```bash
pip install cookiecutter
cookiecutter https://github.com/gilbarbara/react-redux-saga-boilerplate
```

### Generate passwords

You will be asked to provide passwords and secret keys for several components. Open another terminal and run:

```bash
openssl rand -hex 32
# Outputs something like: 99d3b1f01aa639e4a76f4fc281fc834747a543720ba4c8a8648ba755aef9be7f
```

Copy the contents and use that as password / secret key. And run that again to generate another secure key.


### Input variables

The generator (cookiecutter) will ask you for some data, you might want to have at hand before generating the project.

The input variables, with their default values (some auto generated) are:

* `project_name`: The name of the project
* `project_slug`: The development friendly name of the project. By default, based on the project name
* `domain_main`: The domain in where to deploy the project for production (from the branch `production`), used by the load balancer, backend, etc. By default, based on the project slug.
* `domain_staging`: The domain in where to deploy while staging (before production) (from the branch `master`). By default, based on the main domain.

* `docker_swarm_stack_name_main`: The name of the stack while deploying to Docker in Swarm mode for production. By default, based on the domain.
* `docker_swarm_stack_name_staging`: The name of the stack while deploying to Docker in Swarm mode for staging. By default, based on the domain.

* `secret_key`: Backend server secret key. Use the method above to generate it.
* `first_superuser`: The first superuser generated, with it you will be able to create more users, etc. By default, based on the domain.
* `first_superuser_password`: First superuser password. Use the method above to generate it.
* `backend_cors_origins`: Origins (domains, more or less) that are enabled for CORS (Cross Origin Resource Sharing). This allows a frontend in one domain (e.g. `https://dashboard.example.com`) to communicate with this backend, that could be living in another domain (e.g. `https://api.example.com`). It can also be used to allow your local frontend (with a custom `hosts` domain mapping, as described in the project's `README.md`) that could be living in `http://dev.example.com:8080` to communicate with the backend at `https://stag.example.com`. Notice the `http` vs `https` and the `dev.` prefix for local development vs the "staging" `stag.` prefix. By default, it includes origins for production, staging and development, with ports commonly used during local development by several popular frontend frameworks (Vue with `:8080`, React, Angular).
* `smtp_port`: Port to use to send emails via SMTP. By default `587`.
* `smtp_host`: Host to use to send emails, it would be given by your email provider, like Mailgun, Sparkpost, etc.
* `smtp_user`: The user to use in the SMTP connection. The value will be given by your email provider.
* `smtp_password`: The password to be used in the SMTP connection. The value will be given by the email provider.
* `smtp_emails_from_email`: The email account to use as the sender in the notification emails, it would be something like `info@your-custom-domain.com`.
 
* `postgres_password`: Postgres database password. Use the method above to generate it. (You could easily modify it to use MySQL, MariaDB, etc).
* `pgadmin_default_user`: PGAdmin default user, to log-in to the PGAdmin interface.
* `pgadmin_default_user_password`: PGAdmin default user password. Generate it with the method above.
 
* `traefik_constraint_tag`: The tag to be used by the internal Traefik load balancer (for example, to divide requests between backend and frontend) for production. Used to separate this stack from any other stack you might have. This should identify each stack in each environment (production, staging, etc).
* `traefik_constraint_tag_staging`: The Traefik tag to be used while on staging.
* `traefik_public_constraint_tag`: The tag that should be used by stack services that should communicate with the public.

* `flower_auth`: Basic HTTP authentication for flower, in the form`user:password`. By default: "`admin:changethis`".

* `sentry_dsn`: Key URL (DSN) of Sentry, for live error reporting. You can use the open source version or a free account. E.g.: `https://1234abcd:5678ef@sentry.example.com/30`.

* `docker_image_prefix`: Prefix to use for Docker image names. If you are using GitLab Docker registry it would be based on your code repository. E.g.: `git.example.com/development-team/my-awesome-project/`.
* `docker_image_backend`: Docker image name for the backend. By default, it will be based on your Docker image prefix, e.g.: `git.example.com/development-team/my-awesome-project/backend`. And depending on your environment, a different tag will be appended ( `prod`, `stag`, `branch` ). So, the final image names used will be like: `git.example.com/development-team/my-awesome-project/backend:prod`.
* `docker_image_celeryworker`: Docker image for the celery worker. By default, based on your Docker image prefix.
* `docker_image_frontend`: Docker image for the frontend. By default, based on your Docker image prefix.

## How to deploy

This stack can be adjusted and used with several deployment options that are compatible with Docker Compose, but it is designed to be used in a cluster controlled with pure Docker in Swarm Mode with a Traefik main load balancer proxy handling automatic HTTPS certificates, using the ideas from <a href="https://dockerswarm.rocks" target="_blank">DockerSwarm.rocks</a>.

Please refer to <a href="https://dockerswarm.rocks" target="_blank">DockerSwarm.rocks</a> to see how to deploy such a cluster in 20 minutes.

## More details

After using this generator, your new project (the directory created) will contain an extensive `README.md` with instructions for development, deployment, etc. You can pre-read [the project `README.md` template here too](./{{cookiecutter.project_slug}}/README.md).

## Based on the project generator

* Full Stack FastAPI Couchbase: [https://github.com/tiangolo/full-stack-fastapi-couchbase](https://github.com/tiangolo/full-stack-fastapi-couchbase).

## Release Notes

### Latest Changes

### 0.0.1
* Initial Release


## License

This project is licensed under the terms of the MIT license.

# Introduction
This repository deploys the Mushroom Classification Application containers via Docker-Compose. The accompanying `docker-compose-prod.yml` and `docker-compose.yml` files in the root of the project can be used respectively for production or to run locally. The `docker-compose-light.prod.yml` shows how the apps can be deployed without the reverse proxy and certbot images, and be exposed onto an external network (for example, the one being used by your reverse proxy).

| Repositories Deployed                                        | DockerHub image                                              | Badges                                                       |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| [Mushroom Classification Flask API](https://github.com/CallumHoughton18/Mushroom-Classification) | [mushroom-api](https://hub.docker.com/repository/docker/callumhoughton22/mushroom-api) | ![Docker Image Size (tag)](https://img.shields.io/docker/image-size/callumhoughton22/mushroom-api/latest) |
| [Mushroom Classification Front-End](https://github.com/CallumHoughton18/Mushroom-Classification-Front-End) | [mushroom-classification-front-end](https://hub.docker.com/repository/docker/callumhoughton22/mushroom-classification-front-end) | ![Docker Image Size (latest by date)](https://img.shields.io/docker/image-size/callumhoughton22/mushroom-classification-front-end) |

The production yml file uses nginx as the reverse proxy server and gunicorn as the WSGI server to the serve the application.

For information on how to use [Docker](https://docs.docker.com/) and [Docker Compose](https://docs.docker.com/compose/) consult the documentation.

## Docker Containers Setup

For both docker-compose files a `.docker.env` file needs to be present in the root of the project. This should contain all the environment variables needed for the Flask API to run. For environment variables that specify paths for the Flask API container the 'working directory' should be assumed to be the src folder.

An example .docker.env file, excluding any sensitive information, would be like:

`FLASK_ENV=development
FLASK_APP=./api/__init__.py
DATASET_DIR=./files
CURRENT_MODEL_DIR=./current_model
TRAINED_MODELS_DIR=./trained_models
FEATURE_DEFINITION_PATH=./files/features-definition.json
LOGS_DIRECTORY=./api_logs`

Also, a .react.docker.env file must be present in the root of the project, containing the environment variable pointing to the api url, an exmaple would look like:
`API_BASE_URL=https://mushroomlapi.callums-stuff.net/`

For the production docker-compose file an `nginx.conf` file needs to be present in the `nginx` directory. For instructions on how to setup this file read the [nginx documentation](https://www.linode.com/docs/web-servers/nginx/nginx-installation-and-basic-setup/). Or, contact the repository owner for an example.
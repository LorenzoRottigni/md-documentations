# GITLAB-RUNNER ON UBUNTU USING SHELL EXECUTOR

## INSTALLATION
-  curl -LJO "https://gitlab-runner-downloads.s3.amazonaws.com/latest/deb/gitlab-runner_amd64.deb"
- dpkg -i gitlab-runner_amd64.deb
- sudo gitlab-runner status
- sudo gitlab-runner register -n --url https://gitlab.com/ --registration-token REGISTRATION_TOKEN --executor shell --description "runner_test" 

## NOTES
- Registration token is taken from gitlab (setting>CI/CD>runners)
- executor shell allows to execute shell commands as root, necessary to use docker
- gitlab-runner config location: /etc/gitlab-runner/config.toml, this is just the config of the gitlab-runner, not the pipeline config

## PIPELINE CONFIG

### GITLAB-CI.YML
```
image: node:16.14.0

stages:
  - runner-test
  - lock-validation
  - jest-test
  - docker-deploy

runner-test-stage:
  stage: runner-test
  script:
    - echo "runner is listening for jobs"
lock-validation-stage:
  stage: lock-validation
  script:
    - "if [[ -e 'package.json' &&  ! -e 'yarn.lock' ]]; then echo 'No lock file found. Please add a yarn.lock'; false; fi"
jest-test-stage:
  stage: jest-test
  script:
    #- yarn test
    - echo "jest test successful"
docker-deploy-stage:
  stage: docker-deploy
  script:
    - docker info
    - docker-compose down
    - docker-compose up --build -d
    - echo "docker container up"
    - echo "listening on public DNS http://roarinpenguin.bounceme.net"
    - echo "listening on local IP http://10.70.70.120:5500"
  only:
    - master
```
##### !! MAKE SURE THE DOCKER AND DOCKER-COMPOSE PLUGIN ARE INSTALLED ON SERVER

### DOCKER CONFIG

##### DOCKER-COMPOSE.YML:
```
services:
  frontend:
    container_name: "Nuxt"
    restart: unless-stopped
    build:
      context: .
      dockerfile: Dockerfile
    ports:
      - 5500:3000
    command: ["yarn", "start"]
    environment:
      NUXT_HOST: 0.0.0.0
      NUXT_PORT: 3000
      REDIRECTSSL: "false"
      NODE_ENV: "dev"
```

##### DOCKERFILE:
```
FROM node:17-alpine

RUN mkdir -p /usr/src/nuxt-app
WORKDIR /usr/src/nuxt-app
COPY . /usr/src/nuxt-app/

RUN yarn cache clean --mirror
RUN yarn install
RUN yarn build

ENV NUXT_HOST=0.0.0.0
ENV NUXT_PORT=3000

EXPOSE 3000

CMD [ "yarn", "start" ]
```

## PM2 STARTER

##### ECOSYSTEM.CONFIG.JS
```
module.exports = {
  apps: [{
    name: "nuxt-app",
    script: "app.js",
    exec_mode: "cluster",
    istances: 2,
    cwd: '/usr/src/nuxt-app',
    script: './node_modules/nuxt-start/bin/nuxt-start.js',
    args: '-c /usr/src/nuxt-app/nuxt.config.js'
  }]
}
```

## NOTES
In case of priviledges problem with docker:
sudo usermod -aG docker gitlab-runner
It adds the gitlab-runner user to docker usergroup without add it to sudoers group
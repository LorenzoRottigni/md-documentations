# IMAGES

Docker images are seqeunces of instructions to start a service.
### You can add a Docker image to Docker registry using:

` sudo docker pull <image-name> ` 

### List of avaiable images: 

` sudo docker images ` or ` sudo docker images ls -a `

### Create your own image from a Dockerfile, example Dockerfile for NuxtJS deployment:

```
FROM node:11.13.0-alpine

# create destination directory
RUN mkdir -p /usr/src/nuxt-app
WORKDIR /usr/src/nuxt-app

# update and install dependency
RUN apk update && apk upgrade
RUN apk add git

# copy the app, note .dockerignore
COPY . /usr/src/nuxt-app/
RUN npm install

# build necessary, even if no static files are needed,
# since it builds the server as well
RUN npm run build

# expose 5000 on container
EXPOSE 5000

# set app serving to permissive / assigned
ENV NUXT_HOST=0.0.0.0
# set app port
ENV NUXT_PORT=5000

# start the app
CMD [ "npm", "start" ]
```

### Build image from Dockerfile:

```
cd /<Dockerfile location>
sudo docker build -t <new-image-name> .
sudo docker images
```

###Remove image from images list (if not used by a running container):
`sudo docker images rm <image-name>`

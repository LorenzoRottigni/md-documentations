## CONTAINERS

On Docker Virtual Boat you can add many containers, each containing one running service.
A Docker container is created and started by running instructions contained in a docker image.
Create a container:

`sudo docker run -d --name <new-container-name> -p <external-port>:<docker-port> <image-name>`

Get active containers list:

` sudo docker container ls `

All containers list:
` sudo docker container ls -a `

Stop container from running status:
` sudo docker container stop <container-name or container-hash>`

Remove container (status stopped) from containers list :
` sudo docker container rm <container-name or container-hash>`

Enter in container bash:
`docker exec --it <container-name> bash`

Run container .sh:
`docker exec --it <container-name> <.sh file>`

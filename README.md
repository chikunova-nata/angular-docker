## Docker commands

`docker build -t friendlyhello .`  Create image using this directory's Dockerfile

`docker run -p 4000:80 friendlyhello`  Run "friendlyname" mapping port 4000 to 80

`docker run -d -p 4000:80 friendlyhello`  Same thing, but in detached mode

`docker container ls`  List all running containers

`docker container ls -a`  List all containers, even those not running

`docker container stop <hash>`  Gracefully stop the specified container

`docker container kill <hash>`  Force shutdown of the specified container

`docker container rm <hash>`  Remove specified container from this machine

`docker container rm $(docker container ls -a -q)`  Remove all containers

`docker image ls -a`  List all images on this machine

`docker image rm <image id>`  Remove specified image from this machine

`docker image rm $(docker image ls -a -q)`  Remove all images from this machine

`docker login`  Log in this CLI session using your Docker credentials

`docker tag <image> username/repository:tag`  Tag <image> for upload to registry

`docker push username/repository:tag`  Upload tagged image to registry

`docker run username/repository:tag`  Run image from a registry


`docker system prune` 
WARNING! This will remove:
        - all stopped containers
        - all networks not used by at least one container
        - all dangling images
        - all build cache
        
`docker system prune --all --force --volumes`
WARNING! This will remove:
        - all stopped containers
        - all networks not used by at least one container
        - all volumes not used by at least one container
        - all images without at least one container associated to them
        - all build cache

prune can also be used on just one aspect:

`docker container prune` Remove all stopped containers
`docker volume prune` Remove all unused volumes
`docker image prune` Remove unused images

#### However, to get the right information for that command, you need to get a list of all container IDs.
`docker container ls -aq`

#### The full command for stopping all docker containers is now:
`docker container stop $(docker container ls -a -q)`

`docker container stop $(docker container ls -a -q) && docker system prune -a -f --volumes` A complete Docker system clean can now be achieved by linking this with the full prune command covered earlier in this post.

Similarly, you now know how to combine docker commands to just remove one aspect if you prefer. Pass a list of all the IDs to the associated remove command.

Containers `docker container rm $(docker container ls -a -q)`

Images `docker image rm $(docker image ls -a -q)`

Volumes `docker volume rm $(docker volume ls -q)`

Networks `docker network rm $(docker network ls -q)`

#### Docker-compose

`docker-compose up and down`
`docker-compose up` to create and start a container. In “detached” mode ( `-d` ), Compose exits after starting the containers, but the containers continue to run in the background. `docker-compose up -d rabbit-mq`

`docker-compose down` Stop and remove containers, networks, images, and volumes, eg `docker-compose down -v`. This has some useful options:
`--rmi type`
Remove images. Type must be one of:
`all`: Remove all images used by any service.
`local`: Remove only images that don't have a custom tag set by the `image` field.
`-v`, `--volumes`

Remove named volumes declared in the `volumes` section of the Compose file and anonymous volumes attached to containers.
`--remove-orphans`

Remove containers for services not defined in the Compose file
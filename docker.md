# Docker

## General commands

    docker container ls -a                              # List all containers, even those not running
    docker container stop <hash>                        # Gracefully stop the specified container
    docker container kill <hash>                        # Force shutdown of the specified container
    docker container rm <hash>                          # Remove specified container from this machine
    docker container rm $(docker container ls -a -q)    # Remove all containers
    docker image ls -a                                  # List all images on this machine
    docker image rm <image id>                          # Remove specified image from this machine
    docker image rm $(docker image ls -a -q)            # Remove all images from this machine
    docker login                                        # Log in this CLI session using your Docker credentials
    docker tag <image> username/repository:tag          # Tag <image> for upload to registry
    docker push username/repository:tag                 # Upload tagged image to registry
    docker run username/repository:tag                  # Run image from a registry

## Start container

    docker run --rm -it --name myubuntu ubuntu bash                                         # Spin up interactive bash (ubuntu)
    docker run --rm -it -v /Users/ehlf/Downloads:/Downloads -w /Downloads alpine:edge sh    # Spin up interactive shell (alpine), mount directory and set working dir

## Copy files

    docker cp ./some_file CONTAINER:/work           # copy file from localhost to container
    docker cp CONTAINER:/var/logs/ /tmp/app_logs    # copy files from container to local path

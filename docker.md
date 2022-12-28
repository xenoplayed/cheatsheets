#### General docker commands

    docker run --rm -it --name myubuntu ubuntu bash # spin up interactive shell in ubuntu with name myubuntu

#### Copy files

    docker cp ./some_file CONTAINER:/work           # copy file from localhost to container
    docker cp CONTAINER:/var/logs/ /tmp/app_logs    # copy files from container to local path

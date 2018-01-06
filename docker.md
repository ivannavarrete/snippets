  
### Example commands

    docker cp <container_id>:<container_path> <host_path>             copy file from container to host

    docker attach <container_name> --sig-proxy=false                  attach to a container, detatch with Ctrl-c

    docker rmi $(docker images -f "dangling=true" -q)                 remove dangling images

    docker rm $(docker ps -f "status=exited" -f "status=created" -q)  remove stopped containers



    docker ps -a                                                      list all containers

    docker image ls                                                   list all images


### docker network

Manage networks

    docker network ls                                                 list networks

    docker network inspect                                            display detailed info on one or more networks

    docker network connect [OPTIONS] NETWORK CONTAINER                connect a container to a network

    docker network disconnect [OPTIONS] NETWORK CONTAINER             disconnect a container from a network

    docker network create [OPTIONS] NETWORK                           create a network

    docker network rm                                                 remove a network

    docker network prune                                              remove unused networks



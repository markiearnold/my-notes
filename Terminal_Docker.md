# Terminal: Docker

## Remove docker volume 

```bash
docker volume ls
docker volume rm your_volume
```

## Prune

### Containers
This will remove:
* all stopped containers
* all networks not used by at least one container
* all dangling images
* all build cache
        
```bash
$ docker system prune
```

### Containers and Volumes
This will remove:
* all stopped containers
* all networks not used by at least one container
* all volumes not used by at least one container
* all images without at least one container associated to them
* all build cache

```bash
$ docker system prune -a --volumes
```

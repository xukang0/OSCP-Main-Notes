## **1. List all Docker containers**

```
# Currently running containers
docker ps

# ALL containers, including stopped ones
docker ps -a
```

You'll see something like:

```
CONTAINER ID   IMAGE          STATUS          NAMES
a1b2c3d4       postgres       Up 2 hours      db
e5f6g7h8       kali           Exited          kali-lab
```

## **2. List all Docker images**

Containers and images are different!

```
docker images -a
```

- **Container:** An instance created from an image.
- **Image:** The template used to create containers.

You can have multiple containers using the same image.

## **3. Remove containers you don't want**

Remove a specific container:

```
docker rm <container_id>
```

If it's currently running, stop it first:

```
docker stop <container_id>
docker rm <container_id>
```

Alternatively, force-remove it:

```
docker rm -f <container_id>
```

## **4. Remove Docker images you don't need**

First, remove containers using that image.

Then:

```
docker rmi <image_id>
```

## **5. Clean up unused Docker resources**

If you want to clean up unused containers and images:

```
# Remove stopped containers
docker container prune

# Remove unused images
docker image prune -a

# Remove unused networks
docker network prune

# Remove unused build cache
docker builder prune
```

Be careful

`docker image prune -a` removes all images not currently used by containers, including images you might want to reuse later.
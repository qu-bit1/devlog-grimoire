### [[images]] commands
```bash
docker build -t myimage .         # Build image from Dockerfile
docker images                     # List images
docker rmi image_name             # Remove image
docker pull image_name            # Download image from Docker Hub
docker push image_name            # Upload image to Docker Hub
```

### [[containers]] commands
```bash
docker run image_name             # Run container from image
docker run -it image_name bash    # Run interactively with bash
docker run -d image_name          # Run in background (detached mode)
docker run -p 8080:80 image       # Map 8080 on host to 80 in container
docker ps                         # List running containers
docker ps -a                      # List all containers (incl. stopped)
docker stop container_id          # Stop running container
docker start container_id         # Start stopped container
docker rm container_id            # Remove container
docker exec -it container_id bash # Exec command in running container
```

### [[volumes]] commands
```bash
docker volume create myvolume             # Create volume
docker run -v myvolume:/data image        # Mnts volume to /data in container
docker volume ls                          # List volumes
docker volume rm myvolume                 # Delete volume
```

### [[networks]] commands
```bash
docker network ls                         # List networks
docker network create mynet               # Create network
docker run --network=mynet image          # Run container in custom network
```

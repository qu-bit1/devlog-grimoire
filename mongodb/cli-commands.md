to start it in [[docker]]
## setup
1. `docker pull mongo` $\to$ this'll pull the mongo image
2. make a [[container]] out of the image 
```bash
docker run
-d 
--name mongo
-p free_host_port_here:27017
-e MONGO_INITDB_ROOT_USERNAME=username_here
-e MONGO_INITDB_ROOT_PASSWORD=pwd_here
mongo
```
3. enter the shell and then in mongosh's shell
```bash
docker exec -it name_of_the_container bash #enter the bash of the container
mongosh --username qubit --password pwd_here # enter the mongosh shell
```

---

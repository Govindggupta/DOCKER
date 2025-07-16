Volumes : used for persisting data . specially used for databases

to start a volume : 
docker volume create volume_databases
docker run -v volume_databases -p 8080:8080 mongo 
this starts the container with a volume 

networks 
docker network create network-name
 docker run -p 3000:3000 --network networkCheck --name backendapp test4:latest
this run the backend app with name backendapp and with the network networkCheck and port 3000 
 
 docker run --name mongodb2 -p 27017:27017 mongo:latest
this run the mongodb container with name mongodb2 and port 27017

and now backend server should request to the mongodb server by using the network name 


-e for environment variables
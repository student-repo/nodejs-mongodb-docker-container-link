# Simple nodejs and mongodb app using docker containers

This app use 2 docker containers which communicate each other (on the first container is nodejs and on the second mongodb database)


### To run mongodb server container:
```
docker run --name mongodbServer -d -p 27017:27017 mongo:latest
```

### To run nodejs with :
```
docker run --name nodejsApp -it --link mongodbServer:mongodbServer -w /app -v $(pwd):/app -p 4000:8000 node:latest /bin/bash
```


inside nodejsApp container do:

```
apt-get update
apt-get install vim
cat /etc/hosts
```
and copy mongodbServer host

```
vim /app/routes/index.js
```

and replace localhost to mongodbServer host

start app

```
cd /app
npm start
```

go to http://localhost:4000/ on your local machine



# Update:

You don't have to do nothing only: 

```
docker run --name mongodbServer -d -p 27017:27017 mongo:latest
docker run --name nodejsApp -it --link mongodbServer:mongodbServer -w /app -v $(pwd):/app -p 4000:8000 node:latest npm start
```



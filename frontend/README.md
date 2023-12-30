# Frontend Micro Service

In Frontend microservice it will connect to both the backend microservice helloservice and profile service.

```
cd frontend
```
Inside the frontend microservice create a .env file for dynamically changing the backend urls for both hello microservice and profile microservice

```
nano .env
```
```
REACT_APP_API_URL=$REACT_APP_API_URL
REACT_APP_API_HELLO=$REACT_APP_API_HELLO
```

Now let's containerise the frontend microservice
```
FROM node:18
WORKDIR /
COPY . /
ENV REACT_APP_API_URL $REACT_APP_API_URL
ENV REACT_APP_API_HELLO $REACT_APP_API_HELLO
RUN npm install
CMD ["npm", "run", "start"]
```

Lets build the Docker Image of the Frontend Microservice
```
docker build -t fe_svc .
```


docker run -it -e REACT_APP_API_URL=http://65.2.38.66:3001 -e REACT_APP_API_HELLO=http://65.2.38.66:3002/fetchUser -p 3000:3000 fe_svc





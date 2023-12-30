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





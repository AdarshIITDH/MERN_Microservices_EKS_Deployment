# SampleMERNwithMicroservices



git clone
cd backend/helloService

nano .env
PORT=$PORT

nano dockerfile
```
FROM node:18
WORKDIR /
COPY . /
RUN npm install
ENV PORT 3001
CMD ["node", "index.js","3001"]
```
```
docker build -t be_hellosvc:v1 -f dockerfile  .
```


cd backend/profileService

nano .env
PORT=$PORT

nano dockerfile
```
FROM node:18
WORKDIR /
COPY . /
RUN npm install
ENV PORT 3002
CMD ["node", "index.js","3002"]
```
```
docker build -t be_profilesvc:v1 -f dockerfile  .
```

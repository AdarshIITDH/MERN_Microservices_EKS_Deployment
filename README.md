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
docker build -t be_hellosvc:v1 .
```
```
docker run -it -e PORT=3001 -p 3001:3001 be_hellosvc:v1
```

cd backend/profileService

nano .env
PORT=$PORT
MONGO_URL=""


nano dockerfile
```
FROM node:18
WORKDIR /
COPY . /
RUN npm install
ENV PORT 3002
ENV MONGO_URL MONGO_URL
CMD ["node", "index.js","3002"]
```
```
docker build -t be_profilesvc:v1 .
```

```
docker run -it -e MONGO_URL="your mongo url" -p 3002:3002 be_profilesvc:v1
```

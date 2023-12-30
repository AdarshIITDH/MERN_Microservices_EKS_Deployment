
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
docker build -t be_hello_svc:latest .
```
```
docker run -it -e PORT=3001 -p 3001:3001 be_hello_svc:latest
```
```
public.ecr.aws/c3w1m1q2/be_hello_svc:latest
https://gallery.ecr.aws/c3w1m1q2/be_hello_svc
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
```
public.ecr.aws/c3w1m1q2/be_profile_svc:latest
https://gallery.ecr.aws/c3w1m1q2/be_profile_svc
```
```
http://<host ip>:3002/fetchUser
```

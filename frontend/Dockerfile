FROM node:18
WORKDIR /
COPY . /
ENV REACT_APP_API_URL $REACT_APP_API_URL
RUN npm install
CMD ["npm", "run", "start"]

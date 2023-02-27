# Week 2 — Distributed Tracing

Assignment

#Run the dockerfile CMD as an external script



#Push and tag a image to DockerHub (they have a free tier)

**tag: ojaysanya/frontend-react-js**

#Use multi-stage building for a Dockerfile build

```
# Stage 1: Build the app
FROM node:16.18 AS build

ENV PORT=3000

COPY . /frontend-react-js
WORKDIR /frontend-react-js
RUN npm install
EXPOSE ${PORT}

RUN npm run build


# Stage 2: Run the app
FROM node:14-alpine AS runtime
WORKDIR /frontend-react-js
COPY --from=build /frontend-react-js/dist ./dist
COPY package*.json ./
RUN npm install --only=production
EXPOSE 3000
CMD ["npm", "start"]

```
#Implement a healthcheck in the V3 Docker compose file

```
version: '3'
services:
  app:
    image: backend-flask:latest
    ports:
      - "3000:3000"
    healthcheck:
      test: ["CMD-SHELL", "curl --fail http://localhost:3000/health || exit 1"]
      interval: 30s
      timeout: 10s
      retries: 5

```
#Research best practices of Dockerfiles and attempt to implement it in your Dockerfile

#Learn how to install Docker on your localmachine and get the same containers running outside of Gitpod / Codespaces

#Launch an EC2 instance that has docker installed, and pull a container to demonstrate you can run your own docker processes. 

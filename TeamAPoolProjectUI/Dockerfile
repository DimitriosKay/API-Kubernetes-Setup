#use node image and set refference name as build
FROM node:10-alpine as build
#set working dir on container to build
WORKDIR /build
#copy files from local dir to working dir on container
COPY . .
#silently installs angular and dependancies
RUN NG_CLI_ANALYTICS=ci npm install -g @angular/cli
RUN NG_CLI_ANALYTICS=ci npm install
#builds angular project
RUN ng build

# makes new container for nginx
#use nginx image
FROM nginx:latest
#set work dir to app on container
WORKDIR /app
#copies from node build (defined above) to directory on nginx container
COPY --from=build /build/dist/TeamAPoolProjectUI .
#copies nginx file over to dependancies
COPY nginx.conf /etc/nginx/nginx.conf

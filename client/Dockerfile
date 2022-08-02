## BUILDER phase
# define the base image a "builder"
FROM node:16-alpine as builder

WORKDIR ./app

COPY package.json .
RUN npm install

COPY . .

RUN npm run build

## /app/build  <-- all the artifacts will end up here
## RUN phase
#define a new base image

#This is the ReactJS nginx - to serve static HTML files, the other one is for routing
FROM nginx
EXPOSE 3000

COPY ./nginx/default.conf /etc/nginx/conf.d/default.conf

# copy the final React build code from the BUILDER phase to the NGINX html
# folder (obtained from the NGINX container documentation)
COPY --from=builder /app/build /usr/share/nginx/html

#the nginx container already has a default command to automatically start NGINX up.
# stage1 as builder
FROM --platform=linux/amd64 node:18 as builder

# copy the package.json to install dependencies
COPY package.json package-lock.json ./

# Install the dependencies and make the folder
#RUN npm install && mkdir /react-ui && mv ./node_modules ./react-ui

WORKDIR /react-ui

COPY . .

# Build the project and copy the files
#RUN npm run build


FROM --platform=linux/amd64 nginx:1.14.2

#!/bin/sh

#COPY ./.nginx/nginx.conf /etc/nginx/nginx.conf
COPY nginx.conf /etc/nginx/nginx.conf

# This is added for certificates
COPY web.crt /usr/nginx/
COPY web.key /usr/nginx/

## Remove default nginx index page
RUN rm -rf /usr/share/nginx/html/*

EXPOSE 443
# EXPOSE 80   #This is the other part changed

ENTRYPOINT ["nginx", "-g", "daemon off;"]

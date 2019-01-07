# base image
FROM node:10.14.2

# set working directory
RUN mkdir /usr/src/app
WORKDIR /usr/src/app

# add `/usr/src/app/node_modules/.bin` to $PATH
ENV PATH /usr/src/app/node_modules/.bin:$PATH

# install and cache app dependencies
COPY ./front-end/package.json /usr/src/app/package.json
RUN npm install --silent
RUN npm install @angular/cli -g --silent

EXPOSE 4200 49153
# start app
CMD ["npm", "start"]

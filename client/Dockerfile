FROM node:16-alpine as builder

USER node
RUN mkdir -p /home/node/app
WORKDIR /home/node/app
COPY --chown=node ./package.json .
RUN npm install
COPY --chown=node . .
RUN npm run build

FROM nginx
EXPOSE 3000
# No need to copy over the deafult.conf from the builder phase
COPY ./nginx/default.conf /etc/nginx/conf.d/default.conf
COPY --from=builder /home/node/app/build /usr/share/nginx/html
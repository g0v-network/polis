ARG TAG=dev

FROM ghcr.io/g0v-network/polis-client-admin:${TAG}          as admin
FROM ghcr.io/g0v-network/polis-client-participation:${TAG}  as participation
FROM ghcr.io/g0v-network/polis-client-report:${TAG}         as report

FROM node:17.3.0-alpine

WORKDIR /app

COPY package*.json ./

RUN npm ci

COPY . .
COPY fs_config.template.json fs_config.json

RUN mkdir /app/build
COPY --from=admin         /app/build/ /app/build
COPY --from=participation /app/build/ /app/build
COPY --from=report        /app/build/ /app/build

EXPOSE 8080

CMD node --max_old_space_size=400 --gc_interval=100 --harmony app.js

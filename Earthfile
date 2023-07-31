VERSION 0.7
FROM node:13.10.1-alpine3.11
PROJECT 123-md-test/earthly-ci-demo
WORKDIR /js-example

deps:
    COPY package.json ./
    COPY package-lock.json ./
    RUN npm install
        RUN npm install
    # Output these back in case npm install changes them.
    SAVE ARTIFACT package.json AS LOCAL ./package.json
    SAVE ARTIFACT package-lock.json AS LOCAL ./package-lock.json

some-pipeline:
    PIPELINE
    TRIGGER push main
    TRIGGER pr main
    BUILD +build

build:
    COPY package.json ./
    COPY package-lock.json ./
    RUN npm install
    FROM +deps
    COPY src src
    RUN mkdir -p ./dist && cp ./src/index.html ./dist/
    RUN npx webpack
    SAVE ARTIFACT dist /dist AS LOCAL dist

docker2:
    FROM +deps
    COPY +build/dist ./dist
    EXPOSE 8080
    ENTRYPOINT ["/js-example/node_modules/http-server/bin/http-server", "./dist"]
    SAVE IMAGE js-example:latest

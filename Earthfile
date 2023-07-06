VERSION 0.7
PROJECT mirho/earthly-ci-demo


FROM alpine:3.17

hello-world-pipeline:
    PIPELINE
    TRIGGER push main
    TRIGGER pr main
    BUILD +hello-world

hello-world:
    RUN echo Hello world


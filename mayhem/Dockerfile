# Build Stage
FROM --platform=linux/amd64 ubuntu:22.04 as builder

## Install build dependencies.
RUN apt-get update && \
    DEBIAN_FRONTEND=noninteractive apt-get install -y clang cmake

## Add source code to the build stage.
ADD . /src

## Build
WORKDIR /src/mayhem/build
RUN cmake .. && cmake --build .

# Package Stage
FROM --platform=linux/amd64 ubuntu:22.04
COPY --from=builder /src/mayhem/build/csv-fuzz /csv-fuzz

# Set up fuzzing!
ENTRYPOINT []
CMD /csv-fuzz

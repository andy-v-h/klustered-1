FROM rust:1

COPY ./Cargo* /code/
COPY ./src/ /code/src/
WORKDIR /code

RUN cargo build --release

FROM rust:1 AS base

WORKDIR /workload
ENTRYPOINT [ "./httpd" ]

FROM base AS v1

COPY /assets/One.webm /workload/assets/video.webm
COPY --from=0 /code/target/release/workload /workload/httpd

FROM base AS v2

COPY /assets/Two.webm /workload/assets/video.webm
COPY --from=0 /code/target/release/workload /workload/httpd

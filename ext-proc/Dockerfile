## Multistage build
FROM golang:1.22.5@sha256:86a3c48a61915a8c62c0e1d7594730399caa3feb73655dfe96c7bc17710e96cf AS build
ENV CGO_ENABLED=0
ENV GOOS=linux

WORKDIR /src
COPY . .
RUN go mod download
RUN go build -o /ext-proc

## Multistage deploy
FROM gcr.io/distroless/static:nonroot@sha256:f41b84cda410b05cc690c2e33d1973a31c6165a2721e2b5343aab50fecb63441

WORKDIR /
COPY --from=build /ext-proc /ext-proc

ENTRYPOINT ["/ext-proc"]

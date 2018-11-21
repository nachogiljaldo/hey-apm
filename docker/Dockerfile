# from .. - docker build -f docker/Dockerfile .
FROM golang:1.11
RUN useradd hey

WORKDIR /go/src/github.com/elastic/hey-apm
RUN go get -u github.com/golang/dep/cmd/dep
COPY . .
RUN dep ensure
RUN CGO_ENABLED=0 GOOS=linux go build -a -installsuffix cgo -o hey-apm .

# https://github.com/golang/go/blob/release-branch.go1.9/src/crypto/x509/root_linux.go
COPY docker/ca-certificates.crt /etc/ssl/certs/
COPY docker/runner /runner
RUN cp /go/src/github.com/elastic/hey-apm/hey-apm /hey-apm

USER hey
ENTRYPOINT ["/runner"]
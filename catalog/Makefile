
GOPATH:=$(shell go env GOPATH)
MODIFY=Mgithub.com/micro/go-micro/api/proto/api.proto=github.com/micro/go-micro/v2/api/proto
SERVICE_SHORTNAME = catalog
BINARY_NAME=$(SERVICE_SHORTNAME)-service


.PHONY: proto
proto:
    protoc --proto_path=. --micro_out=${MODIFY}:. --go_out=${MODIFY}:. proto/$(SERVICE_SHORTNAME)/$(SERVICE_SHORTNAME).proto

.PHONY: build
build: proto
	go build -o $(BINARY_NAME) *.go

.PHONY: test
test:
	go test -v ./... -cover

.PHONY: docker
docker:
	docker build . -t $(BINARY_NAME):latest

.PHONY: tidy
tidy:
	go mod tidy

.PHONY: run
run: build
	./$(BINARY_NAME)

.PHONY: clean
clean:
	go clean
	rm -f $(BINARY_NAME)



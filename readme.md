# gateway

HTTP to gRPC gateway standalone. An example of go-zero gateway.

## Install

```shell
go install github.com/kevwan/gateway@latest
```

## Usage

Example config:

```yaml
Name: gateway
Host: localhost
Port: 8888
Upstreams:
  - Grpc:
      Etcd:
        Hosts:
          - localhost:2379
        Key: hello.rpc
    # protoset mode
    ProtoSet: hello.pb
    # Mapping is optional, auto mapping from annotations (google.api.http)
    Mapping:
      - Method: get
        Path: /pingHello/:ping
        RpcPath: hello.Hello/Ping
  - Grpc:
      Endpoints:
        - localhost:8081
    # no protoset, reflection mode
    # remember to enable reflection in server side
    Mapping:
      - Method: post
        Path: /pingWorld
        RpcPath: world.World/Ping
```

## Run the gateway

```shell
gateway -f config.yaml
```

## Give a Star! ⭐

If you like or are using this project, please give it a **star**. Thanks!

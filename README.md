# gateway

HTTP to gRPC gateway standalone.

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
    Mapping:
      - Method: get
        Path: /pingHello/:ping
        Rpc: hello.Hello/Ping
  - Grpc:
      Endpoints:
        - localhost:8081
    # no protoset, reflection mode
    # remember to enable reflection in server side
    Mapping:
      - Method: post
        Path: /pingWorld
        Rpc: world.World/Ping
```

## Run the gateway

```shell
gateway -f config.yaml
```
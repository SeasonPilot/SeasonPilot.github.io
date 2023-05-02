---
layout: post
categories: grpc
---
Question:

Reply in Chinese (Simplified).
The following is a search input in a search engine, giving useful content or solutions and as much information as you can related to it, use markdown syntax to make your answer more readable, such as code blocks, bold, list:
gRPC 可以提供 RESTful API 的代理或网关

Answer:

您好，这是必应。我将用简体中文回复您。😊

gRPC 是一种高性能、跨语言的远程过程调用（RPC）框架，它基于 HTTP/2 和 Protocol Buffers。gRPC 可以提供 RESTful API 的代理或网关，这意味着您可以使用 gRPC 定义您的服务，并通过 HTTP/JSON 访问它们。

要实现这一目的，您可以使用 gRPC-Gateway，它是 protoc 的一个插件。它可以读取 gRPC 服务定义，并生成一个反向代理服务器，将 RESTful HTTP API 转换为 gRPC。这个服务器是根据您的服务定义中的 google.api.http 注解生成的。

gRPC-Gateway 的优点是：

- 它可以让您使用一种语言（Protocol Buffers）定义您的服务和 API。
- 它可以让您利用 gRPC 的高效、双向流和元数据等特性。
- 它可以让您为不支持 gRPC 的客户端提供 HTTP/JSON 接口。
- 它可以让您与现有的 RESTful 服务集成。

gRPC-Gateway 的缺点是：

- 它需要额外的编译步骤和依赖项。
- 它可能会增加网络延迟和开销。
- 它可能会丢失一些 gRPC 的原生功能，如错误码和拦截器。

要使用 gRPC-Gateway，您需要：

- 在您的服务定义中添加 google.api.http 注解，指定 HTTP 方法和路径。
- 使用 protoc 和 grpc-gateway 插件生成反向代理代码。
- 在您的服务器端启动 gRPC 服务器和反向代理服务器。
- 在您的客户端使用 HTTP/JSON 调用反向代理服务器。

下面是一个简单的示例：

假设您有一个名为 hello.proto 的文件，定义了一个 HelloService，它有一个 SayHello 方法，接受一个 HelloRequest，并返回一个 HelloResponse：

```protobuf
syntax = "proto3";

package hello;

import "google/api/annotations.proto";

message HelloRequest {
  string name = 1;
}

message HelloResponse {
  string message = 1;
}

service HelloService {
  rpc SayHello (HelloRequest) returns (HelloResponse) {
    option (google.api.http) = {
      get: "/hello/{name}"
    };
  }
}
```

注意 google.api.http 注解，它指定了 SayHello 方法对应的 HTTP GET 请求路径。

然后，您可以使用 protoc 和 grpc-gateway 插件生成 gRPC 代码和反向代理代码：

```bash
protoc -I . --go_out=plugins=grpc:. hello.proto
protoc -I . --grpc-gateway_out=logtostderr=true:. hello.proto
```

这将在同一目录下生成 hello.pb.go 和 hello.pb.gw.go 文件。

接下来，您可以在 main.go 文件中实现 HelloService 接口，并启动 gRPC 服务器和反向代理服务器：

```go
package main

import (
	"context"
	"log"
	"net"

	"github.com/golang/glog"
	"google.golang.org/grpc"
	"google.golang.org/grpc/reflection"

	gw "hello/hello"

	"net/http"

	"github.com/grpc-ecosystem/grpc-gateway/runtime"
)

type server struct{}

func (s *server) SayHello(ctx context.Context, in *gw.HelloRequest) (*gw.HelloResponse, error) {
	return &gw.HelloResponse{Message: "Hello " + in.Name}, nil
}

func startGRPCServer() {
	lis, err := net.Listen("tcp", ":9090")
	if err != nil {
		log.Fatalf("failed to listen: %v", err)
	}
	s := grpc.NewServer()
	gw.RegisterHelloServiceServer(s, &server{})
	reflection.Register(s)
	if err := s.Serve(lis); err != nil {
		log.Fatalf("failed to serve: %v", err)
	
\-
\[1]: [gRPC-gateway — REST API and gRPC API in the single definition](https://faun.pub/grpc-gateway-rest-api-and-grpc-api-in-the-single-definition-7cb0957bda68)
\[2]: [grpc-ecosystem/grpc-gateway - Github](https://github.com/grpc-ecosystem/grpc-gateway)
\[3]: [gRPC-Gateway | gRPC-Gateway Documentation Website](https://grpc-ecosystem.github.io/grpc-gateway/)
\[4]: [RESTful API Gateway with gRPC - Techdozo](https://techdozo.dev/restful-api-gatewat-with-grpc/)
\[5]: [API Gateway for gRPC microservices | gRPC Guide](https://grpcguide.com/building-api-gateway-for-grpc)

<hr/>


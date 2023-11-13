# grpc-node-typescript-example
A simple Node application with gRPC communication. Written with Typescript to ensure correct typing in client and server. For simplicity purpose there is only one function `login` shared between client and server.
The gRPC client and server communicate over a network using the gRPC protocol, which is built on top of HTTP/2. The client makes a remote procedure call (RPC) to the server by calling a method on a client-side stub. This method corresponds to a method defined in the server's service definition (the `auth.proto` file). The client and server use Protocol Buffers (protobuf) to serialize and deserialize the method's input and output data.

Here's a step-by-step breakdown:

1. The client creates a `LoginRequest` object and calls the `login` method on the `AuthServiceClient` stub, passing in the `LoginRequest` and a callback function.

2. The `AuthServiceClient` serializes the `LoginRequest` to a protobuf message and sends it to the server over a HTTP/2 connection.

3. The server receives the protobuf message, deserializes it back into a `LoginRequest` object, and calls the `login` function with this object.

4. The `login` function checks the `LoginRequest` against its list of users, creates a `LoginResult`, and calls the callback function with this result.

5. The server serializes the `LoginResult` to a protobuf message and sends it back to the client over the HTTP/2 connection.

6. The client receives the protobuf message, deserializes it back into a `LoginResult` object, and calls the callback function with this object.

gRPC has several advantages over traditional RESTful APIs:

- **Performance**: gRPC uses HTTP/2, which is faster and more efficient than HTTP/1.1 used by most RESTful APIs. HTTP/2 supports multiplexing, bidirectional streaming, and flow control.

- **Strongly-typed interfaces**: gRPC uses protobuf, which enforces a strong typing system. This can help catch bugs at compile time that would only be caught at runtime with a RESTful API.

- **Bi-directional streaming**: gRPC supports streaming requests and responses, while REST is typically request/response.

- **Language agnostic**: gRPC supports many different languages, making it easy to create microservices in any language that can interoperate with each other.

- **Tooling**: gRPC provides tools like `protoc` to automatically generate client and server code from service definitions, reducing the amount of boilerplate code you have to write.

## Running server
```
npm run server
```

## Running client
```
npm run client
```

## Compiling proto file
After any change in `auth.proto` file it needs to be recompiled by running the following command:
```
protoc --plugin=protoc-gen-ts_proto=.\node_modules\.bin\protoc-gen-ts_proto.cmd --ts_proto_out=. ./protos/auth.proto --ts_proto_opt=outputServices=grpc-js,env=node,esModuleInterop=true
```

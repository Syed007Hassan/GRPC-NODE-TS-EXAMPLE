# grpc-node-typescript-example
A simple Node application with gRPC communication. Written with Typescript to ensure correct typing in client and server. For simplicity purpose there is only one function `login` shared between client and server.

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
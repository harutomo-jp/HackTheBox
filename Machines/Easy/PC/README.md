# HackTheBox - PC
<p align="center"><b>rating: EASY</b></p>

Pathway to foothold, found gRPC running on port 50051

resources for understanding gRPC:

https://grpc.io/docs/what-is-grpc/
https://grpc.io/docs/languages/go/basics/
https://grpc.io/docs/guides/


For communicating with gRPC in terminal:
https://github.com/fullstorydev/grpcurl

command to list services available:
grpcurl -plaintext 10.10.11.214:50051 list

SimpleApp
grpc.reflection.v1alpha.ServerReflection

list the methods available for the SimpleApp service:
grpcurl -plaintext 10.10.11.214:50051 list SimpleApp

SimpleApp.LoginUser
SimpleApp.RegisterUser
SimpleApp.getInfo


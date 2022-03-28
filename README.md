# Introduction

Introduction of Distributed-Network-Disk.

New planning architecture (**Don't Repeat Yourself**, use Minio):

```mermaid
graph LR;
Client-Web[Client-Web]--S3-Link-->Minio-Node1[Minio-Node1]
Client-Web[Client-Web]--S3-Link-->Minio-Node2[Minio-Node2]
Client-Web[Client-Web]--S3-Link-->Minio-Node3[Minio-Node3]
Client-WebDAV[Client-WebDAV]--S3-Link-->Minio-Node1[Minio-Node1]
Client-WebDAV[Client-WebDAV]--S3-Link-->Minio-Node2[Minio-Node2]
Client-WebDAV[Client-WebDAV]--S3-Link-->Minio-Node3[Minio-Node3]
User[User]--WebDAV-->Client-WebDAV[Client-WebDAV]
User[User]--Web-->Client-Web[Client-Web]
```

Old architecture:

```mermaid
graph LR;
Client-Web[Client-Web]-.Restful-Control-Link.->Store-Manager[Store-Manager]
Client-Web[Client-Web]--WS-Data-Link-->Store-Node1[Store-Node1]
Client-Web[Client-Web]--WS-Data-Link-->Store-Node2[Store-Node2]
Client-Web[Client-Web]--WS-Data-Link-->Store-Node3[Store-Node3]
Store-Node1[Store-Node1]-.Restful-Control-Link.->Store-Manager[Store-Manager]
Store-Node2[Store-Node2]-.Restful-Control-Link.->Store-Manager[Store-Manager]
Store-Node3[Store-Node3]-.Restful-Control-Link.->Store-Manager[Store-Manager]
Store-Manager[Store-Manager]-.SQL.->PostgreSQL[PostgreSQL]
Client-WebDAV[Client-WebDAV]-.Restful-Control-Link.->Store-Manager[Store-Manager]
Client-WebDAV[Client-WebDAV]--WS-Data-Link-->Store-Node1[Store-Node1]
Client-WebDAV[Client-WebDAV]--WS-Data-Link-->Store-Node2[Store-Node2]
Client-WebDAV[Client-WebDAV]--WS-Data-Link-->Store-Node3[Store-Node3]
User[User]--WebDAV-->Client-WebDAV[Client-WebDAV]
User[User]--Web-->Client-Web[Client-Web]
```

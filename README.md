# Introduction

Introduction of Distributed-Network-Disk.

New planning architecture (**Don't Repeat Yourself**, use Minio):

```mermaid
graph LR;
Client-Web[Client-Web]--S3-Link-->Minio-MetaNode[Minio-MetaNode]
Client-WebDAV[Client-WebDAV]--S3-Link-->Minio-MetaNode[Minio-MetaNode]
Client-Web[Client-Web]--S3-Link-->Minio-DataNode1[Minio-DataNode1]
Client-Web[Client-Web]--S3-Link-->Minio-DataNode2[Minio-DataNode2]
Client-Web[Client-Web]--S3-Link-->Minio-DataNode3[Minio-DataNode3]
Client-WebDAV[Client-WebDAV]--S3-Link-->Minio-DataNode1[Minio-DataNode1]
Client-WebDAV[Client-WebDAV]--S3-Link-->Minio-DataNode2[Minio-DataNode2]
Client-WebDAV[Client-WebDAV]--S3-Link-->Minio-DataNode3[Minio-DataNode3]
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

## MetaNode

Json files in MetaNode, which are used to store the information of the data nodes and file lists.

Var: Bucket name and Metanode uri.

```json
# nodelist.json
{
    string(id): {
        "name": string(node name),
        "url":  string(node url),
    }
}
```

```json
# filelist.json
{
    string(path+filename): {
        "shards": [
            1,
            2,
            ...
        ],
        "modified": int(unix timestamp),
        "size":  int(bytes),
    }
}
```

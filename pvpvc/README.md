# Persistent Volume ve Persistent Volume Claim
**pv ve pvc** konusuyla ilgili dosyalara buradan erişebilirsiniz.

***
NFS Server 
```
$ docker volume create nfsvol

$ docker network create --driver=bridge --subnet=10.255.255.0/24 --ip-range=10.255.255.0/24 --gateway=10.255.255.10 nfsnet

$ docker run -dit --privileged --restart unless-stopped -e SHARED_DIRECTORY=/data -v nfsvol:/data --network nfsnet -p 2049:2049 --name nfssrv ozgurozturknet/nfs:latest

```
***
Persistent Volume objelerinin listelenmesi

```
$ kubectl get pv
```
***
Persistent Volume objelerinin silinmesi

```
$ kubectl delete pv "pv_ismi

Ör: kubectl delete pv mypv
```
***
Persistent Volume Claim objelerinin listelenmesi

```
$ kubectl get pvc
```
***
Persistent Volume objelerinin silinmesi

```
$ kubectl delete pvc "pvc_ismi

Ör: kubectl delete pvc mypvc
```
***
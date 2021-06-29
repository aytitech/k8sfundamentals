# Secret ve Configmap
**secret ve configmap** konusuyla ilgili dosyalara buradan erişebilirsiniz.
***
Imperative olarak Secret objelerinin oluşturulması

```
$ kubectl create secret generic "secret_ismi" --from-literal="anahtar"="değer" --from-file="anahtar"="değerin_okunacagi_dosya" --from-file="değerin_okunacagi_dosya"

Ör: kubectl create secret generic mysecret --from-literal=db_server=db.example.com --from-file=db_server=server.txt --from-file=config.json
```
***
Secret objelerinin listelenmesi

```
$ kubectl get secret
```
***
Secret objelerinin silinmesi

```
$ kubectl delete secret "secret_ismi"

Ör: kubectl delete secret my-secret
```
***
Imperative olarak ConfigMap objelerinin oluşturulması

```
$ kubectl create configmap "configmap_ismi" --from-literal="anahtar"="değer" --from-file="anahtar"="değerin_okunacagi_dosya" --from-file="değerin_okunacagi_dosya"

Ör: kubectl create configmap myconfigmap--from-literal=db_server=db.example.com --from-file=db_server=server.txt --from-file=config.json
```
***
ConfigMap objelerinin listelenmesi

```
$ kubectl get configmap
```
***
ConfigMap objelerinin silinmesi

```
$ kubectl delete configmap "configmap_ismi"

Ör: kubectl delete configmap my-configmap
```
***
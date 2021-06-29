# Service
**service** konusuyla ilgili dosyalara buradan erişebilirsiniz.
***
Service objelerinin listelenmesi

```
$ kubectl get service
```
***
Bir deployment'in expose edilmesi "imperative olarak service objesinin oluşturulması"

```
$ kubectl expose deployment "deployment_ismi" --type="service_tipi" --name="servis_ismi"

Ör: kubectl expose deployment backend --type=ClusterIP --name=backend
```
***
***
Service objelerinin silinmesi

```
kubectl delete service "servis_ismi"

Ör: kubectl delete service backend
```
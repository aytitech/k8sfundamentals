# Deployment
**deployment** konusuyla ilgili dosyalara buradan erişebilirsiniz.
***
Imperative yöntemle Deployment oluşturma.

```
$ kubectl create deployment "deployment_ismi" --image="image_ismi" --replicas="replika_adeti"

Ör: kubectl create deployment firstdeployment --image=nginx:latest --replicas=2
```
***
Deployment listeleme.

```
$ kubectl get deployment
```
***
Deployment silme.

```
$ kubectl delete deployment "deployment_ismi"

Ör: kubectl delete deployment firstdeployment
```
***
Deployment içerisindeki imajı güncelleme.

```
$ kubectl set image deployment/"deployment_ismi" "container_ismi"="yeni_imaj"  

Ör: kubectl set image deployment/firstdeployment nginx=httpd:alpine
```
***
Deployment replika sayısını değiştirme "Scaling"

```
$ kubectl scale deployment "deployment_ismi" --replicas="istenilen_replika_adeti"

Ör: kubectl scale deployment firstdeployment --replicas=5
```
***
Deployment yapılan son değişikliğin geri alınması.

```
$ kubectl rollout undo deployment "deployment_ismi"

Ör: kubectl rollout undo deployment firstdeployment
```
***
Deployment yapılan değişikliklerin kaydının tutulması için "--record" opsiyonu kullanılır. 

```
Ör: kubectl set image deployment rolldeployment nginx=httpd:alpine --record=true 
```
***
Deployment yapılan değişikliklerin listelenmesi.

```
$ kubectl rollout history deployment "deployment_ismi"

Ör: kubectl rollout history deployment rolldeployment
```
***
Deployment yapılan değişikliklerin izlenmesi.

```
$ kubectl rollout status deployment "deployment_ismi"

Ör: kubectl rollout status deployment rolldeployment 
```
***
Deployment üstünde yapılan değişikliklerin durdurulması.

```
$ kubectl rollout pause deployment "deployment_ismi"

Ör: ➜ kubectl rollout pause deployment rolldeployment
```
***
Durdurulan rollout'un devam ettirilmesi. 

```
$ kubectl rollout resume deployment "deployment_ismi"

Ör: ➜ kubectl rollout resume deployment rolldeployment
```
***
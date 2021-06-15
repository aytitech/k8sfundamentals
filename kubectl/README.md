# kubectl
## **kubectl** konusuyla ilgili dosyalara buradan erişebilirsiniz.
***

kubectl config dosyası ```$HOME/.kube/``` konumunda bulunan ```config``` isimli dosyadır.

Ör: Linux ve Mac ```/home/ozgurozturknet/.kube/config``` | Windows ```C:\Users\ozgur\.kube\config```
***

Mevcut kubectl client ve Kubernetes cluster versiyonlarını görmek için:
```
$ kubectl version
```
***
Config dosyasında tanımlı context'leri listeleme:
```
kubectl config get-contexts
```
***
Seçili durumdaki context'i gösterme.
```
$ kubectl config current-context
```
***
config dosyasında tanımlı contextlerden bir tanesini geçerli context olarak atama. 
```
$ kubectl config use-context "context_ismi"
```
***
Geçerli context'de tanımlı Kubernetes cluster hakkında bilgi edinme.
```
$ kubectl cluster-info
```
***
Varsayılan namespace'de bulunan objeleri listeleme
```
$ kubectl get "obje_tipi"

Ör: kubectl get pods
```
***
Varsayılan namespace'de bulunan tek bir objenin özelliklerini listeleme
```
$ kubectl get "obje_tipi" "obje_ismi"

Ör: kubectl get pods testpod
```
***

Varsayılan dışında başka bir namespace'de bulunan objeleri listeleme (_-n "namespace_adi" ekiyle komutların belirtilen namespace üstünde çalıştırılması sağlanmaktadır_)
```
$ kubectl get "obje_tipi" -n "namespace_adi"

Ör: kubectl get pods -n kube-system
```
***
Tüm namespace'lerde bulunan objeleri listeleme (_--all-namespaces ya da kısaca -A eki komutun tüm namespace'leri kapsamasını sağlar_)
```
$ kubectl get "obje_ismi" --all-namespaces

Ör: kubectl get pods --all-namespaces
```
***
kubectl komutlarının geri döndürdüğü çıktı kısıtlı bilgiler içerir ve plain-text olarak döner. **-o** opsiyonuyla bu çıktı belirtilen başka bir formatta döndürülebilir. Örneğin **-o yaml** opsiyonu çıktının yaml formatında döndürülmesini sağlar. Kullanılabilecek opsiyonlar:
- ```-o yaml``` Yaml formatında çıktı döndürür.
- ```-o json``` Json formatinda çıktı döndürür.
- ```-o wide``` Plain-text fakat daha çok bilgi içerir.
- ```-o jsonpath=<template>``` Jsonpath ifadesinde tanımlanan alanları döndürür.
- ```-o name``` Sadece isimleri döndürür. 
- ```-o custom-columns=<spec>``` Comma-seperated olarak belirtilen kolonlardan bir table döndürür. 
```
$ kubectl get "obje_tipi" "obje_ismi" -o "opsiyon_ismi"

Ör: kubectl get pods -o wide
```
***
Kubernetes obje tipleriyle ilgili detaylı bilgi edinmek..
```
$ kubectl explain "obje_tipi"

Ör: kubectl explain pods
```
***
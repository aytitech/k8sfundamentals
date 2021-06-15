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
$ kubectl config use-context <|context_ismi|>
```
***
Geçerli context'de tanımlı Kubernetes cluster hakkında bilgi edinme.
```
$ kubectl cluster-info
```
***
Varsayılan namespace'de bulunan pod'ları listeleme
```
$ kubectl get pods
```
***
Varsayılan dışında başka bir namespace'de bulunan pod'ları listeleme "-n <|namespace_adi |> ekiyle komutların belirtiler namespace üstünde çalıştırılması sağlanmaktadır" 
```
$ 
```
***

```
$ 
```
***

```
$ 
```
***

```
$ 
```
***














```
$ 
```
***
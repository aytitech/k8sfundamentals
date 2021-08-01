## kubectl config

* kubectl aracı bağlanacağı Kubernetes cluster bilgilerine config dosyaları üzerinden erişir,
* Config dosyasında `context` ile  bağlanılacak cluster bilgisini ve kullanıcı bilgilerini autherization için oluşturur. 
* Varsayılan olarak `~/.kube/config` dosyasına bakar

Komutlar:
```
kubextl config #sub command leri gösterir
kubectl config get-contexts # mevcut contextleri listeler
kubectl config current-context #kullanılan context i söyler
kubectl config use-context "minikube" #minikube context ini kullan diyoruz



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
```

## kubectl komutları

* kubectl folder ını kontrol edebilirsiniz.
* kubectl [fiil (getir/sil/uygula gibi)] [nesne(pod/container gibi)] [spesifik obje ismi]
* kubectl komutları context te set edilmiş namespace üzerine uygulanır. Ama namespace set etmek istiyorsak `-n` ile name-space set edebiliriz. Tüm namespace ler için ise: `-A` bütün namespace lere uygular.


### yaml

* dekleratif veri formatı, alternatifi json/xml gibi

```
#hangi api de tanımlanıyor, her obje bir api de bakılacak? `kubectl explain pod` ile görebiliriz.
apiVersion: v1

#ne oluşturacağım? pod mu deployment mı ..?
kind: Pod

#obje ile ilgili unique bilgiler bulunur. dictionary dir. Objeyi betimler
metadata:
  name: firstpod
  labels:
    app: frontend
# her obje için farklı bilgiler gireriz, pod için mesela oluşturulacak container ların bilgilerini girebiliriz.
spec:
```

* yaml dosyalarının kullanımı ile aynı işi tekrar tekrar uygulamak yerine konfigürasyonu kullanırız,
* güncelleme işlemlerini daha rahat yapabiliriz.

* kubectl edit pods [pod ismi] ile de editleme ve hızlı apply sağlanabilir ama çok kullanılmaz.
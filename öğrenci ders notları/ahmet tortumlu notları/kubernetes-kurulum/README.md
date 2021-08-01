* rest çağrıları ile kubernetes api ile iletişime geçebiliriz,
* GUI ile de yönetimi gerçekleştirebiliriz,
* kubectl kubernetes resmi cli aracıdır. K8s cluster oluşturmadan önce kubectl kurlumunu sağlamalı sonra cluster ile bağlanılmalı.

### minikube

* kendi bilgisayarımızda single node cluster sağlar, farklı add-on lar mümkün.
* Eğitim de minikube üzerinden devam edecek
* Kaynak: [https://minikube.sigs.k8s.io/docs/start/](https://minikube.sigs.k8s.io/docs/start/)
* Minikube download kontrol: 
```
minikube status
```
* Minikube başlatmak için: (Eğer docker kullanacaksanız, farklı bir driver için `--driver=` opsiyonunu kullanmalısınız.)
```
minikube start
```

Şimdi bir k8s cluster ayağa kalkmış oldu. Tekrar status kontrolünü yapabilirsiniz:

```
minikube status
```

* Cluster ı silmek istediğinizde de :

```
minikube delete
```

yapabilirsiniz.

* Silme ama durdur demek için de :
```
minikube stop
```
komutunu kullanabilirsiniz.


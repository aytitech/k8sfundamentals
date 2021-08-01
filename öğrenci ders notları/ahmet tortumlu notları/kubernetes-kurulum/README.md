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

### pod yaşam döngüsü

* kullanıcı yaml ile kubernetes cluster a api üzerinden komutu yollar,

* etcd bu pod için veriyi panoya yazar,

* bu aşamadan itibaren pod oluşturulmuştur ve pending aşamasına gider.

* sched etcd gözlerken atanmamış bir pod görür ve uygun node u seçer ve node bilgisini pod a ekler.

* Eğer pod pending te kaldıysa sched node atamamış demektir. Bunun için node üzerinde kaynak kullnaımlarını kontrol edebiliriz.

* kubelet gelen pod u görür ve konteynırları oluşturmaya başlar, bunun için imajı indirir.

>> Gelebilecek hata: imagePullBackOff: imaj çekilemiyor (authentication sağlanamamış veya image ismi düzgün sağlanamamış olabilir.)

>> container içerisinde ana ugyulama kapanırsa container da kapanır.

* container içerisinde RestartPolicy tanımlanır. Default Always, diğer seçenekler On-failure ve Never.

>> CrashLoopBackOff: Pod eğer başarılı çalışmadı ve Restart Always set edildiyse, bir süre çöküş ve tekrar kaldırma sonraında sonrasında beş dakikada bir restart ederken CrashLoopBackOff state ine gelir.
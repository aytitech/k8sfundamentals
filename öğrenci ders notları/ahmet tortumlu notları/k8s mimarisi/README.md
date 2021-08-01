* Kubernetes hem *beyan temelli yapılandırma* hem de *otomasyonu* kolaylaştıran, container iş yüklerini ve hizmetleri yönetmek için oluşturulmuş, taşınabilir ve genişletilebilir açık kaynaklı bir platformdur.

* kubernetes konteyner iş yüklerini yöneten sektörün en büyük platformu.

* kubernetes her işi yapan tek bir uygulamadan oluşmuyor, majör özellikler modüllere bölünmüş durumda. Bu sayede her modül kendi işine odaklanıyor. Ayrıca bu modüllerin genişletilmesi ve özel çözümler geliştirilmesine de imkan sağlıyor.

* Cluster üzerinde nasıl yapılacağını değil ne istediğimizi tarif ediyoruz. Marangoza ne yapacağını söylüyoruz, nasıl yapılacağını değil. imperatif yöntem yerine *dekleratif/beyan* yöntemi kullanılıyor.

* Oluşturulan yapı istediğimizin dışına çıktığında otamatik bu yapıya dönderiliyor: *otomasyon*

## Kubernetes Komponentleri

* Yönetim ve üretim örneği:

1. Sol tarafta control plane/master nodes, 
Resepsiyon:API Server
Pano: etcd veri deposu
vardiya amirliği: controller manager
üretim planlama: schedular componenti (sched)

2. Sağ tarafta da Worker Nodes/Data Plane,
Makineler: Container ların koştuğu worker nodelar,
Usta başları: worker nodelarda çalışan kubelet,
Lojistik elemanımız: network iletişimini sağlayan kube proxy component lerini temsil ediyor(k-proxy)

### kube-apiserver

* Dış dünya ile iletişimin olduğu ortak noktadır. Tüm iletişim apiserver üzerinden gerçekleşir.

* Tüm komponentler api server üzerinden iletişimi kurar,

* Kaynak oluşturma isteklerinin api doğrulamasından sorumludur.

### etcd

* Tüm cluster yapısı, metadata verilerinin tutulduğu key-value veri deposudur.

* Cluster mevcut durumunu üzerinde barındırır.

* etcd ile iletişim kubeapi server üzerinden yapılır.

### kube-schedular

* Yeni oluşturulan veya atamsı yapılması gereken bir podun uygun node atamasının yapıldığı yerdir.

* Kaynak gereksinimini göz önünde bulundurur.

### kube controller manager (c-m)

* etcd yi api server üzerinden izleyerek cluster ın istenilen durumda olmasını sağlar(kaynak üretilmesi/silinmesi gerekiyorsa aksiyon alır).

### worker node

* Container run time,
* kubelet: api server aracılığıyla etcd kontrol eder, ve schedular tarafından bulunduğu node üzerinden çalışması gereken bir pod belirtildiyse o sistemde kubelet oluşturur.
* k-proxy: oluştuurlan podların network proxy hizmetini görür.

## Kubernetes yayın döngüsü

* kubernetes versiyonlarının patch alma sıklığı göz önünde bulundurulduğunda kubernetes in bir versiyonunu kullanıyorsak en geç 12 ayda bir güncellenmesi gerekiyor.

* Kubernetes kaynakları:
[https://cncf.io](https://cncf.io)
[https://kubernetes.io/docs](https://kubernetes.io/docs)
[https://github.com/kubernetes/kubernetes](https://github.com/kubernetes/kubernetes)
# Pod
**pod** konusuyla ilgili dosyalara buradan erişebilirsiniz.
***
Imperative yöntemle pod oluşturma.

```
$ kubectl run "pod_ismi" --image="image_ismi" --restart=Never

Ör: kubectl run firstpod --image=nginx --restart=Never
```
***
Bir objenin ayrıntılı özelliklerini görmek. 
```
$ kubectl describe "obje_tipi" "obje_ismi"

Ör: kubectl describe pods firstpod
```
***
Bir pod objesinin loglarını görüntüleme. _(-f opsiyonu çıktıya yapışmanızı ve anlık olarak üretilen logları görmenizi sağlar)_
```
$ kubectl logs "pod_ismi"

Ör: kubectl logs firstpod
Ör: kubectl logs -f firstpod
```
***
Pod'da komut çalıştırma. _(Eğer pod içerisinde birden fazla container varsa **-c "container_ismi"** opsiyonu ile komutun çalıştırılması istenilen container belirtilebilir)_
```
$ kubectl exec "pod_ismi" -- "komut"

Ör: kubectl exec firstpod -- printenv
Ör: kubectl exec firstpod -c container1 --printenv
```
***
Pod'a shell bağlantısı oluşturma. _(Eğer pod içerisinde birden fazla container varsa **-c "container_ismi"** opsiyonu ile komutun çalıştırılması istenilen container belirtilebilir)_
```
$ kubectl exec -it "pod_ismi" -- "shell_konumu-yada-komutu"

Ör: kubectl exec -it firstpod -- /bin/sh
Ör: kubectl exec -it firstpod -c container1 -- /bin/sh
```
***
Bir Kubernetes objesini silme. 
```
$ kubectl delete "obje_tipi" "obje_ismi"

Ör: kubectl delete pods firstpod
```
***
Json ya da Yaml formatında hazırlanmış bir konfigurasyon dosyası aracılığıyla yeni obje oluşturma. 
```
$ kubectl apply -f "dosya_yolu/dosya_ismi"

Ör: kubectl apply -f ./pod1.yaml
```
***
Oluşturulan objeyi dosya kullanarak silme
```
$ kubectl delete -f "dosya_yolu/dosya_ismi"

Ör: kubectl delete -f ./pod1.yaml
```
***
Label ve port konfigurasyonlarını da ekleyerek bir pod oluşturma. 
```
$ kubectl run "pod_ismi" --image="image_ismi" --port="port_numarası" --labels"anahtar:değer_eşlenikleri" --restart=Never

Ör: kubectl run secondpod --image=nginx --port=80 --labels="app=front-end,team=developer" --restart=Never
```
***
Cluster'da bulunan bir Kubernetes objesini varsayılan text editörü ile açarak özelliklerini güncelleme. 
```
$ kubectl edit "obje_tipi" "obje_ismi"

Ör: kubectl edit pods firstpod
```
***
kubectl komutları sonucu oluşan çıktıyı tek seferlik görmek yerine değişiklikleri izleyebilme imkanına **-w** opsiyonu ile kavuşuruz _(linux dünyasındaki **watch** komutunun yaptığı işin bir benzerini **-w** opsiyonu sağlar)_
```
$ kubectl "komut" -w

Ör: kubectl get pods -w
```
***
kubectl'in çalıştırıldığı bilgisayar üzerinden cluster'da bulunan bir objeye tünel açılarak bağlantı kontrolü yapılması "detaylarına network konusunda geleceğiz"
```
$ kubectl port-forward "obje_tipi"/"obje_ismi" "local_port":"hedef_port"

Ör: kubectl port-forward pod/multicontainer 8080:80
```
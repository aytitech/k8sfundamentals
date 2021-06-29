# Taint ve Toleration
**taint ve toleration** konusuyla ilgili dosyalara buradan erişebilirsiniz.
***
Node'lara taint ekleme.
```
$ kubectl taint node "node_ismi" "anahtar=değer:eylem"

Ör: kubectl taint node minikube platform=production:NoSchedule
```
***
Node'lardan taint kaldırma.
```
$ kubectl taint node "node_ismi" "anahtar-"

Ör: kubectl taint node minikube platform-
```
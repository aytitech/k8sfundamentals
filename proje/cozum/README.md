**1:** 5 node'lu "1 Master + 4 Worker Node" bir Kubernetes cluster kurun. 
<details>
  <summary>Çözümü görmek için tıklayınız!</summary>
Minikube:

```
$ minikube start --nodes=5
```

AKS:

```
$ az group create --name rg-k8sproje --location northeurope

$ az aks create --name aks-k8sproje --resource-group rg-k8sproje --node-vm-size Standard_B2ms --node-count 4 --location northeurope

$ az aks get-credentials --name aks-k8sproje --resource-group rg-k8sproje
```
</details>

***
**2:** "test" ve "production" adlarında 2 namespace oluşturun.
<details>
  <summary>Çözümü görmek için tıklayınız!</summary>

```
$ kubectl create namespace test

$ kubectl create namespace production
```
</details>

***
**3:** "junior" isimli grubun "test" namespace'inde tüm kaynaklar üstünde "okuma, listeleme, yaratma..." gibi tüm haklara, "production" namespace'inde ise tüm kaynaklar üstünde sadece "okuma ve listeleme" haklarına sahip olacağı rol oluşturup bunları grupla ilişkilendirin. Aynı şekilde "senior" isimli grubun "production" ve "test" namespace'lerindeki tüm kaynaklar üstünde "okuma, listeleme, yaratma..." gibi tüm haklara ve cluster üstündeki diğer kaynaklar üstünde ise sadece "okuma ve listeleme" haklarına sahip olacağı rol oluşturup bunları grupla ilişkilendirin.

<details>
  <summary>Çözümü görmek için tıklayınız!</summary>

```
$ kubectl apply -f ./yaml/jr-production-rb.yaml

$ kubectl apply -f ./yaml/jr-test-rb.yaml

$ kubectl apply -f ./yaml/sr-cluster-crb.yaml

$ kubectl apply -f ./yaml/sr-production-rb.yaml

$ kubectl apply -f ./yaml/sr-test-rb.yaml
```
</details>

***
**4:** Sizin seçeceğiniz bir "ingress controller" kurun. (nginx, traefik, haproxy vb.)

<details>
  <summary>Çözümü görmek için tıklayınız!</summary>

Nginx: https://kubernetes.github.io/ingress-nginx/deploy/

AKS:
```
$ kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v0.47.0/deploy/static/provider/cloud/deploy.yaml
```

Minikube:
```
$ minikube addons enable ingress
```
</details>

***
**5:** Cluster'da seçeceğiniz 3 worker node sadece "production" ortamında deploy edeceğiniz ve cluster tarafından oluşturulan podlar schedule edilebilsin. Bunun dışındaki podların bu worker node üstünde oluşturulmamasını sağlayın. 
<details>
  <summary>Çözümü görmek için tıklayınız!</summary>

```
$ node1=$(kubectl get no -o jsonpath="{.items[1].metadata.name}")

$ node2=$(kubectl get no -o jsonpath="{.items[2].metadata.name}")

$ node3=$(kubectl get no -o jsonpath="{.items[3].metadata.name}")

$ kubectl taint node $node1 tier=production:NoSchedule

$ kubectl taint node $node2 tier=production:NoSchedule

$ kubectl taint node $node3 tier=production:NoSchedule

$ kubectl label node $node1 tier=production

$ kubectl label node $node2 tier=production

$ kubectl label node $node3 tier=production
```

</details>

***
**6:** Wordpress uygulamasını hem "test" hem de "production" namespace'lerinde deploy edin. (wordpress:latest ve mysql:5.6 imajlarından oluşturulacak)

- mysql "ClusterIp" tipi bir servisle cluster içinden erişilebilir olacak. 
- Her iki uygulamanın da uzun dönem verilerini "persistent volume"ler üzerinde saklanacak.
- Her iki uygulamanın da hiç bir hassas bilgisi "ör: şifre" uygulama ya da yaml dosyaları içerisinde tutulmayacak. 
- Her iki uygulama da aynı worker node üstünde schedule edilecek.
- Her iki uygulama için de cpu ve memory kaynak kısıtları tanımlı olacak.  
<details>
  <summary>Çözümü görmek için tıklayınız!</summary>

```
$ kubectl create secret generic mysql-test-secret -n test --from-file=MYSQL_ROOT_PASSWORD=./yaml/mysql_root_password.txt --from-file=MYSQL_USER=./yaml/mysql_user.txt --from-file=MYSQL_PASSWORD=./yaml/mysql_password.txt --from-file=MYSQL_DATABASE=./yaml/mysql_database.txt

$ kubectl create secret generic mysql-prod-secret -n production --from-file=MYSQL_ROOT_PASSWORD=./yaml/mysql_root_password.txt --from-file=MYSQL_USER=./yaml/mysql_user.txt --from-file=MYSQL_PASSWORD=./yaml/mysql_password.txt --from-file=MYSQL_DATABASE=./yaml/mysql_database.txt

$ kubectl apply -f ./yaml/wptest.yaml

$ kubectl apply -f ./yaml/wpprod.yaml
```

</details>

***
**7:** "test" namespace'inde deploy edilen wordpress uygulaması "testblog.example.com", "production" namespace'inde deploy edilen wordpress uygulaması "companyblog.example.com" olarak ingress üstünden dış dünyaya expose edilecek.
<details>
  <summary>Çözümü görmek için tıklayınız!</summary>

```
$ kubectl apply -f ./yaml/wpingress.yaml
```

</details>

***
**8:** "production" namespace'inde "ozgurozturknet/k8s:v1" imajından, 5 replikalı, update stratejisi olarak aynı anda 2 pod'un update edilebileceği bir deployment oluşturun. "/healthcheck" endpoint'ini sorgulayan "liveness probe" ve "/ready" endpoint'ini sorgulayan bir "readiness probe" tanımları da olsun. 
<details>
  <summary>Çözümü görmek için tıklayınız!</summary>

```
$ kubectl apply -f ./yaml/deployment.yaml
```

</details>

***
**9:** Bir önceki görevde oluşturduğunuz deployment'i "loadbalancer" tipi bir servisle dış dünyadan erişilebilir hale getirin. 
<details>
  <summary>Çözümü görmek için tıklayınız!</summary>

```
$ kubectl expose deployment k8s-deployment --type=LoadBalancer -n production
```

</details>

***
**10:** Bu deployment'i önce 3 replikaya indirin. Ardından 10 replikaya çıkarın. Sonrasında bu deployment'i "ozgurozturknet/k8s:v2" imajıyla güncelleyin.
<details>
  <summary>Çözümü görmek için tıklayınız!</summary>

```
$ kubectl scale deployment k8s-deployment --replicas=3 -n production

$ kubectl scale deployment k8s-deployment --replicas=10 -n production

$ kubectl set image deployment/k8s-deployment k8s=ozgurozturknet/k8s:v2 -n production
```

</details>

***
**11:** "fluentd" uygulamasını bir "daemonset" olarak cluster'da deploy edin. 
<details>
  <summary>Çözümü görmek için tıklayınız!</summary>

```
$ kubectl apply -f ./yaml/daemonset.yaml
```

</details>

***
**12:** 2 node'lu bir "mongodb" cluster'i "statefulset" olarak cluster'da deploy edin. "mongodb" cluster'ın çalıştığından emin olun. 
<details>
  <summary>Çözümü görmek için tıklayınız!</summary>

```
$ kubectl apply -f ./yaml/statefulset.yaml

$ kubectl exec -it mongostatefulset-0 -- bash

root@mongostatefulset-0:/# mongo

> rs.initiate({ _id: "MainRepSet", version: 1, 
members: [ 
 { _id: 0, host: "mongostatefulset-0.mongo-svc.default.svc.cluster.local:27017" }, 
 { _id: 1, host: "mongostatefulset-1.mongo-svc.default.svc.cluster.local:27017" } ]});

MainRepSet:PRIMARY> db.getSiblingDB("admin").createUser({
...       user : "mongoadmin",
...       pwd  : "P@ssw0rd!1",
...       roles: [ { role: "root", db: "admin" } ]
...  });

MainRepSet:PRIMARY> rs.status();

```

</details>

***
**13:** Cluster'da tüm objeler üstünde "okuma ve listeleme" haklarına sahip bir "service account" oluşturun. Bu service account’u bağladığınız bir pod oluşturun ve bağlanarak "curl" ile cluster’daki tüm podları listeleyin. 
<details>
  <summary>Çözümü görmek için tıklayınız!</summary>

```
$ kubectl apply -f ./yaml/serviceaccount.yaml

$ kubectl exec -it pod-proje -- bash

bash-5.0# CERT=/var/run/secrets/kubernetes.io/serviceaccount/ca.crt

bash-5.0# TOKEN=$(cat /var/run/secrets/kubernetes.io/serviceaccount/token)

bash-5.0# curl --cacert $CERT https://kubernetes/api/v1/pods --header "Authorization:Bearer $TOKEN" | jq '.items[].metadata.name'

```

</details>

***
**14:** Worker node'lardan bir tanesinin üzerindeki tüm podları tahliye edin ve ardından yeni pod schedule edilememesini sağlayın. 
<details>
  <summary>Çözümü görmek için tıklayınız!</summary>

```
$ nodedrain=$(kubectl get no -o jsonpath="{.items[3].metadata.name}")

$ kubectl drain $nodedrain --ignore-daemonsets --delete-local-data

$ kubectl cordon $nodedrain

```

</details>

***

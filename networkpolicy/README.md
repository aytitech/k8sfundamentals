# Network Policy

## Minikube

* Minikube'u calico plug-in'iyle başlat

```
$ minikube start --cpus 4 --memory 6144 --cni=calico --container-runtime=docker --host-only-cidr=172.17.17.1/24
```

* Podları ve namespaceleri oluştur

```
$ kubectl apply -f deploy.yaml
```

* Network Policy deploy et
```
$ kubectl apply -f policy.yaml
```

* Poda'ya bağlan ve sadece 1.1.1.1'e 80 portuna gidebildiğini başka yere gidemediğini teyit et

```
$ kubectl exec -it -n ns-a poda -- bash
```

* PodB ve Frontend podlarından pod'a 80 portundan gidebildiğini teyit et. PodC'den ise gidemeyeceksin.

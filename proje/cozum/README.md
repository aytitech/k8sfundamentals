**1:** 5 node'lu "1 Master + 4 Worker Node" bir Kubernetes cluster kurun. 

Minikube:
```
minikube start ---node=5
```

AKS:

```
$ az group create --name rg-k8sproje --location northeurope

$ az aks create --name aks-k8sproje --resource-group rg-k8sproje --node-vm-size Standard_B2ms --node-count 4 --location northeurope

$ az aks get-credentials --name aks-k8sproje --resource-group rg-k8sproje
```
***
**2:** "test" ve "production" adlarında 2 namespace oluşturun.

```
$ kubectl create namespace test

$ kubectl create namespace prod
```
***
**3:** "junior" isimli grubun "test" namespace'inde tüm kaynaklar üstünde "okuma, listeleme, yaratma..." gibi tüm haklara, "production" namespace'inde ise tüm kaynaklar üstünde sadece "okuma ve listeleme" haklarına sahip olacağı rol oluşturup bunları grupla ilişkilendirin. Aynı şekilde "senior" isimli grubun "production" ve "test" namespace'lerindeki tüm kaynaklar üstünde "okuma, listeleme, yaratma..." gibi tüm haklara ve cluster üstündeki diğer kaynaklar üstünde ise sadece "okuma ve listeleme" haklarına sahip olacağı rol oluşturup bunları grupla ilişkilendirin.


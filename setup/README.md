# Kurulum
**Kubernetes Kurulum** konusuyla ilgili dosyalara buradan erişebilirsiniz.

## kubeadm kurulum

https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/install-kubeadm/

**0:** sanal makine oluşturma
```
$ multipass launch --name master -c 2 -m 2G -d 10G
$ multipass launch --name node1 -c 2 -m 2G -d 10G
```
* Master node'a bağlanıp ```sudo hostnamectl set-hostname master``` komutunu girin. node1'e bağlanıp ```sudo hostnamectl set-hostname node1``` komutunu girin.

**1:** Kernel modulleri aktive ediyor ve swap kapatıyoruz

```
$ sudo modprobe overlay
$ sudo modprobe br_netfilter
```

```
$ cat <<EOF | sudo tee /etc/modules-load.d/k8s.conf
overlay
br_netfilter
EOF
```

```
$ cat <<EOF | sudo tee /etc/sysctl.d/k8s.conf
net.bridge.bridge-nf-call-iptables  = 1
net.bridge.bridge-nf-call-ip6tables = 1
net.ipv4.ip_forward                 = 1
EOF
```

```
$ sudo sysctl --system
```

```
$ sudo swapoff -a
$ free -m
$ sudo sed -i '/ swap / s/^\(.*\)$/#\1/g' /etc/fstab
```

**2:** containerd kurulumu

```
$ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker.gpg
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
$ sudo apt update
$ sudo apt install containerd.io
$ sudo systemctl daemon-reload
$ sudo systemctl enable --now containerd
$ sudo systemctl start containerd
$ sudo mkdir -p /etc/containerd
$ sudo su -
$ containerd config default | tee /etc/containerd/config.toml
$ exit
$ sudo sed -i 's/            SystemdCgroup = false/            SystemdCgroup = true/' /etc/containerd/config.toml
$ sudo systemctl restart containerd

```

**3:** kubeadm kurulumu


```
$ sudo ufw allow 6443/tcp
$ sudo ufw allow 2379:2380/tcp
$ sudo ufw allow 10250/tcp
$ sudo ufw allow 10259/tcp
$ sudo ufw allow 10257/tcp
$ sudo apt-get update
$ sudo apt-get install -y apt-transport-https ca-certificates curl
$ sudo curl -fsSLo /usr/share/keyrings/kubernetes-archive-keyring.gpg https://packages.cloud.google.com/apt/doc/apt-key.gpg
$ echo "deb [signed-by=/usr/share/keyrings/kubernetes-archive-keyring.gpg] https://apt.kubernetes.io/ kubernetes-xenial main" | sudo tee /etc/apt/sources.list.d/kubernetes.list
$ sudo apt-get update
$ sudo apt-get install -y kubelet kubeadm kubectl
$ sudo apt-mark hold kubelet kubeadm kubectl
```

**4:** kubernetes cluster kurulumu

```
$ sudo kubeadm config images pull

$ sudo kubeadm init --pod-network-cidr=192.168.0.0/16 --apiserver-advertise-address=<ip> --control-plane-endpoint=<ip>
```

```
$ mkdir -p $HOME/.kube
$ sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
$ sudo chown $(id -u):$(id -g) $HOME/.kube/config
```

```
$ kubectl create -f https://raw.githubusercontent.com/projectcalico/calico/v3.25.1/manifests/tigera-operator.yaml
$ kubectl create -f https://raw.githubusercontent.com/projectcalico/calico/v3.25.1/manifests/custom-resources.yaml
```

```
kubectl taint nodes --all node-role.kubernetes.io/control-plane-
kubectl taint nodes --all node-role.kubernetes.io/master-
```

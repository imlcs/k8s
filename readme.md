1. 安装 yum 源
```
# 添加 docker-ce 阿里源
cd /etc/yum.repos.d && \
wget https://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo

# 添加 kubernetes 阿里源
# vi /etc/yum.repos.d/kubernetes.repo

[kubernetes]
name=kubernetes
baseurl=https://mirrors.aliyun.com/kubernetes/yum/repos/kubernetes-el7-x86_64/
enabled=1
gpgcheck=0

```
2. 安装并初始化 kubeadm 
- 安装
```
yum install kubelet kubeadm kubectl
```
- 初始化
```
kubeadm init --pod-network-cidr 10.244.0.0/16 --service-cidr 10.96.0.0/12 \
--ignore-preflight-errors=Swap


# 初始化日志

Your Kubernetes master has initialized successfully!

To start using your cluster, you need to run the following as a regular user:

  mkdir -p $HOME/.kube
  sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
  sudo chown $(id -u):$(id -g) $HOME/.kube/config

You should now deploy a pod network to the cluster.
Run "kubectl apply -f [podnetwork].yaml" with one of the options listed at:
  https://kubernetes.io/docs/concepts/cluster-administration/addons/

You can now join any number of machines by running the following on each node
as root:

  kubeadm join 192.168.4.11:6443 --token 5ja10h.69uhv5781gep1rou --discovery-token-ca-cert-hash sha256:e47c1a62c9c284979787c9ee6311a4402d89aec8c84e67075ac5bf3d68832658
```

- 部署pods
```
alias kbc=kubectl

# 创建 pod
kbc run nginx-deploy --image=nginx:alpine --port=80 --replicas=1
# 连接 pod
kbc exec -it {pod_name} -- /bin/sh
# 创建 services
kbc expose deployment nginx-deploy --name=nginx --port=80 --target-port=80 --protocol=TCP
# 扩容缩容
kbc scale --replicas=2 deployment myapp
# 升级更新
kbc set image deployment myapp myapp=ikubernetes/myapp:v2
# 更新状态
kbc rollout status deployment myapp
# pod 状态
kbc describe pods myapp-6946649ccd-69p8n # pod name
# 回滚到上一个版本
kbc rollout undo deployment myapp
# 编辑 svc
kbc edit svc myapp
```

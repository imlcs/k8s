### 创建 token 认证流程
1. 生成密钥认证文件
```
cd /etc/kubernetes/pki
(umask 077; openssl genrsa -out dashboard.key 2048)
openssl x509 -req  -in dashboard.csr -CA ca.crt -CAkey ca.key -CAcreateserial -out dashboard.crt -days 365
```

2. 创建 serviceaccount
```
kce serviceaccount dashboard-admin -n kube-system
```
3. 创建 secret
```
kce secret generic dashboard-cert -n kube-system --from-file=dashboard.crt=./dashboard.crt --from-file=dashboard.key=./dashboard.key
kds secret -n kube-system dashboard-cert
```
4. 绑定集群管理对象
```
kce clusterrolebinding dashboard-cluster-admin --clusterrole=cluster-admin --serviceaccount=kube-system:dashboard-admin
```
5. 修改 svc 类型为 NodePort
```
kbc patch svc -n kube-system kubernetes-dashboard -p '{"spec":{"type":"NodePort"}}'
```
6. 获取 token 
```
kds secret dashboard-admin-token-dq5jf -n kube-system  # secret 对象名称不一样,自行查看对象名
```

### 创建 config 认证流程

1. 创建 serviceaccount
```
kce serviceaccount dashboard-admin -n kube-system
```
2. 使用 rolebinding 或者 clusterrolebinding 绑定至合理的role或者clusterrole
```
kce clusterrolebinding dashboard-cluster-admin --clusterrole=cluster-admin --serviceaccount=kube-system:dashboard-admin
```
3. 配置 config 文件
```
kbc config set-cluster kubernetes --certificate-authority=/etc/kubernetes/pki/ca.crt --server="https://192.168.4.11:6443" --embed-certs=true --kubeconfig=/root/cluster-admin.conf

# 获取 token，secret 名字自行获取
KUBE_TOKEN=$(kubectl get secret dashboard-admin-token-dq5jf -n kube-system -o jsonpath={.data.token}|base64 -d)

kbc config set-credentials cluster-admin --token=$KUBE_TOKEN --kubeconfig=/root/cluster-admin.conf

kbc config set-context cluster-admin@kubernetes --cluster=kubernetes --user=cluster-admin --kubeconfig=/root/cluster-admin.conf

kbc config use-context cluster-admin@kubernetes --kubeconfig=/root/cluster-admin.conf
```

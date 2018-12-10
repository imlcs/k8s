### docker 网络模式
- bridge：自由网络名称空间
- joined：共享使用另外一个容器的网络名称空间
- open：共享使用宿主机的网络名称空间
- none：不适用宿主机的网络名称空间

### Kubernetes 网络通信
1. 容器间通信：同一个Pod内的多个容器间的通信，lo
2. Pod间通信：Pod IP -> Pod IP
3. Pod与Service通信：Pod IP -> Cluster IP
4. Service与集群外部客户端的通信

### CNI
- flannel：支持多种后端
```
Vxlan
    vxlan
    Directrouting
Host Gateway

配置参数：
    Network：flannel 使用 CIDR 格式的网络地址，用于为Pod配置网络功能
        10.244.0.0/16 ->
            master: 10.244.0.0/24
            node1:  10.244.1.0/24
            node2:  10.244.2.0/24
            ...
            node255:10.244.255.0/24
    SubnetLen：Network 切分子网供各节点使用时，使用的掩码长度，默认为24
    SubnetMin：10.244.10.0 (分给节点的其实子网段，默认从0开始)
    SubnetMax:
    Backend: vxlan, host-gw, udp
```
- calico
- canel
- kube-router
- 解决方案
```
虚拟网桥
多路复用：MacVLAN
硬件交换：SR-IOV
```

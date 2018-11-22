#### Service 的工作模式
- userSpace: 1.1-
- iptables: 1.10+
- ipvs: 1.11+
#### Service 的类型
- ExternalName: 集群外部的服务引入集群内部，在集群内部直接使用
- ClusterIP: 默认
- NodePort: 接入集群外流量
- and LoadBalancer: 创建云环境上的LB
#### 资源记录
```
SVC_NAME.NS_NAME.DOMAIN.LTD.

默认DOMAIN.LTD: svc.cluster.local.

SVC_NAME 为 redis 时: redis.default.svc.cluster.local.
```

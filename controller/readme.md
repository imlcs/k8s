### Pod 控制器
- ReplicaSet: rs-demo.yaml
- Deployment: deployment-demo.yaml
- DaemonSet: ds-demo.yaml
- Job
- Cronjob
- StatefulSet
```
1. 稳定并且唯一的网络标识符
2. 稳定并且持久的存储
3. 有序、平滑的部署和扩展
4. 有序、平滑的终止和删除
5. 有序的滚动更新

三个组件：
    headless services
    StatefulSet
    volumeClaimTemplate

dns解析时格式： pod_name.svc_name.ns_name.svc.cluster.local
    myapp-0.myapp.default.svc.cluster.local
```
- Operator:

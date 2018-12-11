### 调度器：
- 预选策略：
1. CheckNodeCondition;
2. GeneralPredicates:
```
HostName: 检查Pod对象是否定义了 pods.spec.hostname

PodFitsHostPorts: pods.spec.containers.ports.hostPort

MatchNodeSelector: pods.spec.nodeSelector

PodFitsResources: 检查Pod的资源需求是否可以被节点所满足
```
3. NoDiskConflict: 检查Pod依赖的存储卷需求是否满足(默认没有启用)
4. PodToleratesNodeTaints: 检查Pod上的 spec.toleration 可容忍的污点是否完全包含节点上的污点
5. PodToleratesNodeNoExecuteTaints: (默认没有启用)
6. CheckNOdeLabelPresence: 检查标签的存在性(默认没有启用)
7. CheckServiceAffinity: (默认没有启用)
---
- 优选函数
1. LeastRequested(MostRequested):
```
(cpu((capacity - sum(requested)) * 10 / capacity) + memory((capacity - sum(requested)) * 10 / capacity) / 2
```
2. BalancedResourceAllocation: CPU 和内存资源占用率相近的胜出
3. NodePreferAvoidPods: 几点注解信息"scheduler.alpha.kubernetes.io/preferAvoidPods"
4. TaintToleration: 将Pod对象的 spec.tolerations 列表项与与节点的taints列表项进行匹配度检查，匹配条目越多，得分越低
5. SeletorSpreading:

---
节点选择器： nodeSelector，nodeName
节点亲和调度：nodeAffinity

---
### taint：污点
```
kubectl taint node node1 node-type:production:NoSchedule
```

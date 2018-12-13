### 容器的资源需求，资源限制
- requests：需求，最低保障
- limits：限制，硬限制

- CPU
```
1颗逻辑CPU，
1 = 1000(m) millicores
500m = 0.5 CPU

cpu.limits = 500m (最大CPU资源)
cpu.requests = 200m (最小CPU资源)
```
https://kubernetes.io/docs/concepts/configuration/manage-compute-resources-container/
- memory
```
Ei,Pi,Ti,Gi,Mi,Ki
```

- Qos Class
```
优先级由高到低

Guranteed:
    同时设置CPU和内存的 requests 和 limits
        cpu.limits=cpu.requests
        memory.limits=memory.requests
Burstale:
    至少有一个容器设置CPU或memory的requests属性
BestEffort: 
    没有任何一个容器设置了requests或limits属性
```

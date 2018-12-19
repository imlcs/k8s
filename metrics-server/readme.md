资源指标：metrics-server
自定义指标：prometheus，k8s-prometheus-adapter

新一代架构：
    核心指标流水线：有kubelet、metrics-server以及API server提供的api组成；CPU累计使用率、内存实时使用率、pod资源占用率以及容器的磁盘占用率
    监控流水线：用于从系统收集各种指标数据并提供终端用户、存储系统以及HPA、它们包含核心指标及许多非核心指标。非核心指标本身不能被k8s所解析

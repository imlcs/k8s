### Helm
1. 核心术语

- Chart: 一个 helm 的程序包
- Repository: Charts 仓库， https/http 服务器
- Release: 特定的 Chart 部署与目标集群上的一个实例
- Chart -> Config -> Release

2. 程序架构
- helm: 客户端，管理本地的 Chart 仓库， 管理 Chart， 与 Tiller 服务器交互，发送 Chart，实例安装、查询、卸载等操作
- Tiller: 服务端,接收 helm 发来的 Chart 与 Config，合并生成release

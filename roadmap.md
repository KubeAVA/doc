## 异构资源管理与调度系统

本文档为**异构资源管理与调度系统**的研究路线，具体的路线细节处于动态调整中。若无特殊说明，每一阶段内的不同工作内容均处于并行工作模式。

### 第一阶段

- 开发支持 GPU 资源的 kube-acc 项目
  
  - 详情：基于 Kubernetes 的 Device Plugin 机制，扩展 GPU 为可使用、可调度的抽象资源。
  - 完成情况：已完成
  - 成果地址：https://github.com/KubeAVA/kube-acc

- kube-acc 集成腾讯开源 GPU 资源控制模块 vcuda-controller
  
  - 详情：将腾讯开源 GPU 资源控制模块打包为镜像，集成进入 kube-acc 项目，使 Pod 能够按照配额文件限制使用 GPU 显存和算力，达到隔离与控制的效果。
  - 完成情况：已完成
  - 成果地址：registry.cn-beijing.aliyuncs.com/doslab/vcuda-lib:v1.0.3

### 第二阶段

- 开发限制 GPU 资源的 cuda-ctrl 项目
  
  - 详情：参考腾讯开源的 vcuda-controller 以及 KubeShare 项目，自己实现 GPU 资源控制模块，为其它异构资源（FPGA、ASIC等）进行技术验证。
  - 完成情况：开发中
  - 预期开发路线：
    - 阅读相关代码，初步设计：已完成
    - 导入 CUDA 相关定义：已完成
    - 拦截资源限制相关的 CUDA API函数：已完成
    - 构建 CUDA API 拦截测试用例：已完成
    - 进行显存资源的限制：正在进行
    - 进行算力资源的限制：待完成
    - 构建限制算法抽象化模块：待完成
  - 成果地址：https://github.com/KubeAVA/cuda-ctrl

- 调研与验证 FPGA 资源的使用
  
  - 详情：调研 FPGA 如何运行深度学习的应用，在实际的开发板上验证，尝试不同的技术路线，并评估最合适的技术路线。
  - 完成情况：进行中
  - 预期路线：
    - 调研 TVM 的 VTA 相关技术路线，使用 PYNQ 方式将深度学习应用部署到 FPGA 开发板上：正在进行
    - 调研 Xilinx 的 Vitis-AI 的相关技术路线，将深度学习应用部署到 FPGA 开发板上：正在进行
    - 评估合适的技术路线，并实际部署：待完成
  - 成果地址：暂无

### 第三阶段

- 开发限制 FPGA 资源的 fpga-ctrl 项目

  - 详情：在开发 cuda-ctrl 的基础上，开发 FPGA 资源控制模块。
  - 完成情况：待完成
  - 预期开发路线：
    - 与开发 cuda-ctrl 相似，在第二阶段**调研与验证 FPGA 资源的使用**完成后，再补充细节
  - 成果地址：暂无
  
- kube-acc 集成自研的 FPGA 资源控制模块 fpga-ctrl
  
  - 详情：将自研的 FPGA 资源控制模块 fpga-ctrl 打包为镜像，集成进入 kube-acc 项目，使 Pod 能够按照配额文件限制使用 FPGA 内存和算力，达到隔离与控制的效果。
  - 完成情况：待完成
  - 预期开发路线：
    - 与集成 cuda-ctrl 相似，在第二阶段**调研与验证 FPGA 资源的使用**与第三阶段**开发限制 FPGA 资源的 fpga-ctrl 项目**完成后，再补充细节
  - 成果地址：暂无

### 第四阶段

- 重构 kube-acc 项目，改善代码通用性
  
  - 详情：重构 kube-acc 的代码，设计公用的接口，适配各种运行时和各种异构资源。
  - 完成情况：待完成
  - 预期开发路线：
    - 重构项目代码：待完成
  - 成果地址：https://github.com/KubeAVA/kube-acc

- 探索资源控制代码的复用与自动生成
  
  - 详情：探索各种异构资源的控制模块的代码复用的可能性，实现代码自动生成。
  - 完成情况：待完成
  - 预期路线：
    - 阅读 AVA 的论文和代码，了解相关的原理：进行中
    - 设计代码复用的模块以及代码自动生成的逻辑：待完成
    - 开发与验证代码自动生成的功能：待完成
  - 成果地址：暂无
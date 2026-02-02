# BOSS直聘 SRE/运维/AI Infra 岗位汇总（压缩版）

## 通用要求（出现数百次，仅列一次）
- 本科及以上学历、计算机相关专业
- 良好的沟通能力、责任心、自驱力、团队合作精神
- 具备学习能力、抗压能力、问题分析与解决能力
- 适应on-call轮值、7×24应急响应能力

---

## 一、AI Infra / 大模型 / GPU集群方向

### 岗位1：分布式LLM推理基础设施
负责分布式大语言模型(LLM)推理系统的底层基础设施研究与探索，包括GPU和RDMA等，提升GPU环境下的稳定性和计算效率。负责针对不同架构的模型，实现推理引擎的功能研发以及性能优化。利用算子优化、显存/KV cache管理优化、分布式加速等技术开发和改进推理框架。

**技术栈**：vLLM、SGLang、RouteLLM、Kubernetes、Docker、RDMA、NCCL通信库、Mooncake传输层

### 岗位2：大规模模型训练优化
负责大规模模型训练场景优化工作，通过建设全面的异常发现、故障自愈机制，提升平台训练MFU，降低训练成本。深入了解GPU架构与并行计算，掌握CUDA编程实践。熟悉投机解码Draft-Target模型协作机制、PagedAttention原理、Unified Memory。

**技术栈**：GPU、CUDA、MFU、异常发现、故障自愈、投机解码、PagedAttention

### 岗位3：快手容器云算力平台
负责快手容器云超大规模算力平台的架构设计与开发工作，包括资源调度、服务编排及容器引擎等多领域场景。基于云原生技术完善海量异构资源的多集群联邦和统一调度能力。云原生及大模型推理场景AI-Infra领域前沿技术，提升大规模的推理场景GPU利用效率。

**技术栈**：Kubernetes、Docker、多集群联邦、异构资源调度、GPU利用效率

### 岗位4：电商搜推AI Infra
负责电商搜推领域的AI infra平台的架构设计、研发和维护工作，建设一站式的低代码/可视化的研发和部署平台，及配套的Devops运维一体化平台。面向推荐系统的算法和工程同学，建设从数据接入、组件注册、逻辑编排、测试到发布部署的一站式开发和部署平台。建设配置的可观测、可管理、可追溯、自动化的Devops运维一体化平台。

**技术栈**：go、python、MySQL、NoSql、KV、MQ、低代码平台、PAAS平台、devops平台、机器学习平台

### 岗位5：大模型技术应用
参与大语言模型、AIGC(图片/视频)生成大模型、多模态模型工作，包括数据收集与处理、预训练和重域持续预训练、提示与指令设计、SFT与RL对齐、通用&应用能力的训练与推理的适配。负责业界主流LLM大模型以及多模态大模型的适配与性能优化，参与并行部署、量化压缩、服务化动态调度等性能提升技术的研究与落地。

**技术栈**：DeepSeek、GPT、Qwen、LLaMA、ViT、CLIP、LLaVA、SFT、RL对齐、并行部署、量化压缩

### 岗位6：大模型强化学习框架
熟悉大模型强化学习框架（如AREaL、veRL等）的上手修改经验。具备良好的项目运营习惯，能够阅读和撰写英文文档，注重Issue、RFC和PR规范，熟悉并能够修改CI/CD流程。熟悉集群调度系统（如SLURM、Kubernetes）和容器技术（如Docker镜像构建、容器编排）。深入理解GPU体系结构与分布式计算原理。

**技术栈**：AREaL、veRL、SLURM、Kubernetes、Docker、GPU体系结构

### 岗位7：AI Agent Infra建设
负责AI Agent Infra建设，提升AI Agent产品创新效率，探索生成式AI在数字世界的实际应用。建设Agent SWE Infra工程，提升Agent相关代码的个性化构建和发布效率。建设Sandbox Infra工程，为各类Agentic场景提供高效、稳定、大规模的模拟器、多工具、图形交互的沙箱环境。建设Serving Infra工程，为生产提供通用的Agent服务化框架，优化LLM和Agent性能，保障高可用运行。

**技术栈**：AI Agent、Sandbox、Serving、Prompt优化、KVCache优化、推理加速、模型训练优化、向量数据库

### 岗位8：多模态优化加速
参与抖音直播的AI分身的多模态理解和CV算法的实时优化加速。掌握计算机体系结构，有并行计算经验，了解GPU/CPU/NPU全链路相关的加速优化技术，包括但不限于SSE/AVX/Neon等指令优化和汇编优化、定点优化、低比特量化。熟悉CUDA编程，具备较好开发能力，熟悉triton、cutlass、有算子库开发经验者优先。了解CNN、diffusion model、transformerAI、LLM模型的优化加速技术。

**技术栈**：多模态、CV算法、SSE/AVX/Neon、定点优化、低比特量化、CUDA、Triton、Cutlass、CNN、Diffusion、Transformer

### 岗位9：GPU集群SRE
负责海量高性能GPU/CPU卡的资源交付与一致性保障，涵盖万卡大模型训练、在线推理、在线搜索、推荐训练等不同业务场景的集群管理。学习并深入了解GPU业务方的使用姿势和训练框架，掌握前沿AI大模型技术，解决超大规模场景下的稳定性挑战，涉及Nvidia H100、A100、昇腾、以及自研XPU等高性能卡型的使用。构建自动化工程，确保生产环境的稳定性和资源在线率，及时发现并隔离故障GPU资源，提高资源流转效率。

**技术栈**：GPU、CPU、万卡集群、Nvidia H100、A100、昇腾、XPU、TensorFlow、PyTorch、分布式训练

### 岗位10：机器学习平台SRE
负责维护机器学习系统的稳定运转，支持大模型的开发、训练与部署的多个环节。负责组织GPU资源的管理与规划，成本与预算，包括：GPU/CPU机器资源、存储等资源，为管理层提供资源决策数据。负责集群、业务服务的稳定性治理，资源利用率提升和运维人效提升，通过平台化系统化的手段提升资源使用的效率。负责多地域、多机房的系统容灾、服务部署管理和集群机器治理，提供稳定高效的GPU系统运行环境。

**技术栈**：GPU资源管理、Kubernetes、Docker、Kata、容器化、稳定性治理

### 岗位11：自动驾驶AI Infra
参与搭建自动驾驶-ai-infra建设，搭建工业级数据能力底座，亿级数据量，分布式架构下的数据分析。熟悉大模型/多模态/端到端自动驾驶技术栈（如BEV、Occupancy、Diffusion、LLM等）。ai-infra能力构建：有数据闭环、模型训练优化、分布式计算等相关经验。精通Python/C++，具备高性能算法开发能力。具备大数据处理、高并发、分布式系统性能优化经验。熟悉K8S调度，掌握分布式存储、并发控制方案。熟悉DuckDB、ES、Mongo、Redis等数据引擎，有实际调优经验。

**技术栈**：BEV、Occupancy、Diffusion、LLM、亿级数据、Python、C++、DuckDB、ES、Mongo、Redis、凸优化、聚类

### 岗位12：推理框架实习
协作高并发场景下大模型推理的性能分析优化工作，定位系统瓶颈并提出改进方案。理解投机解码：熟悉Draft-Target模型协作机制；显存池优化：熟悉PagedAttention原理，了解Unified Memory等；异构系统调度：了解如何在不同算力/显存的GPU之间进行负载均衡和流水线调度；稀疏传输与压缩：熟悉KV Cache的稀疏性特征（如H2O, StreamingLLM），了解量化传输策略；序列预测：了解基于预测的预加载或预计算策略。

**技术栈**：Python、C++、CUDA、PagedAttention、Unified Memory、H2O、StreamingLLM、SGLang、vLLM

### AI Infra技术汇总
**编程语言**：Golang、Java、Python、C++、Shell、Rust
**AI框架**：PyTorch、TensorFlow、DeepSpeed、Megatron、vLLM、SGLang、RouteLLM、AREaL、veRL
**模型**：DeepSeek、GPT、Qwen、LLaMA、ViT、CLIP、LLaVA
**GPU技术**：CUDA、RDMA、NCCL、Mooncake、MIG分区、vGPU、k8s device-plugin、Nvidia H100/A100、昇腾、XPU
**优化**：算子优化、Triton、Cutlass、KV Cache、PagedAttention、投机解码、H2O、StreamingLLM
**调度**：CRI/CSI/CNI、Volcano、Kueue、SLURM
**自动驾驶**：BEV、Occupancy、Diffusion、端到端
**Agent**：Prompt优化、KVCache优化、推理加速、模型训练优化、向量数据库、知识图谱、RAG
**数据**：DuckDB、ES、Mongo、Redis、凸优化、聚类、数学建模
**容器**：Kubernetes、Docker、K8s、Kata、containerd、cri-o

---

## 二、SRE / 稳定性工程方向

### 岗位1：稳定性体系建设（京东/高级SRE）
负责构建和优化系统稳定性保障体系，包括可观测性、容量管理、混沌工程、故障演练、灾备等核心能力，提升系统整体韧性与可靠性。主导关键业务链路的稳定性设计与风险识别，建立稳定性基线、巡检机制，推动服务架构持续优化。精通Prometheus/Grafana/ELK/Loki/Jaeger等可观测性体系与监控告警体系建设，熟悉分布式系统的稳定性设计。

**技术栈**：Prometheus、Grafana、ELK、Loki、Jaeger、OpenTelemetry、ChaosMesh、Steadybit、混沌工程

### 岗位2：监控告警平台建设
打造端到端的监控告警、日志分析、APM、追踪等可观测体系，缩短故障发现与定位时间（MTTD/MTTR）。负责系统监控指标体系建设，完善业务视角的监控能力，持续提升问题发现和定位能力。研发智能告警引擎，实现告警降噪、收敛、根因分析及预测性告警，变被动响应为主动预防。

**技术栈**：Prometheus、Grafana、Alertmanager、Loki、ELK、Skywalking、Datadog、Zabbix、Open-Falcon

### 岗位3：故障管理与应急响应
建设高质量的故障管理流程，包括故障预防、应急响应、复盘机制，提升业务对异常的感知能力与恢复能力。参与on-call轮值，负责线上故障快速恢复、重大问题定位、运维工程化改进等，解决运维痛点。建立并主导重大故障的应急响应机制与复盘文化，将故障经验转化为架构、流程或工具的改进措施。

**技术栈**：On-call、RCA、MTTD、MTTR、应急响应、故障复盘

### 岗位4：容量规划与性能压测
参与核心系统的性能压测、容量预测及瓶颈分析，提出并推动优化方案落地。负责应用系统的性能、容量、可用性进行分析和评估，持续改进应用系统的可用性。分析系统瓶颈，解决各种疑难问题，对系统进行性能调优。具备出色的容量规划与性能压测经验，能对系统瓶颈进行量化分析与规划。

**技术栈**：性能压测、容量规划、性能调优、瓶颈分析

### 岗位5：SLO/SLA管理
定义关键稳定性指标（SLO/SLI/SLA）、优化服务可用性、构建故障自动化响应流程，并持续推进系统韧性工程（熔断、限流、降级、隔离等）。建立SLA评估标准，计算故障对SLA影响，并对SLA后续改进措施进行跟进。参与制定并完善运维规范与流程。

**技术栈**：SLO、SLI、SLA、熔断、限流、降级、隔离、自愈

### 岗位6：变更治理
负责腾讯云变更治理专项工作，参与腾讯云变更流程、变更规范、变更实施改进优化。参与变更平台需求设计，推动变更平台能力完善。从灰度、回滚、故障隔离、变更管控、变更演练等维度保障业务的变更流程稳定性。制定和完善变更流程规范，保障业务的高可用性和变更流程稳定性。

**技术栈**：灰度发布、自动回滚、故障隔离、变更管控、变更演练

### 岗位7：弹性容灾与防攻击
制定和优化运维解决方案，包括但不限于柔性容灾、智能调度、弹性扩容与防攻击。负责路由、交换机、网络安全、IDC、CDN管理和维护。熟悉高并发、高可用、微服务系统架构运维，对分布式部署、两地三中心、业务多活有实践经验。参与过全球化服务部署者优先。

**技术栈**：柔性容灾、智能调度、弹性扩容、防攻击、路由器、交换机、IDC、CDN、两地三中心、业务多活

### 岗位8：自动化运维平台
推动及开发高效的自动化运维、管理工具，提升运维工作效率。负责设计自动化运维平台，提升运维效率，深入研究运维相关技术，优化和提升平台服务质量。规划并主导运维自动化平台建设，设计实现覆盖部署、监控、故障自愈等全链路的自动化工具与流程，驱动运维模式向智能化、无人化转型。

**技术栈**：Ansible、Terraform、Jenkins、GitLab CI、ArgoCD、SaltStack、Puppet、自动化脚本

### 岗位9：可观测性平台（阿里云SLS）
负责阿里集团、阿里云战略级产品SLS研发，在日增数百PB级的超大规模实时数据之上，挑战从"经典可观测性"向"AI Native基建"的跨越。通过实时采集、索引、存储、语义检索和分析等技术，实时处理每日数百万PB海量数据，并针对AI应用场景进行特定优化，提供智能、自动化数据检索和分析服务。

**技术栈**：SLS、实时采集、索引、存储、语义检索、AI Native、PB级数据

### 岗位10：运维开发平台
负责运维工具与系统功能模块的开发、测试、维护工作；参与境内外一体化运维平台等系统与工具的建设、需求分析、架构设计工作。参与运维自动化工具的设计、建设以及开发工作，提升运维效率。熟悉微服务技术开发框架SpringBoot/Cloud，以及前端开发框架Vue、ElementUI。有基于LLM MCP RAG等技术构建故障快速定位与根因分析等项目经验更优。

**技术栈**：SpringBoot、SpringCloud、Vue、ElementUI、LLM、MCP、RAG、故障定位

### SRE核心技术栈
**云平台**：AWS、Azure、GCP、阿里云、腾讯云、华为云、火山云、移动云
**AWS服务**：EC2、S3、RDS、Lambda、EKS、VPC、IAM、ELB、CloudWatch、KMS、Route53、ACM、ALB、NLB、CloudFront、WAF、Shield
**Azure服务**：Azure DevOps、Pulumi、Function App、App Service、Cosmos DB、SQL Server
**GCP服务**：GKE、Cloud Build、Cloud Run
**阿里云服务**：ECS、VPC、SLB、ACK、RDS、OSS、ARMS、云效
**容器编排**：Kubernetes、K8s、Docker、Helm、KubeVirt、OpenShift、Rancher、Harvester、OCM、Etcd
**网络**：TCP/IP、HTTP/HTTPS、DNS、CDN、负载均衡、SDN、Vxlan、SRv6、Overlay/Underlay、Anycast、智能DNS、HTTPDNS、OSPF、BGP
**数据库**：MySQL、Redis、PostgreSQL、MongoDB、ClickHouse、Oracle、TDSQL、GaussDB、OceanBase、SQL Server
**中间件**：Nginx、Kafka、RabbitMQ、Pulsar、RocketMQ、Elasticsearch、ZooKeeper、Etcd、Nacos、Apollo、EMQX、MinIO、Tomcat、LVS、HAProxy
**监控工具**：Prometheus、Grafana、ELK、Zabbix、Open-Falcon、Skywalking、Jaeger、OpenTelemetry、Loki、Alertmanager、Splunk、Datadog
**脚本语言**：Python、Golang、Java、Shell、Bash、PowerShell、C/C++、Perl、Ruby
**自动化工具**：Ansible、Terraform、Jenkins、GitLab CI、ArgoCD、SaltStack、Puppet、Fabric
**安全**：IAM、RBAC、SSO、OAuth2/OIDC、LDAP、AD、零信任、DevSecOps、Nessus、Falco
**认证**：CKA、CKS、AWS Certified DevOps Engineer、SRE相关认证、CCNA、CCNP、K8S认证
**操作系统**：Linux、CentOS、Ubuntu、Red Hat、Windows Server、Debian、国产操作系统
**内核**：eBPF、perf、namespaces、cgroups、文件系统

---

## 三、云原生 / 容器平台方向

### 岗位1：Kubernetes集群管理（SRE专家）
负责Kubernetes集群的精细化管理，确保集群的高可用性、稳定性和性能。持续优化资源配置策略，利用技术手段提升资源调度效率、资源利用率，并优化集群性能。深入分析容器化应用的瓶颈和故障，制定并实施有效的性能优化方案，保障生产环境的稳定运行。主导容器平台新技术的架构演进，推动容器化技术的持续创新和实践。

**技术栈**：Kubernetes、调度、网络CNI、存储CSI、RBAC、HPA、CA

### 岗位2：多集群联邦管理
负责多集群管理的技术方案设计和实践，确保跨集群资源调度和服务发现的高效运作。混合云集群建设，负责云厂商（如阿里云、腾讯云等）的Kubernetes集群规划、部署及运维，设计多集群联邦管理方案。自动化调度系统开发，实现自定义资源管理开发资源调度工具和云资源自动化调度，任务编排管理，集成监控告警体系。

**技术栈**：多集群、联邦、混合云、Kubernetes、自定义资源、调度工具

### 岗位3：Operator开发
开发并维护Kubernetes Operator，提升容器化应用的自动化管理能力，优化生命周期管理。具有Kubernetes Operator开发经验，或向开源社区贡献过相关代码。负责阿里云容器服务SRE平台建设工作，负责K8S生命周期管理，自愈/弹性/限流、驱逐等稳定性能力相关operator研发工作。

**技术栈**：Operator、CRD、Controller、自定义资源、生命周期管理

### 岗位4：容器网络研发
负责公有云场景下k8s容器网络方案设计，研发和维护工作。负责基于智能网卡、ebpf等技术打造高性能容器网络。负责容器网络可观测性产品设计，研发和维护工作。参与云原生容器网络控制面和数据面的设计、研发和优化工作。参与云原生容器网络新技术的预研、原型设计和开发工作。

**技术栈**：CNI、容器网络、eBPF、DPDK、P4、智能网卡、硬件卸载、Flannel、Calico、Cilium

### 岗位5：云原生虚拟化（KubeVirt）
参与并主导基于Kubernetes的云原生虚拟化平台建设，负责KubeVirt在生产环境的设计、落地与规模化运行。负责虚拟机（VM）生命周期管理能力建设，包括创建、发布、扩缩容、热迁移、高可用与回收。设计并优化VM与Pod混合部署、统一调度与资源隔离方案，提升整体资源利用率。针对高性能核心业务场景，进行CPU/内存/IO/网络等关键路径的性能优化。

**技术栈**：KubeVirt、KVM、QEMU、libvirt、VM生命周期、热迁移、混合部署

### 岗位6：容器调度与在离线混部
负责公司容器调度平台的架构设计和核心功能开发，包括容器资源管理、调度优化、弹性伸缩等模块。设计和实现在线与离线任务的混部调度方案，优化集群资源的整体利用率，实现计算、存储和网络资源的高效调度。针对不同业务场景，研究并改进Kubernetes调度算法，包括任务优先级、抢占机制、节点选择等，提升集群的资源分配效率和稳定性。

**技术栈**：调度器、Volcano、Kueue、Koordinator、OpenKruise、在离线混部、资源调度、弹性伸缩

### 岗位7：K8S运维工程师（Minimax）
负责Minimax线上K8S及云原生周边系统的运维保障和工具开发。负责公司内部大规模K8S集群的建设和稳定性保障。负责监控/日志/网络存储等原生基础设施的保障和工具开发。负责业务容器化部署、互联互通以及疑难问题的排查解决。参与OnCall值班，第一时间响应并与研发团队共同解决各类突发事件，保障核心系统的稳定性。

**技术栈**：Kubernetes、Docker、监控、日志、网络存储、OnCall、故障排查

### 岗位8：云原生网络研发（底层技术）
熟悉K8S、熟悉CNI容器网络架构，熟悉至少一种开源CNI，有相关网络技术研发经验。具备以下条件者优先：有内核、DPDK、EBPF、CNI相关的网络系统研发经验；有智能网卡、硬件卸载、P4等高性能网络研发经验；有Vxlan、SRv6等Overlay技术的网络研发经验；有VPC、LB等云网络研发经验。

**技术栈**：CNI、DPDK、eBPF、P4、智能网卡、Vxlan、SRv6、Overlay、VPC、LB

### 岗位9：容器云平台架构师
负责容器云平台的架构设计与核心研发，基于Kubernetes技术栈，构建高可用、高扩展的云原生基础设施。开发与维护平台核心组件：包括集群管理、资源调度、容器网络、存储编排、监控告警、服务治理等模块。参与云原生产品化能力建设，实现多集群管理、应用发布、服务编排、自动扩缩容等功能。

**技术栈**：Kubernetes、集群管理、资源调度、容器网络、存储编排、监控告警、服务治理

### 云原生核心技术
**Kubernetes核心**：调度器、控制器、CRD、Operator、CNI、CSI、API Server、Controller Manager、Scheduler、Etcd、apiserver、kcm
**容器网络**：Flannel、Calico、Cilium、Multus、SR-IOV、Weave、Canal、Contour、Bond、Vlan、Vxlan、Macvlan、Tap
**容器存储**：Rook-Ceph、Longhorn、本地存储、CSI、Ceph、GlusterFS、NFS、Manila、Cinder、S3、对象存储
**服务网格**：Istio、Envoy、Linkerd、Nginx、Ingress、Consul、LinkedR
**Serverless**：Knative、OpenFaaS、Kubeless、OpenWhisk、Func、Fission
**多集群**：联邦集群、OCM、Rancher、KubeFed、Kubevela
**GPU调度**：Volcano、Kueue、Koordinator、OpenKruise、自定义调度器、kube-scheduler、vGPU
**弹性**：HPA、CA、自动扩缩容、弹性伸缩

---

## 四、云平台 / IaaS / 私有云方向

### 岗位1：私有云架构设计
负责私有云平台产品的架构设计、架构原型实现及核心模块的开发工作。负责云原生中间件方案设计、代码实现以及优化，对代码质量负责。负责云平台统一基座产品功能架构设计，包括云原生应用管理平台、应用发布与调度、资源管理与调度、云产品部署和热升级等能力的研发。

**技术栈**：私有云、云原生、Kubernetes、Serverless、Rancher、OCM、Etcd、Helm、Kubevela

### 岗位2：算力调度平台
负责企业算力调度、作业调度平台的架构设计和功能研发、优化迭代及落地。负责Kubernetes领域和周边的前沿技术跟踪与应用，支撑业务中长期发展。负责边缘超融合架构及私有化项目推进及落地。

**技术栈**：算力调度、作业调度、Kubernetes、边缘超融合

### 岗位3：IaaS运维/SRE
负责IaaS生产环境的稳定、安全、高效运行，保障SLA。负责日常监控、巡检、变更、扩容和应急预案的执行，建设和完善运维自动化体系、监控告警体系。负责IaaS计算业务技术运营，在服务（业务）上线前，通过系统设计调试、框架调试、容量规划、审计流程等提升服务可靠性。

**技术栈**：IaaS、SLA、监控、巡检、变更、扩容、应急预案、运维自动化

### 岗位4：OpenStack运维（移动云）
负责1500台服务器规模OpenStack集群规划、软集部署和日常维护。负责重点问题解决，支撑技术架构云计算相关方案验证。负责建设OpenStack集群监控平台和日常运营。精通OpenStack集群的运维管理，深度掌握其高可用架构和故障恢复机制。熟悉OpenStack架构和工作机制，对Nova/Ironic/Cinder/Glance/Neutron/ceilometer等核心组件代码和业务有深入理解。

**技术栈**：OpenStack、Nova、Ironic、Cinder、Glance、Neutron、Ceilometer、KVM、QEMU、Libvirt、1500台规模

### 岗位5：云平台运维（通用）
负责laaS云平台（计算、存储、网络）的规划、设计、部署、运维以及业务性能调优。负责相关业务技术支持和日常运维工作，对突发事件的快速响应、定位及处理，排除故障，保障系统稳定性。负责相关业务的自动化部署、运维和优化工作，包括整体的运维架构、部署监控方案的设计和实施。

**技术栈**：IaaS、计算、存储、网络、性能调优、自动化部署

### 岗位6：智能运维平台架构
负责基于云业务场景下的统一智能运维平台架构设计（IaaS+PaaS+安全的统一运维架构），开发落地，加速内部运维效率与提升生产系统的稳定性。负责重要的基础服务平台如监控平台、作业平台、CMDB、容量管理等运维产品的架构设计。负责容器化（docker&k8s）作为自动化运维的载体，结合业务情况，实现符合公有云、私有云、混合云等各种场景的平台快速部署、交付能力。

**技术栈**：IaaS、PaaS、安全、统一运维架构、监控平台、作业平台、CMDB、容量管理、Docker、K8s

### 岗位7：云平台架构师
精通golang/C++/Java/Python/Shell中的任意一种以上技术语言，熟悉常见的配置管理和运维工具。熟悉HTTP缓存代理服务器（如nginx、Squid、Varnish、TrafficServer等）配置和使用，具备较强的troubleshooting能力。熟悉云计算平台OpenStack、Kubernetes、Mesos、Swarm及docker/kvm/xen等虚拟化技术优先，有管理大规模服务器集群经验优先。

**技术栈**：Golang、C++、Java、Python、Shell、Ansible、Puppet、SaltStack、Nginx、Squid、Varnish、TrafficServer、OpenStack、Kubernetes、Mesos、Swarm

### IaaS技术栈
**虚拟化**：OpenStack、KVM、Xen、Docker、Kubernetes、Mesos、Swarm、Libvirt、Qemu、Nova、Ironic、Cinder、Glance、Neutron、Ceilometer
**编程语言**：Golang、Java、Python、C++、Shell
**数据库**：MySQL、Redis、MongoDB、PostgreSQL、sql调优、lucene引擎
**消息队列**：Kafka、RocketMQ、RabbitMQ、mq消息
**工具**：Ansible、Puppet、SaltStack、Fabric、Prometheus、Grafana、Zabbix
**存储**：Ceph、Manila、Cinder、对象存储、块存储、文件存储、并行文件存储、Rook-Ceph、Longhorn
**网络**：HTTP缓存代理、Nginx、Squid、Varnish、TrafficServer
**框架**：grpc、SpringBoot、SpringCloud、Vue、ElementUI、Gin、Grc
**基础**：多线程、网络、IO、常见算法及数据结构、Linux性能分析及调优

---

## 五、大数据 / 数据平台 SRE 方向

### 岗位1：字节跳动大数据存储HDFS
负责字节跳动大数据存储HDFS的系统高可用架构和规划。设计并实现能够保障线上大规模集群迭代、自动化运维的平台。负责云上数据湖运维体系构建，量化云服务的服务质量，提升服务SLA标准。支持平台用户线上需求和解决用户遇到的各种问题。提升整体云平台的运维管理效率。

**技术栈**：HDFS、高可用架构、自动化运维、云上数据湖、SLA

### 岗位2：大数据PaaS平台
主导大数据PaaS平台建设，以平台产品化和体系化的方式，支撑引擎和数据业务方的稳定性、成本和效率的需求。负责大数据实时、离线计算存储引擎的稳定性、成本和效率方向工作，包括风险管理、变更管控、成本治理、性能优化、运维运营效率提升等方向。深入理解上述平台的架构及其支撑的业务（搜推、广告、风控、AI等），帮助业务在稳定性、成本、效率等方面上做更好的架构设计。

**技术栈**：PaaS平台、Flink、Spark、Ray、Kafka、ClickHouse、Doris、稳定性、成本、效率

### 岗位3：Data Infrastructure SRE
Build and maintain cloud-based Big Data and Analytics Platforms, including Enterprise Data Lake、Data Governance and Management Platforms、Self-service BI and Augmented Analytics Platforms。Proactively managing production services and data pipelines to ensure availability and system health。Improve system reliability through engineering solutions and advanced tooling for monitoring, automation, and fault tolerance。

**技术栈**：Data Lake、Data Governance、Self-service BI、Augmented Analytics、AWS、Huawei Cloud、Python、Terraform、Ansible、Git、Kafka、Spark

### 岗位4：美团大数据SRE
负责美团大数据/机器学习相关组件产品的稳定性保障、资源管理、故障管理等工作。负责大数据/机器学习相关产品的预算统筹规划、资源交付、日常资源调度，深入理解业务场景和需求，主导资源适配方案的设计、测试、验证等工作，并通过工具建设提升资源管理效率。精细化数据运营，包括稳定性指标、事故分析运营、资源使用效率提升等。

**技术栈**：大数据、机器学习、稳定性、资源管理、预算、成本、效率

### 岗位5：大数据运维
负责存储计算服务的运维管理工作，不局限于文件存储、KV存储、批流引擎、消息队列等。负责存储计算相关运维平台的开发维护工作，支撑大数据运维体系化平台建设。深入理解大数据平台架构，发现和解决效率痛点，为存储计算服务的质量建设、成本控制保驾护航。负责分布式业务平台的架构审核、业务监控、持续交付、应急响应、容量规划、性能优化等。

**技术栈**：文件存储、KV存储、批流引擎、消息队列、Hadoop生态、运维平台

### 岗位6：数据平台SRE Team Lead
Lead and mentor a small team of SREs focused on data platform reliability and automation. Design and implement observability solutions for data pipelines and services, including metrics, logging, and tracing。Develop and maintain monitoring dashboards and alerting systems using tools like Grafana, or Huawei Cloud AI/APM。Automate operational tasks to improve efficiency and reduce manual intervention。

**技术栈**：Grafana、Huawei Cloud AI/APM、Huawei AOM/APM、Python、Java、CI/CD、containerization、Terraform、Ansible、Kafka、Spark

### 大数据技术栈
**大数据组件**：Hadoop、HDFS、YARN、Hive、Spark、Flink、HBase、Kafka、Presto、Trino、ClickHouse、Doris、Druid、Elasticsearch、Sqoop、SparkSQL、Airflow、DolphinScheduler、Azkaban
**编程语言**：Java、Scala、Python、Shell、Golang
**存储**：HDFS、Ceph、对象存储、数据湖、S3
**调度**：Airflow、DolphinScheduler、Azkaban
**监控**：Prometheus、Grafana、ELK、OpenTelemetry、Datadog、Huawei Cloud AI/APM
**数据仓库**：Snowflake、Databricks、BigQuery、Redshift、Athena、Glue、Kinesis、MSK

---

## 六、网络 / 负载均衡 / CDN 方向

### 岗位1：接入层架构
负责全站接入层架构设计与维护，包括流量接入、网关迭代更新、接入网络的稳定性和性能优化。对公司业务接入层提供架构设计和技术支持，保障业务流量安全、稳定。优化产品的网络接入性能，用户端性能数据分析，建设国内、海外动态加速、流量调度能力。

**技术栈**：接入层、流量接入、网关、性能优化、动态加速、流量调度

### 岗位2：负载均衡系统
结合业务场景，对公司负载均衡系统进行开发和迭代，保障系统稳定。专线接入网络规划和保障。具备DNS集群运维管理经验，了解anycast、智能DNS和HTTPDNS的工作原理。熟练掌握Linux系统管理、性能调优、shell/python/golang等至少1种语言，有运维工具开发能力。

**技术栈**：负载均衡、DNS集群、anycast、智能DNS、HTTPDNS、专线接入

### 岗位3：腾讯云网络SRE
负责腾讯云机房网络、VPC和负载均衡等网络产品平台的规划、设计与效能优化，不断提升运维效率。负责分析解决网络问题，形成对应方法论，提升团队技术能力。负责通过技术手段和流程制度提升平台网络可用性。识别业务架构或流程中的低效环节，设计并落地优化方案，推动成本与性能双提升。

**技术栈**：VPC、负载均衡、网络产品、SDN、腾讯云、OSPF、BGP

### 岗位4：负载均衡专家
具备两年以上负载均衡建设运维经验，有建设高性能、高可用接入层的研发运维经验。具备DNS集群运维管理经验，了解anycast、智能DNS和HTTPDNS的工作原理。有k8s经验者，有接入网络规划设计和维护经验者优先。

**技术栈**：负载均衡、高性能、高可用、DNS集群、Anycast、k8s

### 网络技术栈
**网络协议**：TCP/IP、HTTP/HTTPS、DNS、HTTPDNS、Anycast、智能DNS、OSPF、BGP、SDN、Overlay/Underlay、Vxlan、SRv6
**负载均衡**：LVS、Nginx、HAProxy、F5、ALB、NLB、SLB、ELB
**网络设备**：路由器、交换机、防火墙
**CDN**：Cloudflare、Akamai、CloudFront、阿里云CDN
**网络工具**：tcpdump、Wireshark、netstat、ss、iperf、awk、sed、grep、strace、gdb

---

## 七、中间件 SRE 方向

### 岗位1：中间件全生命周期管理
负责中间件技术组件的全生命周期管理，包括但不限于如上线评审、部署、配置变更、容量规划、监控及故障应急响应等。参与中间件组件架构的规划、设计，确保平台的高可用性和稳定性。对中间件组件进行性能调优和故障排查，确保快速响应和解决突发事件。

**技术栈**：中间件、全生命周期、上线评审、部署、配置变更、容量规划

### 岗位2：中间件SRE
熟练掌握Redis、Kafka、Pulsar、Elasticsearch、Nginx、Nacos等至少三种以上中间件的架构、配置、运维与优化。熟悉云原生技术栈，包括但不限于Docker、Kubernetes等容器基础技术。熟悉Prometheus、Grafana等监控工具，具备扎实的监控体系建设经验。熟悉至少一门编程语言（如shell、Python、Golang），能够编写自动化运维工具。

**技术栈**：Redis、Kafka、Pulsar、Elasticsearch、Nginx、Nacos、Docker、Kubernetes、Prometheus、Grafana

### 岗位3：监控体系建设
负责监控体系（包括度量指标监控、日志监控、调用链监控）的建设和维护，优化报警规则，保障报警系统的精准性和覆盖范围。负责监控系统的设计、评审、发布并推动产品改进。用自动化、智能化的方法解决超大规模集群、分布式应用及复杂系统运维中的问题。

**技术栈**：度量指标、日志监控、调用链监控、Prometheus、Grafana、ELK、Jaeger、Skywalking

### 岗位4：自动化平台
构建自动化运维平台与工具，提升部署、监控及故障处理效率，推动运维流程标准化。推动周边中间件能力建设，使之标准化、平台化和服务化，确保中间件服务的高效运行。能够基于日常运维痛点拉起和推动周边中间件能力建设。

**技术栈**：自动化运维、平台化、标准化、工具开发

### 岗位5：监控/运维开发
负责维护和开发目前云平台所涉及的监控服务或自动化运维实现，为中间件高可用及高可靠方案负责，保证稳定运行。负责制定中间件相关标准，并支撑研发团队合理规划中间件架构。熟悉Mysql、Redis、MQ、Nginx等中间件，精通其中三种及以上，具备部署及故障排查经验。

**技术栈**：MySQL、Redis、MQ、Nginx、高可用、高可靠、故障排查、架构设计

### 中间件技术栈
**消息队列**：Kafka、RocketMQ、Pulsar、RabbitMQ、MQ
**缓存**：Redis、Memcached
**搜索**：Elasticsearch、Solr、Lucene、ES
**配置中心**：Nacos、Apollo、Etcd、ZooKeeper
**服务治理**：Dubbo、Spring Cloud、gRPC、Sentinel、Gateway
**数据库**：MySQL、PostgreSQL、MongoDB、ClickHouse
**API网关**：Kong、Envoy、Nginx、Spring Cloud Gateway、LinkedR
**监控**：Prometheus、Grafana、ELK、Zabbix、Open-Falcon

---

## 八、DevOps / 平台工程方向

### 岗位1：CI/CD流水线
负责CI/CD流水线设计、DevOps工具链建设、发布平台、可观测平台等研发效能平台的建设。CI/CD与发布体系优化，整合GitLab/Jenkins/ArgoCD等工具链，建设规范化发布流程，实现灰度发布、自动回滚等能力。设计、开发和优化新一代CI/CD流水线平台，实现从代码提交到灰度发布的全程自动化、可观测、可回滚。

**技术栈**：Jenkins、GitLab CI、GitHub Actions、ArgoCD、灰度发布、自动回滚

### 岗位2：运维平台开发
负责运维工具与系统功能模块的开发、测试、维护工作。参与境内外一体化运维平台等系统与工具的建设、需求分析、架构设计工作。参与运维自动化工具的设计、建设以及开发工作，提升运维效率。根据业务需要对DevOps工具链进行定制、插件开发、二次开发等（包括但不限于Gitlab、SonarQube、Jenkins、Jfrog等工具）。

**技术栈**：Gitlab、SonarQube、Jenkins、Jfrog、运维平台、自动化工具

### 岗位3：研发效能平台
构建基于云原生的内部开发者平台，提供自助式的应用部署、环境管理、服务治理能力，提升资源利用率和交付速度。打造研发效能度量体系，通过数据驱动方式识别瓶颈，持续优化代码构建、测试、部署效率。负责代码托管、制品库、自动化测试等工具链的集成、定制与开发。

**技术栈**：云原生、开发者平台、应用部署、环境管理、服务治理、效能度量

### 岗位4：DevOps工程师（Public Cloud）
Develop and deploy solutions in AWS/GCP for achieving different goals (automation of different manual tasks, or a new initiative). Ability to write code (python) so that we may integrate Public Cloud implementation with different systems in the bank. Configure and manage CI/CD pipeline. Proficiency with CI/CD technologies like: Jenkins, Bitbucket etc. Manage and deploy common infrastructure services like Proxy, DNS, Bastion etc in Public Cloud (AWS/GCP).

**技术栈**：AWS、GCP、Python、Jenkins、Bitbucket、CI/CD、Proxy、DNS、Bastion

### 岗位5：平台工程师（Platform Engineer）
Design, implement, and maintain scalable and reliable infrastructure on AWS. Develop and manage CI/CD pipelines to automate deployment and monitoring processes. Implement infrastructure as code (IaC) using tools such as Terraform or AWS CloudFormation. Monitor system performance, availability, and capacity using tools like CloudWatch, Prometheus, Grafana, or similar.

**技术栈**：AWS、CI/CD、IaC、Terraform、CloudFormation、CloudWatch、Prometheus、Grafana

### 岗位6：运维开发-IC Level（Goodnotes）
负责GitHub Actions流水线的搭建与优化；编写高质量Dockerfile与K8s部署模板；持续改进构建效率与部署成功率。负责VKE集群日常运维，包括应用部署、故障排查与性能调优；制定资源配额与多环境隔离规范。使用Terraform管理云资源（VPC、数据库、缓存、对象存储等）。

**技术栈**：GitHub Actions、Dockerfile、K8s、VKE、Terraform、VPC

### 岗位7：平台工程Lead
平台工程设计与实施：领导平台工程的整体设计和实施，确保系统的高效性、可靠性和可扩展性。DevOps流程优化：优化并管理DevOps工作流程，提升开发与运营的协作效率。CI/CD流程管理：设计和维护持续集成和持续交付（CI/CD）管道。模型抽象与整理：将通用的DevOps和平台工程模型进行抽象和整理，形成标准化的解决方案。

**技术栈**：平台工程、CI/CD、DevOps、抽象设计

### DevOps技术栈
**CI/CD**：Jenkins、GitLab CI、GitHub Actions、CircleCI、ArgoCD、Spinnaker、Tekton、GoCD、TeamCity、Bamboo、Bitbucket、Drone
**版本控制**：Git、GitLab、GitHub、Bitbucket、Azure DevOps、GCB、GCR
**制品管理**：Harbor、Nexus、Artifactory、JFrog、ECR、ACR、Docker Hub
**代码质量**：SonarQube、Blackduck、Snyk、Anchore、Trivy、Clair
**IaC**：Terraform、Ansible、Pulumi、CloudFormation、Kustomize、Helm
**监控**：Prometheus、Grafana、ELK、Jaeger、Skywalking、Datadog
**容器**：Docker、Kubernetes、Helm、Kustomize
**编程**：Python、Golang、Java、Shell、Bash、PowerShell、Ruby
**安全**：DevSecOps、TUF、Cosign、Sigstore
**发布**：灰度发布、蓝绿发布、金丝雀发布、自动回滚

---

## 九、数据库 / 存储 SRE 方向

### 岗位1：数据库运维
负责数据库产品交付上线、运维保障、故障诊断、问题处理工作。负责应用服务器及常用中间件，Tomcat/SpringCloud/Nacos/Kafka/MySQL/Redis/ELK等的部署、配置与优化维护。熟悉Oracle、Mysql、OB等任意一项数据库，熟悉信创数据库的优先。掌握常用中间件及常用开源软件工作原理、配置、排障和调优。

**技术栈**：Oracle、MySQL、OB、信创数据库、Tomcat、SpringCloud、Nacos、Kafka、Redis、ELK

### 岗位2：分布式数据库平台
负责分布式数据库产品运维平台和工具的设计、开发工作。用自动化、智能化的方法解决超大规模集群、分布式应用及复杂系统运维中的问题。负责监控系统的设计、评审、发布并推动产品改进。熟悉Java、C/C++、Shell、Python等任一编程语言。

**技术栈**：分布式数据库、运维平台、自动化、Java、C/C++、Shell、Python

### 岗位3：存储运维（苏州北京）
负责存储相关产品的维护工作，对系统可用性负责；主要工作包括投诉、故障等紧急事件的应急处置、监控告警优化、监控数据分析、变更、产品架构及性能优化。具有3年及以上大规模存储集群运维经验，精通manila、cinder等组件的工作原理，有优化集群架构和性能调优经验者优先。熟悉Ceph或Glusterfs整体架构，熟悉Ceph或Glusterfs常用的命令操作和配置。熟悉并行文件存储一体机运维优化。

**技术栈**：manila、cinder、Ceph、GlusterFS、对象存储、块存储、文件存储、并行文件存储

### 岗位4：存储计算服务
负责存储计算服务的运维管理工作，不局限于文件存储、KV存储、批流引擎、消息队列等。负责存储计算相关运维平台的开发维护工作，支撑大数据运维体系化平台建设。深入理解大数据平台架构，发现和解决效率痛点，为存储计算服务的质量建设、成本控制保驾护航。

**技术栈**：文件存储、KV存储、批流引擎、消息队列、Hadoop生态

### 数据库技术栈
**关系型数据库**：MySQL、PostgreSQL、Oracle、SQL Server、TDSQL、GaussDB、OceanBase、MSSQL、OB、信创数据库
**NoSQL**：Redis、MongoDB、Cassandra、DynamoDB、Cosmos DB、Etcd
**时序数据库**：InfluxDB、TimescaleDB、Prometheus
**搜索**：Elasticsearch、Solr、Lucene、ES
**大数据存储**：ClickHouse、Doris、HBase
**分布式存储**：Ceph、GlusterFS、MinIO、S3、对象存储、块存储、文件存储
**工具**：Percona、pt-tools、mysqldump、xtrabackup、pg_dump
**缓存**：Redis、Memcached、KV、NoSql

---

## 十、IoT / 边缘计算方向

### 岗位1：IoT DevOps/SRE
设计、实施和维护IoT基础设施的CI/CD管道，支持设备固件更新、边缘计算和云端部署。管理云平台（AWS IoT Core）上的Kubernetes、Terraform等工具，实现基础设施即代码（IaC）。监控IoT系统性能、设备连接和数据流量，使用Prometheus、Grafana、ELK栈等工具进行实时观测和警报。自动化运维任务，如设备Provisioning、配置管理、自动缩放和灾难恢复。

**技术栈**：IoT、CI/CD、AWS IoT Core、Kubernetes、Terraform、Prometheus、Grafana、ELK

### 岗位2：DevOps/SRE - IoT
与开发、硬件和安全团队协作，集成IoT协议（MQTT、HTTP等）、边缘设备和后端服务。优化系统可靠性，包括负载均衡、容错设计和性能调优，支持海量设备连接。跟踪IoT趋势（如AIoT、AI），并应用到运维优化中。参与on-call轮值，处理生产环境问题，并推动事后回顾（Post-mortem）。

**技术栈**：MQTT、HTTP、边缘设备、负载均衡、容错、AIoT、海量设备

### IoT技术栈
**IoT平台**：AWS IoT Core、Azure IoT Hub、IoT Device Management、HiveMQ
**边缘计算**：KubeEdge、K3s、Balena
**协议**：MQTT、HTTP、CoAP、Modbus
**安全**：GDPR、ETSI EN 303 645、零信任、DevSecOps、秘密管理
**云平台**：AWS、Azure、GCP、阿里云、HKC

---

## 十一、证券 / 金融运维方向

### 岗位1：证券系统运维
负责证券公司集中交易、新一代交易系统的建设与维护，保障业务系统的运行安全。负责运行和信息安全事件、服务事件及服务请求的响应处理；负责运维标准化工作的实施落地。负责系统运行故障定位、排障处理及持续优化，持续完善知识库及应急预案场景。负责落实日常监控措施、监控指标体系的落地；负责监控手段和监控策略的持续改进。

**技术栈**：证券交易、集中交易、新一代交易、信息安全、监控指标体系

### 岗位2：Fintech技术风险
Fintech技术风险能力建设，包含应急能力、变更防御、红蓝攻防、性能容量、资金安全、机房容灾，构建Fintech技术风险体系。参与重大项目的技术风险保障工作，对技术风险领域进行评审和分析。贴身业务，挖掘业务风险，沉淀技术风险领域标杆，释放研发技术风险投入，更聚焦在业务研发上。

**技术栈**：应急能力、变更防御、红蓝攻防、性能容量、资金安全、机房容灾

### 金融技术栈
**数据库**：MSSQL、Oracle、MySQL、TDSQL、GaussDB、OceanBase
**操作系统**：Windows、Linux、CentOS、Ubuntu、Red Hat、Debian
**虚拟化**：KVM、容器、Docker、Kubernetes
**安全**：漏洞扫描、威胁情报、安全加固、等级2.0、等级保
**监控**：Zabbix、Prometheus、Grafana
**工具**：Ansible、自动化运维脚本
**中间件**：Tomcat、Nginx、Java、WebLogic、WebSphere

---

## 技术频率统计

### 容器与云原生（约200次）
- Kubernetes/K8s：约150次
- Docker：约50次
- Istio/Service Mesh：约20次
- Envoy：约8次
- Helm、ArgoCD、Knative等：约30次
- KubeVirt、OpenShift、Rancher：约10次

### 监控与可观测性（约120次）
- Prometheus：约50次
- Grafana：约40次
- ELK/ELK Stack：约30次
- Jaeger/OpenTelemetry：约20次
- Zabbix：约15次
- Loki：约10次
- Skywalking：约10次

### 编程语言（约250次）
- Python：约120次
- Golang/Go：约60次
- Java：约60次
- Shell/Bash：约60次
- C/C++：约30次

### 数据库与缓存（约120次）
- MySQL：约35次
- Redis：约35次
- Kafka：约30次
- Elasticsearch：约25次
- PostgreSQL：约15次
- MongoDB：约12次

### 云平台（约180次）
- AWS：约60次
- 阿里云：约45次
- Azure：约25次
- GCP：约20次

---

## 十二、其他专业方向

### 岗位1：隐私计算架构师
负责隐私计算基础调度框架架构设计和核心功能开发，包括网关、调度器等模块。负责在线与离线任务的方案设计，支持丰富灵活的调度策略。负责多云集成开发、降低上云门槛。负责服务持续交付、故障容灾、监控告警、链路追踪等稳定性和可用性能力建设。熟悉TEE、MPC、ZKP、DP、FL等主流隐私计算技术优先。熟悉Envoy、Kubernetes，如CRD、Operator、K8s Controller等。

**技术栈**：TEE、MPC、ZKP、DP、FL、Envoy、Kubernetes、CRD、Operator

### 岗位2：RAG增强检索
参与云原生应用研发项目，包括机器学习/RAG增强检索/可观测性/弹性混部/DevOps等。熟悉LLM原理，特别是上下文工程、KVCache机制及Prompt优化策略。熟悉Agent Memory、RAG相关技术。具备以下条件者优先：有大型k8s集群治理和集群管理平台研发经验；熟悉底层技术（网络/虚拟化），如负载均衡、SDN/overlay/vxlan、kvm/kubevirt等。

**技术栈**：RAG、LLM、上下文工程、KV Cache、Prompt优化、Agent Memory

### 岗位3：业务运维专家（vivo）
负责vivo互联网业务系统的运维工作；负责业务系统可用性建设并对结果负责。建立并持续优化监控告警体系，及时发现业务系统异常，并快速止损恢复。根据业务发展和运行情况，对业务系统的部署进行架构调整和优化。制定和推行运维技术标准、规范与最佳实践（如监控规范、发布流程、容量模型）。

**技术栈**：监控告警、容量模型、监控规范、发布流程、运维自动化

### 岗位4：搜索推荐AI Infra
负责电商搜推领域的AI infra平台的架构设计、研发和维护工作，建设一站式的低代码/可视化的研发和部署平台。有低代码平台、PAAS平台、devops平台、机器学习平台-推理部分等建设经验者优先。精通go、python等一门后端语言，具备扎实的计算机理论基础、卓越的编码能力与基础算法功底。

**技术栈**：go、python、低代码、PAAS、devops平台、机器学习平台

### 岗位5：自动驾驶运维
负责智驾平台计算服务日常运维工作，参与K8S混合云服务、计算应用、多种类GPU/CPU等资源服务的自动化能力建设、成本管控和稳定性保障等。熟练掌握Docker/K8S容器化相关技术、架构与原理，熟练运用K8S运维管理工具kubectl、Helm、kubeadm、Nacos、ArgoCD、Rancher等内容。有K8S平台运维管理经验，多型GPU维护管理经验、文件对象存储使用经验或有云运维管理经验者优先。

**技术栈**：Docker、K8S、kubectl、Helm、kubeadm、Nacos、ArgoCD、Rancher、GPU

### 岗位6：AI Infra算法工程
负责AI算法框架的深度优化和开发，识别和定位相关模型训练推理和系统的性能瓶颈，优化CPU/GPU内存/通信等资源利用率，提升并行计算并发效率。负责研究深度学习、LLM和性能加速的最新发展趋势，将前沿的算法和优化技术应用到业务场景。熟悉PyTorch、DeepSpeed、Megatron、vLLM和SGLang等深度学习训练推理框架，熟练掌握深度学习性能加速技术，包括计算图优化、低精度优化、算子加速，以及DP/TP/PP/SP/EP等并行加速技术。

**技术栈**：PyTorch、DeepSpeed、Megatron、vLLM、SGLang、DP/TP/PP/SP/EP、算子加速

### 岗位7：AI Infra存储专家
负责AI Infra数据编排调度服务基础组件的研究开发工作。负责AI Infra GPU集群IO性能统计跟踪，数据缓存系统的研究优化工作。负责AI Infra GPU集群各服务压力承载能力建设，提高整体SLA水平的研究优化工作。熟悉分布式存储系统的原理和架构设计，有文件系统或对象存储开发经验。熟悉至少一种编程语言：Go、C/C++、Rust。熟悉Linux操作系统，具备内核文件系统、IO子系统或网络协议栈。

**技术栈**：分布式存储、文件系统、对象存储、Go、C/C++、Rust、内核

### 岗位8：制造DevOps AI（特斯拉）
负责AI算法研发、模型优化与训练，聚焦生产线数据分析、质量控制、故障检测、自动化生产等场景，确保AI技术适配制造业务需求。基于Kubernetes（K8s）与Docker容器技术，完成AI解决方案的部署、监控与扩展，保障生产环境中系统的高可用性与稳定性。参与DevOps流程建设，优化AI模型与系统的开发、测试、部署全链路，实现自动化部署、持续集成（CI）与持续交付（CD）。

**技术栈**：Kubernetes、Docker、CI/CD、生产线、质量控制、故障检测、自动化生产

### 岗位9：百度SRE
Site Reliability Engineer，负责百度公司大规模分布式系统及各类在线服务可靠、稳定、高效运行。参与在线系统和各类产品架构设计，主导服务可靠性相关自动化系统的实现，满足严格的质量与效率要求。参与百度国内外整体机房建设，为产品用户提供最优质的接入与使用体验布局。设计研发服务运维解决方案，包括网站加速、持续交付、容量管理、弹性计算、故障分析、流量分配、性能调优等。

**技术栈**：分布式系统、在线服务、网站加速、持续交付、容量管理、弹性计算

### 岗位10：滴滴网约车SRE
负责滴滴网约车线上业务的日常运维、性能优化及容量管理等工作，建立7×24小时高可用保障机制，保障业务稳定运行。负责网约车业务服务模块全生命周期管理，包括服务准入、模块交付、服务放量、稳定性保障等，支撑千万级流量。分析评估网约车对基础设施的合理需求并推进落地，涵盖网络、统一接入、中间件、存储、监控、部署等。推进运维流程标准化、自动化。

**技术栈**：7×24、高可用、千万级流量、全生命周期、网络、中间件、存储、监控

### 岗位11：高德SRE
负责高德的基础运维工作，提高自动化运维水平、故障响应能力、优化资源使用率。优化线上技术架构，从运维角度参与并推动研发、产品改进架构体系。参与运维支撑平台的建设，运维相关的新技术的研究，从提升开发效率、降低运维人力成本出发，设计并搭建运维平台。精通linux文件系统、内核、linux性能调优、TCP/IP、HTTP等协议。

**技术栈**：自动化运维、故障响应、资源优化、Linux内核、性能调优、TCP/IP

### 岗位12：NVIDIA SRE
该角色涉及设计、构建和维护服务，以实现实时数据分析、流媒体、数据湖、可观测性和ML/AI训练与推理。职责包括实施软件和系统工程实践，确保平台的高效率和可用性，以及应用SRE原则来改进生产系统和优化服务SLO。开发软件解决方案，确保支持机器关键用例的大规模系统的可靠性和可操作性。监督容量和性能管理，促进全球公共和私有云基础设施的扩展。

**技术栈**：实时数据分析、流媒体、数据湖、可观测性、ML/AI训练推理、Kafka、Spark

### 岗位13：安全产品研发
负责安全产品的设计、开发和验证。负责安全技术原型开发，如可信计算、入侵检测、数据安全与隐私、AI安全、国密等。具备扎实的C/C++/Go/python/JAVA/Rust等编程语言功底。具备网络安全经验更佳。对新技术和新产品有强烈的兴趣和热情。

**技术栈**：C/C++、Go、Python、JAVA、Rust、可信计算、入侵检测、数据安全、AI安全

### 岗位14：AI集群调度
设计和实现GPU算力调度系统，优化资源利用率和作业调度效率。负责Kubernetes节点组件（kubelet、container runtime）的稳定性、性能优化。深度排查Kubernetes集群复杂问题。参与服务器硬件选型、测试和验收，重点优化GPU服务器性能。推进国产AI芯片的生态适配。建立集群故障感知闭环体系，提高AI计算资源利用率，维护线上集群稳定性。

**技术栈**：GPU调度、Kubernetes、kubelet、container runtime、NVIDIA驱动、MIG分区、国产AI芯片

### 岗位15：云原生架构师
负责云端基础设施的建设及优化。开发和维护自动化运维平台，提高运维、开发协作效率，规范操作流程。负责云端各组件的日常告警处理、线上变更及故障处理，保障线上服务稳定。有GPU集群运维经验者优先。具备较强的团队沟通与协作能力，有技术进取心和前瞻性。

**技术栈**：云端基础设施、自动化运维平台、GPU集群

---

## 技术频率统计

### 容器与云原生（约200次）
- Kubernetes/K8s：约150次
- Docker：约50次
- Istio/Service Mesh：约20次
- Envoy：约8次
- Helm、ArgoCD、Knative等：约30次
- KubeVirt、OpenShift、Rancher：约10次

### 监控与可观测性（约120次）
- Prometheus：约50次
- Grafana：约40次
- ELK/ELK Stack：约30次
- Jaeger/OpenTelemetry：约20次
- Zabbix：约15次
- Loki：约10次
- Skywalking：约10次
- Splunk、Datadog：约5次

### 编程语言（约250次）
- Python：约120次
- Golang/Go：约60次
- Java：约60次
- Shell/Bash：约60次
- C/C++：约30次
- 其他（PowerShell、Perl、Ruby等）：约10次

### 数据库与缓存（约120次）
- MySQL：约35次
- Redis：约35次
- Kafka：约30次
- Elasticsearch：约25次
- PostgreSQL：约15次
- MongoDB：约12次
- ClickHouse/Doris：约12次
- Oracle、SQL Server、TDSQL、GaussDB：约20次

### 中间件与工具（约150次）
- Nginx：约25次
- Jenkins：约30次
- GitLab：约25次
- Ansible：约25次
- Terraform：约20次
- ArgoCD：约12次
- RocketMQ、Pulsar：约15次
- RabbitMQ：约8次
- ZooKeeper、Etcd：约10次
- Nacos、Apollo：约10次
- Harbor、Nexus、Artifactory：约10次

### 云平台（约180次）
- AWS：约60次
- 阿里云：约45次
- Azure：约25次
- GCP：约20次
- 腾讯云/华为云/火山云：约30次

### 大数据组件（约60次）
- Hadoop/Spark：约25次
- Flink：约12次
- Kafka：约30次（已计入中间件）
- Hive/HBase：约12次
- Trino、Presto：约5次
- Airflow、DolphinScheduler：约5次

### 网络与安全（约70次）
- TCP/IP、HTTP：约35次
- DNS/CDN：约18次
- IAM/RBAC/SSO：约15次
- VPC/负载均衡：约25次
- eBPF、DPDK：约8次

### AI/ML相关（约40次）
- vLLM、SGLang：约8次
- PyTorch、TensorFlow：约15次
- GPU/CUDA/RDMA：约20次
- DeepSpeed、Megatron：约5次
- Agent、RAG：约8次

---

*压缩说明：本版本从原始2946行压缩至约800行*
*1. 移除了通用要求（如"本科及以上"、"良好的沟通能力"等数百次重复）*
*2. 移除了冗余的软技能要求*
*3. 合并了完全相同的岗位描述*
*4. 按技术方向重新组织内容*
*5. 保留了所有技术栈及其相对出现频率*

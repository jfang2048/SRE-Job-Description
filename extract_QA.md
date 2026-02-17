# 云原生AI/LLM平台基础设施工程师 - 面试&工业界能力拓展指南
## 一、总体结论（招聘市场真实能力模型）
### 岗位核心定位
**Cloud Native Infrastructure Engineer for AI / LLM platform**
核心职责：
- 运行超大规模 Kubernetes 集群
- 管理 GPU / HPC 资源
- 构建自动化交付与运维体系
- 优化 AI 训练与推理基础设施
- 做性能调优与可靠性工程
- 平台工程 + 调度 + 系统优化

岗位能力本质：
```
Kubernetes platform engineer
+ SRE
+ distributed systems
+ GPU cluster infra
+ performance engineer
```

### 面试高频追问
1. 请简述你理解的AI/LLM平台基础设施工程师和传统K8s运维工程师的核心区别？
2. 你过往做过的最复杂的K8s+GPU集群运维案例是什么？核心挑战和解决方案是什么？
3. 站在LLM推理优化的角度，你认为云原生基础设施层能做哪些核心优化？

### 工业界核心落地场景
1. 支撑日均万卡级GPU集群的LLM训练/推理任务调度与资源管理
2. 构建从代码提交到模型部署的全流程GitOps自动化流水线
3. 保障LLM推理服务99.99%以上的可用性，同时控制GPU资源利用率≥80%
4. 针对千亿参数大模型推理做KVCache、显存调度等底层优化

## 二、技术能力频率排序（面试+工业界权重）
### 第一层（必须掌握，所有岗位共同核心）
#### 1️⃣ Kubernetes（绝对核心中的核心）
几乎100%岗位要求，企业级要求远不止“会用”，需达到“源码级理解+生产级落地”水平。

##### 架构与核心机制
| 核心知识点 | 面试高频问题 | 工业界落地场景 |
|------------|--------------|----------------|
| kube-apiserver | 1. kube-apiserver的限流机制有哪些？<br>2. 如何优化apiserver的QPS性能？<br>3. apiserver的etcd缓存机制原理？ | 1. 超大规模集群（万节点）apiserver水平扩展<br>2. 基于apiserver audit日志做权限审计与异常检测<br>3. 针对AI任务定制apiserver的资源访问策略 |
| etcd | 1. etcd的Raft协议核心流程？<br>2. etcd的性能调优参数有哪些？<br>3. etcd数据分片/备份/恢复方案？ | 1. 生产环境etcd集群跨区域高可用部署<br>2. 针对K8s事件风暴的etcd读写优化<br>3. etcd存储容量规划与碎片整理 |
| scheduler | 1. 默认调度器的调度流程（预选+优选）？<br>2. 如何解决调度器的“饥饿”问题？<br>3. 调度器的性能瓶颈如何优化？ | 1. 大规模GPU集群的调度器性能调优（万级Pod调度）<br>2. 基于节点GPU负载的调度器优选策略定制<br>3. 调度器与GPU资源预留的协同设计 |
| controller-manager | 1. Controller的Reconciliation Loop原理？<br>2. 如何避免Controller的reconcile风暴？<br>3. 自定义Controller的开发注意事项？ | 1. 基于Controller实现GPU资源的生命周期管理<br>2. 定制StatefulSet Controller适配LLM训练任务<br>3. Controller的并发度调优与故障自愈 |
| kubelet | 1. kubelet的Pod生命周期管理流程？<br>2. kubelet的资源隔离机制？<br>3. 如何排查kubelet与containerd通信异常？ | 1. 针对GPU节点的kubelet参数调优（如容器启动超时）<br>2. kubelet的监控指标定制与异常告警<br>3. 离线节点的kubelet状态恢复方案 |
| container runtime (containerd) | 1. containerd的架构（shim/runc/CRI）？<br>2. containerd的镜像拉取优化？<br>3. 如何排查containerd容器启动失败？ | 1. 生产环境containerd的多版本兼容部署<br>2. 基于containerd的GPU容器镜像加速<br>3. containerd的日志采集与问题定位 |
| 调度流程 | 1. Pod的完整调度链路（从创建到运行）？<br>2. 调度失败的常见原因与排查方法？<br>3. 如何实现Pod的跨节点迁移？ | 1. LLM训练任务的调度优先级设计<br>2. 基于调度流程的GPU碎片整理策略<br>3. 调度器与节点亲和性的冲突解决 |
| controller reconciliation loop | 1. Reconciliation Loop的指数退避机制？<br>2. 如何保证Controller的幂等性？<br>3. Controller的事件触发机制？ | 1. 定制Controller实现LLM推理服务的自动扩缩容<br>2. 基于Reconciliation Loop的集群配置一致性校验<br>3. Controller的故障重试策略设计 |

##### 工作负载模型
| 核心知识点 | 面试高频问题 | 工业界落地场景 |
|------------|--------------|----------------|
| Pod lifecycle | 1. Pod的全生命周期阶段（Pending/Running等）？<br>2. Pod的探针（liveness/readiness/startup）设计原则？<br>3. 如何处理Pod的优雅退出？ | 1. LLM推理Pod的探针定制（基于推理延迟的readiness）<br>2. Pod终止时的GPU显存释放优化<br>3. 基于Pod生命周期的故障自动恢复 |
| Deployment / StatefulSet | 1. Deployment与StatefulSet的核心区别？<br>2. StatefulSet的Headless Service作用？<br>3. Deployment的滚动升级策略调优？ | 1. LLM推理服务用Deployment的灰度发布设计<br>2. 分布式训练任务用StatefulSet的网络拓扑设计<br>3. StatefulSet的PVC持久化与数据备份 |
| DaemonSet | 1. DaemonSet的调度策略？<br>2. 如何限制DaemonSet的资源占用？<br>3. DaemonSet的更新策略？ | 1. GPU节点的监控Agent用DaemonSet部署<br>2. 基于DaemonSet的节点GPU驱动统一管理<br>3. DaemonSet的故障隔离与升级回滚 |
| Job / CronJob | 1. Job的并行度与完成策略？<br>2. CronJob的时区问题与执行策略？<br>3. 如何处理失败的Job？ | 1. LLM微调任务用Job的批量调度<br>2. CronJob实现GPU集群的定期健康检查<br>3. 大规模Job的资源限制与优先级管理 |

##### 网络
| 核心知识点 | 面试高频问题 | 工业界落地场景 |
|------------|--------------|----------------|
| CNI原理 | 1. CNI的调用流程（Add/Del/Check）？<br>2. 常用CNI插件（Calico/Flannel）的区别？<br>3. 如何开发自定义CNI插件？ | 1. 基于Calico的GPU节点网络策略定制<br>2. CNI插件的性能调优（如减少Pod启动网络耗时）<br>3. 多集群CNI的互通设计 |
| Overlay vs Underlay | 1. Overlay网络的封装开销？<br>2. Underlay网络的适用场景？<br>3. 如何选择Overlay/Underlay？ | 1. LLM训练集群用Underlay网络（RDMA）<br>2. 推理服务用Overlay网络的多租户隔离<br>3. 混合网络模式的流量调度设计 |
| Service / kube-proxy | 1. Service的四种类型（ClusterIP/NodePort等）？<br>2. kube-proxy的iptables/ipvs模式区别？<br>3. Service的会话保持实现？ | 1. LLM推理服务用NodePort/LoadBalancer暴露<br>2. kube-proxy ipvs模式的性能调优<br>3. 基于Service的流量限流与负载均衡 |
| Ingress / Gateway | 1. Ingress与Gateway API的区别？<br>2. 常用Ingress控制器（Nginx/Traefik）调优？<br>3. 如何实现Ingress的灰度发布？ | 1. LLM推理服务的Ingress七层路由设计<br>2. Gateway API的多租户LLM服务隔离<br>3. Ingress的TLS终止与性能优化 |
| 网络策略 | 1. NetworkPolicy的匹配规则？<br>2. 如何实现Pod间的网络隔离？<br>3. NetworkPolicy的性能影响？ | 1. GPU集群的网络策略（限制训练节点访问）<br>2. 多租户LLM平台的网络隔离策略<br>3. NetworkPolicy的审计与合规检查 |

##### 集群运维
| 核心知识点 | 面试高频问题 | 工业界落地场景 |
|------------|--------------|----------------|
| 多集群管理 | 1. 多集群管理方案（Karmada/ClusterAPI）？<br>2. 多集群的资源同步策略？<br>3. 跨集群的服务发现？ | 1. 多地域GPU集群的统一管理（Karmada）<br>2. 跨集群的LLM训练任务调度<br>3. 多集群的配置一致性校验 |
| HA部署 | 1. K8s集群HA的核心组件部署策略？<br>2. 如何测试HA集群的故障转移？<br>3. HA集群的脑裂问题如何避免？ | 1. 生产级GPU集群的K8s HA部署（3主+多节点）<br>2. HA集群的故障自动切换演练<br>3. etcd集群的HA与数据一致性保障 |
| 滚动升级 | 1. K8s版本升级的注意事项？<br>2. 滚动升级的暂停/继续/回滚策略？<br>3. 升级过程中的风险点？ | 1. GPU集群的K8s版本无痛升级<br>2. 升级过程中LLM服务的可用性保障<br>3. 升级失败的回滚预案设计 |
| 容量规划 | 1. K8s集群的容量评估指标？<br>2. 如何避免集群资源碎片？<br>3. GPU集群的容量规划方法？ | 1. 基于历史数据的GPU集群容量预测<br>2. 集群资源碎片的自动整理策略<br>3. LLM推理服务的弹性容量规划 |
| 故障排查 | 1. K8s集群故障排查的核心思路？<br>2. 常见故障（Pod无法调度/网络不通）排查步骤？<br>3. 如何定位GPU Pod的故障？ | 1. 生产环境K8s集群故障排查手册制定<br>2. 基于日志/监控的故障自动定位<br>3. GPU Pod启动失败的根因分析（RCA） |

##### 高级能力（招聘强烈偏好）
| 核心知识点 | 面试高频问题 | 工业界落地场景 |
|------------|--------------|----------------|
| Operator / CRD开发 | 1. CRD的定义与验证机制？<br>2. Operator的开发框架（kubebuilder/operator-sdk）？<br>3. Operator的状态管理？ | 1. 定制GPU Operator管理GPU驱动/插件<br>2. LLM推理服务Operator的开发（自动扩缩容）<br>3. Operator的高可用与故障自愈设计 |
| scheduler扩展 | 1. Scheduler Framework的扩展点？<br>2. 如何开发调度器插件？<br>3. 调度器插件的优先级设计？ | 1. 基于GPU显存利用率的调度器插件<br>2. LLM训练任务的拓扑感知调度插件<br>3. 调度器插件的性能调优与冲突解决 |
| kubelet调优 | 1. kubelet的核心参数（--max-pods等）调优？<br>2. kubelet的资源监控粒度调整？<br>3. kubelet的垃圾回收策略？ | 1. GPU节点kubelet的pod数量上限调优<br>2. kubelet的GPU指标采集频率优化<br>3. kubelet的镜像垃圾回收策略定制 |
| control plane性能优化 | 1. control plane的性能瓶颈点？<br>2. apiserver/etcd/scheduler的调优组合？<br>3. 大规模集群control plane的水平扩展？ | 1. 万节点GPU集群control plane的性能调优<br>2. control plane的监控指标定制与告警<br>3. control plane的资源隔离（CPU/内存） |
| 集群网络调优 | 1. 集群网络的延迟/吞吐优化？<br>2. RDMA在K8s集群的落地？<br>3. eBPF在网络调优中的应用？ | 1. LLM训练集群的RDMA网络调优<br>2. 基于eBPF的网络流量监控与优化<br>3. 集群网络的MTU调优与分片控制 |
| GPU调度 | 1. K8s的GPU调度机制（nvidia-device-plugin）？<br>2. 如何实现GPU显存的精细化调度？<br>3. 多租户GPU共享的调度策略？ | 1. 基于GPU算力/显存的多维度调度<br>2. LLM推理任务的GPU共享调度（如vGPU）<br>3. GPU调度的优先级与抢占机制设计 |
| GitOps (ArgoCD / Flux) | 1. ArgoCD的核心组件与同步机制？<br>2. Flux与ArgoCD的区别？<br>3. GitOps的回滚策略？ | 1. LLM平台的全流程GitOps（代码-配置-部署）<br>2. ArgoCD的多集群同步与权限控制<br>3. GitOps的审计日志与合规检查 |

##### 平台工程
| 核心知识点 | 面试高频问题 | 工业界落地场景 |
|------------|--------------|----------------|
| 多租户 | 1. K8s多租户的实现方案（命名空间/集群）？<br>2. 多租户的资源隔离机制？<br>3. 多租户的权限管理？ | 1. LLM平台的多租户隔离（命名空间+网络策略）<br>2. 多租户的GPU资源配额与计费<br>3. 多租户的日志/监控隔离 |
| quota | 1. ResourceQuota与LimitRange的区别？<br>2. 如何设置GPU资源的quota？<br>3. quota的超限处理策略？ | 1. 多租户LLM平台的GPU quota管理<br>2. 基于quota的资源弹性调整<br>3. quota的监控告警与超限额预警 |
| RBAC | 1. RBAC的核心概念（Role/ClusterRole等）？<br>2. 如何设计最小权限的RBAC策略？<br>3. RBAC的审计与权限回收？ | 1. LLM平台的RBAC权限体系设计<br>2. 基于RBAC的GPU资源访问控制<br>3. RBAC的自动权限巡检与合规校验 |
| policy engine (Kyverno / Gatekeeper) | 1. Kyverno与Gatekeeper的区别？<br>2. 如何编写策略校验GPU Pod配置？<br>3. 策略的强制执行与审计模式？ | 1. 基于Kyverno的GPU Pod安全策略校验<br>2. Gatekeeper的多集群策略统一管理<br>3. 策略的灰度发布与故障回滚 |

#### 2️⃣ Linux系统基础（深度要求）
不是“会命令”，是**内核级理解**，需能基于内核原理解决生产环境问题。

| 核心知识点 | 面试高频问题 | 工业界落地场景 |
|------------|--------------|----------------|
| 进程模型 | 1. Linux进程的生命周期（fork/exec/exit）？<br>2. 进程的调度策略（CFS/实时调度）？<br>3. 僵尸进程/孤儿进程的产生与处理？ | 1. LLM推理进程的调度策略调优（实时调度）<br>2. 进程资源限制（ulimit）的生产配置<br>3. 大规模GPU进程的监控与异常终止处理 |
| 内存管理 | 1. Linux内存管理机制（页表/交换区/缓存）？<br>2. OOM killer的触发机制与调优？<br>3. 大页内存（HugePage）的配置与应用？ | 1. GPU节点的大页内存配置（提升LLM推理性能）<br>2. OOM killer的规则定制（避免杀死核心LLM进程）<br>3. 内存泄漏的排查与定位（strace/perf） |
| 文件系统 | 1. 常见文件系统（ext4/xfs）的区别？<br>2. 文件系统的挂载参数调优？<br>3. 分布式文件系统（Lustre）的适配？ | 1. GPU节点的XFS文件系统调优（提升数据读写）<br>2. LLM训练数据的文件系统缓存策略<br>3. 文件系统的IO监控与性能瓶颈定位 |
| TCP/IP栈 | 1. TCP的三次握手/四次挥手？<br>2. TCP的拥塞控制算法（CUBIC/BBR）？<br>3. UDP在LLM训练中的应用？ | 1. GPU集群的TCP BBR算法调优（提升传输速度）<br>2. TCP连接数调优（支撑大规模LLM服务）<br>3. RDMA基于UDP的传输优化 |
| namespace | 1. Linux的6种namespace（PID/Network等）？<br>2. namespace的隔离原理？<br>3. 如何手动创建namespace？ | 1. 容器namespace的底层隔离机制排查<br>2. GPU资源的namespace隔离定制<br>3. 多租户LLM服务的namespace隔离 |
| cgroup | 1. cgroup v1/v2的区别？<br>2. cgroup的资源控制（CPU/内存/GPU）？<br>3. cgroup的层级结构？ | 1. GPU节点的cgroup v2配置（精细化资源控制）<br>2. LLM进程的cgroup资源限制<br>3. cgroup的监控指标采集与告警 |
| system call | 1. 常见系统调用（read/write/fork）？<br>2. 系统调用的性能优化？<br>3. strace如何追踪系统调用？ | 1. LLM推理进程的系统调用优化（减少IO耗时）<br>2. 基于strace的LLM进程故障排查<br>3. 系统调用的权限控制与审计 |
| 网络调试 | 1. tcpdump/wireshark的常用过滤规则？<br>2. 如何定位TCP连接超时问题？<br>3. RDMA网络的调试方法？ | 1. GPU集群网络丢包的tcpdump排查<br>2. LLM推理服务的网络延迟定位<br>3. RDMA连接异常的调试与修复 |
| 性能分析 | 1. perf的核心使用场景（CPU/内存/IO）？<br>2. eBPF的性能分析工具（bpftrace）？<br>3. 如何分析GPU节点的CPU瓶颈？ | 1. LLM推理进程的perf性能剖析<br>2. 基于eBPF的GPU节点IO监控<br>3. 大规模集群的性能基线与异常检测 |

##### 常用诊断工具
| 工具 | 面试高频问题 | 工业界落地场景 |
|------|--------------|----------------|
| strace | 1. strace的核心参数（-p/-e/-t）？<br>2. 如何用strace排查进程卡死问题？<br>3. strace的性能开销如何控制？ | 1. LLM推理进程启动失败的strace排查<br>2. 追踪GPU驱动进程的系统调用<br>3. strace日志的自动化分析与告警 |
| gdb | 1. gdb的核心调试命令（break/next/print）？<br>2. 如何调试核心转储文件（core dump）？<br>3. 如何调试Go语言编写的K8s组件？ | 1. K8s组件崩溃的core dump分析<br>2. GPU驱动内核模块的gdb调试<br>3. 自定义Operator的gdb调试 |
| perf | 1. perf stat/perf record/perf report的区别？<br>2. 如何用perf定位CPU热点函数？<br>3. perf如何分析内存访问？ | 1. LLM推理进程的CPU热点分析<br>2. K8s scheduler的perf性能剖析<br>3. GPU节点的perf事件监控 |
| tcpdump | 1. tcpdump的过滤规则（端口/协议/IP）？<br>2. 如何抓取RDMA流量？<br>3. tcpdump的输出格式解析？ | 1. GPU集群间的TCP流量抓取与分析<br>2. LLM训练数据传输的丢包排查<br>3. tcpdump日志的自动化解析与存储 |
| wireshark | 1. wireshark的常用分析功能（统计/过滤）？<br>2. 如何分析TCP重传问题？<br>3. wireshark与tcpdump的协同使用？ | 1. LLM推理服务的HTTP/GRPC流量分析<br>2. RDMA协议的wireshark解析<br>3. 网络故障的可视化分析报告 |
| ebpf | 1. eBPF的核心原理与应用场景？<br>2. 常用eBPF工具（bcc/bpftrace）？<br>3. eBPF在K8s中的应用？ | 1. 基于eBPF的GPU节点网络监控<br>2. eBPF实现LLM进程的IO限流<br>3. eBPF的K8s容器安全审计 |

#### 3️⃣ Container技术
必须理解底层实现，能解决容器运行时的核心问题。

| 核心知识点 | 面试高频问题 | 工业界落地场景 |
|------------|--------------|----------------|
| namespace隔离 | 1. 6种namespace的隔离范围？<br>2. namespace的嵌套与共享？<br>3. 如何突破namespace隔离？ | 1. GPU容器的PID/Network namespace隔离<br>2. 多租户LLM容器的namespace隔离加固<br>3. namespace隔离的安全审计 |
| cgroup资源控制 | 1. cgroup v2的资源控制能力？<br>2. 如何限制容器的GPU使用？<br>3. cgroup的统计信息采集？ | 1. LLM容器的GPU显存cgroup限制<br>2. 容器CPU/内存的cgroup精细化控制<br>3. cgroup的资源使用监控与告警 |
| image layering | 1. 容器镜像的分层原理（Copy-on-Write）？<br>2. 如何优化镜像层的大小？<br>3. 镜像分层的缓存策略？ | 1. LLM模型镜像的分层优化（基础层+模型层）<br>2. 镜像分层的增量更新策略<br>3. 镜像层的安全扫描与漏洞检测 |
| runtime (runc / containerd) | 1. runc的核心流程（create/start/delete）？<br>2. containerd的架构（shim/CRI）？<br>3. runc与containerd的版本兼容？ | 1. 生产环境containerd的高可用部署<br>2. runc的安全配置（seccomp/apparmor）<br>3. containerd的镜像加速与缓存 |

##### 企业级要求
| 核心要求 | 面试高频问题 | 工业界落地场景 |
|----------|--------------|----------------|
| 镜像安全扫描 | 1. 常用镜像扫描工具（Trivy/Clair）？<br>2. 镜像漏洞的分级与处理策略？<br>3. 如何集成扫描到CI/CD？ | 1. LLM模型镜像的自动化安全扫描<br>2. 镜像漏洞的实时告警与修复<br>3. 扫描结果的合规审计与报告 |
| 镜像仓库管理 | 1. 私有镜像仓库（Harbor）的部署与调优？<br>2. 镜像仓库的权限控制？<br>3. 镜像的生命周期管理？ | 1. 企业级Harbor集群的高可用部署<br>2. LLM镜像的多版本管理与回滚<br>3. 镜像仓库的缓存与同步策略 |
| 容器启动性能 | 1. 容器启动慢的常见原因？<br>2. 如何优化容器启动时间？<br>3. GPU容器的启动优化？ | 1. LLM推理容器的启动加速（镜像预拉取）<br>2. 容器启动的并行化优化<br>3. GPU驱动预加载减少容器启动耗时 |
| runtime调优 | 1. containerd的配置参数调优？<br>2. runc的性能优化？<br>3. 运行时的监控指标采集？ | 1. 生产环境containerd的并发度调优<br>2. runc的seccomp规则优化（减少开销）<br>3. 运行时的异常监控与自动恢复 |

#### 4️⃣ DevOps / CI/CD / Platform Engineering
企业全部要求自动化交付，需能设计端到端的自动化流水线。

| 核心知识点 | 面试高频问题 | 工业界落地场景 |
|------------|--------------|----------------|
| pipeline设计 | 1. CI/CD流水线的核心阶段（构建/测试/部署）？<br>2. 如何设计高可用的流水线？<br>3. 流水线的并行化优化？ | 1. LLM平台的全流程CI/CD（代码-镜像-部署）<br>2. 多环境（测试/预发/生产）的流水线设计<br>3. 流水线的故障自动重试与回滚 |
| artifact管理 | 1. 制品（镜像/二进制/模型）的版本管理？<br>2. 制品仓库的高可用部署？<br>3. 制品的追溯与审计？ | 1. LLM模型制品的版本化管理<br>2. 多地域制品仓库的同步策略<br>3. 制品的完整性校验与防篡改 |
| GitOps | 1. GitOps的核心原则（声明式/版本控制）？<br>2. ArgoCD/Flux的落地实践？<br>3. GitOps的回滚与审计？ | 1. LLM平台的GitOps全流程落地<br>2. 多集群GitOps的配置同步<br>3. GitOps的操作审计与合规检查 |
| 环境管理 | 1. 多环境的隔离策略（命名空间/集群）？<br>2. 环境配置的管理（ConfigMap/Secret）？<br>3. 环境的一键部署与销毁？ | 1. LLM平台的多环境（开发/测试/生产）隔离<br>2. 环境配置的加密存储与注入<br>3. 临时测试环境的自动销毁 |

##### 常见工具
| 工具 | 面试高频问题 | 工业界落地场景 |
|------|--------------|----------------|
| Jenkins | 1. Jenkins的流水线语法（Declarative）？<br>2. Jenkins的插件管理与调优？<br>3. Jenkins的高可用部署？ | 1. LLM训练任务的Jenkins流水线<br>2. Jenkins与GitLab的集成（webhook）<br>3. Jenkins的构建节点资源隔离 |
| GitLab CI | 1. GitLab CI的.gitlab-ci.yml语法？<br>2. GitLab Runner的部署与调优？<br>3. 如何实现CI/CD的缓存？ | 1. LLM平台代码的GitLab CI自动化<br>2. GitLab Runner的GPU节点适配<br>3. CI/CD缓存的优化（模型依赖） |
| ArgoCD | 1. ArgoCD的同步策略（自动/手动）？<br>2. ArgoCD的应用健康检查？<br>3. ArgoCD的多集群管理？ | 1. LLM推理服务的ArgoCD持续部署<br>2. ArgoCD的回滚策略与演练<br>3. ArgoCD的RBAC权限控制 |
| Tekton | 1. Tekton的核心资源（Task/Pipeline）？<br>2. Tekton与K8s的原生集成？<br>3. Tekton的性能调优？ | 1. 云原生LLM平台的Tekton流水线<br>2. Tekton的Task复用与参数化<br>3. Tekton的并行任务调度优化 |
| Helm | 1. Helm的Chart结构与模板？<br>2. Helm的版本管理与回滚？<br>3. Helm的钩子（Hook）使用？ | 1. LLM服务的Helm Chart开发<br>2. Helm的多环境values配置<br>3. Helm的Chart仓库管理与安全 |
| Kustomize | 1. Kustomize的核心功能（补丁/叠加）？<br>2. Kustomize与Helm的区别？<br>3. Kustomize的配置复用？ | 1. LLM平台的多环境Kustomize配置<br>2. Kustomize的补丁定制（GPU资源）<br>3. Kustomize与GitOps的集成 |
| Terraform | 1. Terraform的核心概念（资源/状态/模块）？<br>2. Terraform的状态管理（remote state）？<br>3. 如何编写可复用的Terraform模块？ | 1. GPU集群的Terraform自动化部署<br>2. 多云厂商GPU资源的Terraform管理<br>3. Terraform的计划与应用审计 |
| Ansible | 1. Ansible的Playbook语法？<br>2. Ansible的模块开发？<br>3. Ansible的批量执行优化？ | 1. GPU节点的Ansible自动化配置<br>2. Ansible的K8s集群初始化<br>3. Ansible的并行执行与错误处理 |

#### 5️⃣ Observability / SRE体系
所有岗位强调稳定性，需能设计端到端的可观测性体系。

##### 三大信号
| 信号类型 | 面试高频问题 | 工业界落地场景 |
|----------|--------------|----------------|
| metrics | 1. 核心metrics类型（Counter/Gauge/Histogram）？<br>2. Prometheus的指标采集原理？<br>3. 如何设计LLM平台的核心指标？ | 1. LLM推理服务的核心指标（延迟/吞吐/显存）<br>2. GPU集群的Prometheus指标采集<br>3. 指标的聚合与降采样策略 |
| logs | 1. 日志采集的核心方案（Fluentd/Logstash）？<br>2. 日志的结构化与索引优化？<br>3. 如何处理大规模日志？ | 1. LLM训练/推理日志的集中采集<br>2. 日志的结构化解析（JSON格式）<br>3. 日志的存储分层（热/冷数据） |
| tracing | 1. 分布式追踪的核心原理（Trace/Span）？<br>2. OpenTelemetry的接入方案？<br>3. 如何分析LLM服务的追踪数据？ | 1. LLM推理服务的分布式追踪（GRPC/HTTP）<br>2. 跨集群追踪数据的采集与关联<br>3. 追踪数据的性能瓶颈定位 |

##### 体系设计
| 核心知识点 | 面试高频问题 | 工业界落地场景 |
|------------|--------------|----------------|
| SLI / SLO / SLA | 1. SLI/SLO/SLA的定义与关系？<br>2. 如何设计LLM服务的SLO？<br>3. SLO达标率的计算与监控？ | 1. LLM推理服务的SLO设计（可用性99.99%）<br>2. SLO告警的分级与响应流程<br>3. SLO未达标的根因分析（RCA） |
| alerting | 1. 告警分级（P0/P1/P2）的设计？<br>2. Prometheus Alertmanager的配置？<br>3. 如何避免告警风暴？ | 1. GPU集群的告警分级与响应流程<br>2. LLM服务的告警抑制与聚合<br>3. 告警的自动升级与闭环 |
| capacity planning | 1. 容量规划的核心指标与方法？<br>2. 如何预测GPU集群的容量需求？<br>3. 容量不足的预警与扩容策略？ | 1. LLM推理服务的GPU容量规划<br>2. 基于历史数据的容量预测模型<br>3. 自动扩容的阈值与策略设计 |
| incident response | 1. 故障响应的核心流程（发现/定位/恢复）？<br>2. 故障分级（P0/P1/P2）的标准？<br>3. 故障响应的复盘机制？ | 1. LLM平台的故障响应手册（Runbook）<br>2. 故障响应的自动化工具（PagerDuty）<br>3. 故障的跨团队协作流程 |
| RCA | 1. 根因分析的核心方法（5Why/鱼骨图）？<br>2. 如何编写高质量的RCA报告？<br>3. RCA的落地与改进措施？ | 1. LLM服务故障的RCA分析<br>2. RCA报告的模板与评审流程<br>3. 改进措施的跟踪与落地验证 |

##### 常用组件
| 组件 | 面试高频问题 | 工业界落地场景 |
|------|--------------|----------------|
| Prometheus | 1. Prometheus的架构（采集/存储/查询）？<br>2. PromQL的高级查询语法？<br>3. Prometheus的远程存储配置？ | 1. GPU集群的Prometheus高可用部署<br>2. LLM指标的PromQL查询与可视化<br>3. Prometheus的采集频率调优 |
| Grafana | 1. Grafana的面板设计原则？<br>2. Grafana的告警配置？<br>3. Grafana的多数据源集成？ | 1. LLM平台的全景监控大屏<br>2. GPU资源的Grafana告警面板<br>3. Grafana的用户权限管理 |
| ELK | 1. ELK的架构（Elasticsearch/Logstash/Kibana）？<br>2. Elasticsearch的分片与副本调优？<br>3. Kibana的日志分析与可视化？ | 1. LLM日志的ELK集中存储与分析<br>2. Elasticsearch的索引生命周期管理<br>3. Kibana的日志告警与仪表盘 |
| OpenTelemetry | 1. OpenTelemetry的核心组件（Collector/SDK）？<br>2. 如何接入LLM服务的追踪数据？<br>3. OpenTelemetry与Prometheus的集成？ | 1. LLM推理服务的全链路追踪<br>2. OpenTelemetry Collector的高可用部署<br>3. 追踪数据的导出与存储优化 |
| Alertmanager | 1. Alertmanager的路由与分组配置？<br>2. 告警的抑制与静默规则？<br>3. Alertmanager的高可用部署？ | 1. GPU集群告警的分组与路由<br>2. 非工作时间的告警静默配置<br>3. Alertmanager的告警集成（钉钉/邮件） |

#### 6️⃣ 编程能力（平台开发级别）
需具备云原生工具/组件的开发能力，而非仅脚本编写。

| 编程语言 | 面试高频问题 | 工业界落地场景 |
|----------|--------------|----------------|
| Go（云原生首选） | 1. Go的协程/通道/内存模型？<br>2. 如何用Go开发K8s Operator？<br>3. Go的性能调优（pprof）？ | 1. 自定义K8s调度器插件开发<br>2. LLM推理服务的Go SDK开发<br>3. Go程序的内存泄漏排查与优化 |
| Python（自动化） | 1. Python的协程（asyncio）使用？<br>2. 如何编写高性能Python脚本？<br>3. Python的依赖管理（Poetry/Pipenv）？ | 1. GPU集群的自动化运维脚本<br>2. LLM训练任务的调度脚本<br>3. Python的性能优化（C扩展/Numba） |
| Shell（运维） | 1. Shell的条件判断/循环/函数？<br>2. 如何编写健壮的Shell脚本？<br>3. Shell脚本的错误处理？ | 1. GPU节点的初始化Shell脚本<br>2. 日常运维的Shell自动化工具<br>3. Shell脚本的日志与错误捕获 |

##### 高级岗位要求
| 核心能力 | 面试高频问题 | 工业界落地场景 |
|----------|--------------|----------------|
| 控制器开发 | 1. Controller的Reconciliation Loop实现？<br>2. Kubebuilder的使用流程？<br>3. Controller的测试方法？ | 1. GPU资源管理Controller开发<br>2. LLM推理服务自动扩缩容Controller<br>3. Controller的单元测试与集成测试 |
| 调度器插件 | 1. Scheduler Framework的扩展点开发？<br>2. 调度器插件的编译与部署？<br>3. 调度器插件的性能测试？ | 1. 基于GPU拓扑的调度器插件<br>2. LLM训练任务的优先级调度插件<br>3. 调度器插件的灰度发布与验证 |
| infra工具开发 | 1. 云原生工具的开发规范？<br>2. 如何设计CLI工具（Cobra）？<br>3. 工具的版本管理与发布？ | 1. LLM平台的CLI工具开发<br>2. GPU集群的诊断工具开发<br>3. 工具的自动化测试与发布流水线 |

### 第二层（AI infra 关键能力）
这是AI infra方向的核心分水岭，面试重点考察实际落地经验。

#### 7️⃣ GPU / HPC 集群基础设施
招聘非常集中，需具备GPU集群的全生命周期管理能力。

| 核心知识点 | 面试高频问题 | 工业界落地场景 |
|------------|--------------|----------------|
| GPU资源管理 | 1. NVIDIA Device Plugin的工作原理？<br>2. 如何实现GPU的精细化调度（显存/算力）？<br>3. vGPU的部署与调优？ | 1. 生产环境GPU资源的动态分配<br>2. 多租户GPU共享的资源隔离<br>3. vGPU在LLM推理中的落地 |
| 多GPU通信 | 1. NCCL的通信原理与调优？<br>2. 多GPU通信的性能瓶颈？<br>3. 如何排查NCCL通信失败？ | 1. LLM训练的NCCL通信优化<br>2. 多机多卡通信的拓扑感知<br>3. NCCL的日志分析与问题定位 |
| 集群拓扑 | 1. GPU集群的网络拓扑（胖树/环形）？<br>2. 如何感知集群拓扑并优化调度？<br>3. 拓扑感知的通信优化？ | 1. LLM训练集群的拓扑规划<br>2. 基于拓扑的GPU调度策略<br>3. 拓扑感知的NCCL通信优化 |
| 分布式训练架构 | 1. 分布式训练的核心模式（数据/模型并行）？<br>2. AllReduce的实现原理？<br>3. 如何适配K8s的分布式训练？ | 1. LLM分布式训练的K8s部署<br>2. AllReduce通信的性能优化<br>3. 分布式训练的故障容错设计 |

##### 关键技术
| 技术 | 面试高频问题 | 工业界落地场景 |
|------|--------------|----------------|
| CUDA | 1. CUDA的核心概念（核函数/线程块）？<br>2. CUDA的内存管理（全局/共享内存）？<br>3. 如何排查CUDA错误？ | 1. LLM推理的CUDA核函数优化<br>2. CUDA内存的复用与优化<br>3. CUDA版本兼容与驱动管理 |
| NCCL | 1. NCCL的集合通信操作（AllGather/AllReduce）？<br>2. NCCL的环境变量调优？<br>3. NCCL与RDMA的集成？ | 1. LLM训练的NCCL性能调优<br>2. NCCL的多流并行优化<br>3. NCCL的故障检测与恢复 |
| RDMA | 1. RDMA的核心原理（零拷贝/内核旁路）？<br>2. RDMA的部署与配置？<br>3. RDMA的性能测试方法？ | 1. GPU集群的RDMA网络部署<br>2. LLM训练的RDMA通信优化<br>3. RDMA的故障排查与调优 |
| InfiniBand | 1. InfiniBand的架构与协议？<br>2. InfiniBand与RDMA的关系？<br>3. InfiniBand的性能调优？ | 1. 超大规模GPU集群的InfiniBand部署<br>2. InfiniBand的分区与隔离<br>3. InfiniBand的监控与告警 |
| RoCE | 1. RoCE的核心原理（RDMA over Ethernet）？<br>2. RoCE v1/v2的区别？<br>3. RoCE的部署注意事项？ | 1. GPU集群的RoCE网络部署<br>2. RoCE的丢包检测与处理<br>3. RoCE与传统以太网的兼容 |
| parallel filesystem | 1. 并行文件系统（Lustre/BeeGFS）的原理？<br>2. 并行文件系统的性能调优？<br>3. 如何适配LLM训练数据？ | 1. LLM训练数据的并行文件系统部署<br>2. 文件系统的IO调度优化<br>3. 数据缓存策略与性能提升 |

#### 8️⃣ AI训练与推理架构（infra视角）
不是算法工程，而是从系统角度优化训练/推理流程。

##### 训练并行策略
| 策略类型 | 面试高频问题 | 工业界落地场景 |
|----------|--------------|----------------|
| data parallel | 1. 数据并行的核心原理？<br>2. 数据并行的通信开销？<br>3. 如何优化数据并行的性能？ | 1. LLM大规模数据并行训练的调度<br>2. 数据并行的梯度同步优化<br>3. 数据并行的故障容错设计 |
| tensor parallel | 1. 张量并行的核心原理？<br>2. 张量并行的切分策略？<br>3. 张量并行的性能瓶颈？ | 1. 千亿参数LLM的张量并行训练<br>2. 张量并行的通信优化（NCCL）<br>3. 张量并行的显存管理 |
| pipeline parallel | 1. 流水线并行的核心原理？<br>2. 流水线并行的气泡问题？<br>3. 如何优化流水线并行？ | 1. 万亿参数LLM的流水线并行训练<br>2. 流水线并行的气泡消除<br>3. 流水线并行的负载均衡 |
| expert parallel (MoE) | 1. MoE的核心原理？<br>2. 专家并行的调度策略？<br>3. MoE的显存优化？ | 1. MoE模型的分布式训练部署<br>2. 专家并行的负载均衡优化<br>3. MoE模型的推理性能调优 |

##### 推理优化
| 核心知识点 | 面试高频问题 | 工业界落地场景 |
|------------|--------------|----------------|
| batching | 1. 推理批处理的核心策略（静态/动态）？<br>2. 批大小的调优方法？<br>3. 批处理的延迟/吞吐权衡？ | 1. LLM推理的动态批处理优化<br>2. 批大小的自适应调整<br>3. 批处理的队列管理与调度 |
| memory管理 | 1. 推理显存的优化策略（显存复用）？<br>2. 如何避免显存碎片？<br>3. 显存溢出的处理策略？ | 1. LLM推理的显存碎片整理<br>2. 显存复用的算法优化<br>3. 显存溢出的自动降级策略 |
| latency优化 | 1. 推理延迟的核心瓶颈？<br>2. 如何优化LLM推理的首包延迟？<br>3. 延迟与吞吐的平衡策略？ | 1. LLM推理的低延迟优化（TensorRT-LLM）<br>2. 首包延迟的优化（前缀缓存）<br>3. 延迟敏感型推理服务的调度 |

#### 9️⃣ 推理引擎与缓存机制
JD中明确出现，是LLM推理优化的核心。

##### KVCache（重点）
| 核心知识点 | 面试高频问题 | 工业界落地场景 |
|------------|--------------|----------------|
| 本质 | 1. KVCache的核心原理？<br>2. KVCache在Transformer中的作用？<br>3. KVCache的显存占用计算？ | 1. LLM推理的KVCache设计<br>2. KVCache的显存占用优化<br>3. KVCache的命中策略设计 |
| 作用 | 1. KVCache如何降低计算量？<br>2. KVCache的吞吐提升效果？<br>3. KVCache的延迟优化原理？ | 1. 大模型推理的KVCache调优<br>2. KVCache的吞吐/延迟权衡<br>3. KVCache的性能基准测试 |
| cache memory layout | 1. KVCache的内存布局优化？<br>2. 行优先/列优先布局的区别？<br>3. 如何适配GPU显存布局？ | 1. LLM推理的KVCache布局优化<br>2. 显存对齐的KVCache设计<br>3. 多GPU KVCache的布局协同 |
| eviction策略 | 1. 常见的缓存淘汰策略（LRU/LFU）？<br>2. 如何设计KVCache的淘汰策略？<br>3. 淘汰策略的性能影响？ | 1. LLM推理的KVCache LRU优化<br>2. 基于访问频率的淘汰策略<br>3. 淘汰策略的自适应调整 |
| GPU显存管理 | 1. KVCache的显存分配策略？<br>2. 如何避免KVCache的显存碎片？<br>3. 显存不足时的KVCache策略？ | 1. KVCache的显存池化管理<br>2. 显存碎片的自动整理<br>3. 显存不足时的KVCache降级 |
| prefix sharing | 1. Prefix Sharing的核心原理？<br>2. 如何实现Prefix Sharing？<br>3. Prefix Sharing的性能提升？ | 1. 批量推理的Prefix Sharing优化<br>2. Prefix Sharing的显存节省计算<br>3. Prefix Sharing的兼容性适配 |
| paged KVCache | 1. 分页KVCache的核心原理？<br>2. 分页大小的调优？<br>3. 分页KVCache的性能影响？ | 1. vLLM的分页KVCache落地<br>2. 分页大小的自适应调整<br>3. 分页KVCache的缺页处理 |

##### 典型场景
| 场景/工具 | 面试高频问题 | 工业界落地场景 |
|-----------|--------------|----------------|
| vLLM | 1. vLLM的核心架构（PagedAttention）？<br>2. vLLM的部署与调优？<br>3. vLLM的性能瓶颈？ | 1. 生产环境vLLM的高可用部署<br>2. vLLM的批处理优化<br>3. vLLM与K8s的集成调度 |
| TensorRT-LLM | 1. TensorRT-LLM的优化原理？<br>2. 如何编译LLM模型到TensorRT-LLM？<br>3. TensorRT-LLM的性能调优？ | 1. LLM推理的TensorRT-LLM加速<br>2. TensorRT-LLM的量化优化<br>3. TensorRT-LLM的部署自动化 |
| SGLang | 1. SGLang的核心特性？<br>2. SGLang与vLLM的区别？<br>3. SGLang的适用场景？ | 1. 交互式LLM推理的SGLang落地<br>2. SGLang的并发控制优化<br>3. SGLang的资源占用调优 |

#### 🔟 向量数据库 / RAG基础设施
频繁出现，需能部署/优化向量数据库支撑RAG场景。

| 技术/工具 | 面试高频问题 | 工业界落地场景 |
|-----------|--------------|----------------|
| Milvus | 1. Milvus的核心架构（数据节点/索引节点）？<br>2. Milvus的索引类型（IVF_FLAT/HNSW）？<br>3. Milvus的性能调优？ | 1. RAG系统的Milvus高可用部署<br>2. Milvus的索引优化（查询性能）<br>3. Milvus的分片与扩容策略 |
| Elasticsearch | 1. Elasticsearch的向量搜索实现？<br>2. ES的索引调优（分片/副本）？<br>3. ES的向量查询性能优化？ | 1. RAG系统的ES向量搜索落地<br>2. ES的向量索引优化<br>3. ES的查询缓存策略 |
| pgvector | 1. pgvector的核心原理？<br>2. pgvector的索引类型（IVFFlat/HNSW）？<br>3. pgvector的性能调优？ | 1. 轻量级RAG系统的pgvector部署<br>2. pgvector的查询优化（索引选择）<br>3. pgvector的事务与一致性保障 |

##### infra职责
| 核心职责 | 面试高频问题 | 工业界落地场景 |
|----------|--------------|----------------|
| 部署 | 1. 向量数据库的高可用部署策略？<br>2. 如何适配GPU加速向量计算？<br>3. 向量数据库的多环境部署？ | 1. 生产级向量数据库的集群部署<br>2. GPU加速的向量数据库部署<br>3. 向量数据库的灾备部署 |
| 扩展 | 1. 向量数据库的水平扩展策略？<br>2. 分片策略的设计？<br>3. 扩展过程中的可用性保障？ | 1. 向量数据库的动态扩缩容<br>2. 基于数据量的分片调整<br>3. 扩展过程中的查询无感知 |
| 查询性能调优 | 1. 向量查询的性能瓶颈？<br>2. 索引类型的选择依据？<br>3. 如何优化向量查询延迟？ | 1. RAG系统的向量查询性能调优<br>2. 索引的动态调整（离线/在线）<br>3. 查询缓存的优化策略 |

### 第三层（高级 infra specialization）
用于进入顶级AI infra团队，面试重点考察深度定制与优化能力。

#### 11️⃣ Kubernetes深度扩展
| 核心知识点 | 面试高频问题 | 工业界落地场景 |
|------------|--------------|----------------|
| scheduler framework | 1. Scheduler Framework的核心扩展点？<br>2. 如何开发自定义调度器？<br>3. 调度器的性能调优？ | 1. LLM训练任务的定制调度器<br>2. 调度器框架的插件化开发<br>3. 大规模调度器的性能优化 |
| custom resource orchestration | 1. 自定义资源的编排策略？<br>2. 如何实现CRD的状态管理？<br>3. CRD的版本控制？ | 1. LLM推理服务的CRD编排<br>2. 自定义资源的生命周期管理<br>3. CRD的升级与兼容策略 |
| batch scheduler (Volcano / Kueue) | 1. Volcano的核心调度策略？<br>2. Kueue的资源管理原理？<br>3. 如何适配LLM批量训练任务？ | 1. LLM批量训练任务的Volcano调度<br>2. Kueue的资源配额管理<br>3. 批量调度的优先级与抢占 |
| multi-tenant GPU scheduling | 1. 多租户GPU调度的隔离策略？<br>2. 如何实现GPU的按比例共享？<br>3. 多租户的GPU计费？ | 1. 多租户LLM平台的GPU调度<br>2. GPU资源的租户隔离<br>3. 多租户GPU使用的计量与计费 |

#### 12️⃣ 虚拟化与容器融合
| 技术/工具 | 面试高频问题 | 工业界落地场景 |
|-----------|--------------|----------------|
| KVM | 1. KVM的虚拟化原理？<br>2. KVM的性能调优？<br>3. KVM与GPU的直通？ | 1. GPU直通的KVM虚拟机部署<br>2. KVM的性能调优（CPU/内存）<br>3. KVM虚拟机的快速部署 |
| QEMU | 1. QEMU的虚拟化实现？<br>2. QEMU的GPU直通配置？<br>3. QEMU的性能优化？ | 1. QEMU的GPU直通适配LLM推理<br>2. QEMU的IO性能调优<br>3. QEMU的快照与恢复 |
| KubeVirt | 1. KubeVirt的核心架构？<br>2. KubeVirt与K8s的集成？<br>3. KubeVirt的GPU虚拟化？ | 1. K8s集群的KubeVirt部署<br>2. VM+容器的统一调度<br>3. KubeVirt的GPU资源管理 |

##### 目标
统一 VM + container 调度，支撑混合负载的LLM平台。

#### 13️⃣ 高性能网络
| 核心技术 | 面试高频问题 | 工业界落地场景 |
|----------|--------------|----------------|
| SR-IOV | 1. SR-IOV的虚拟化原理？<br>2. SR-IOV的配置与调优？<br>3. SR-IOV与GPU集群的集成？ | 1. GPU集群的SR-IOV部署<br>2. SR-IOV的性能调优<br>3. SR-IOV的多租户隔离 |
| RDMA | 1. RDMA的内核旁路原理？<br>2. RDMA的连接管理？<br>3. RDMA的故障排查？ | 1. LLM训练的RDMA网络优化<br>2. RDMA的连接池管理<br>3. RDMA的性能监控与告警 |
| eBPF | 1. eBPF的网络编程？<br>2. eBPF的流量控制？<br>3. eBPF的性能开销？ | 1. 基于eBPF的GPU集群网络监控<br>2. eBPF实现LLM服务的流量限流<br>3. eBPF的网络故障定位 |
| DPDK | 1. DPDK的核心原理？<br>2. DPDK的性能调优？<br>3. DPDK与LLM服务的集成？ | 1. 高性能LLM推理服务的DPDK加速<br>2. DPDK的多核优化<br>3. DPDK的内存管理 |
| VXLAN | 1. VXLAN的封装原理？<br>2. VXLAN的性能调优？<br>3. VXLAN的多租户隔离？ | 1. GPU集群的VXLAN网络部署<br>2. VXLAN的封装开销优化<br>3. 多租户LLM平台的VXLAN隔离 |

#### 14️⃣ 分布式存储
| 技术/工具 | 面试高频问题 | 工业界落地场景 |
|-----------|--------------|----------------|
| Ceph | 1. Ceph的核心架构（MON/OSD/MDS）？<br>2. Ceph的性能调优？<br>3. Ceph与GPU的集成？ | 1. LLM训练数据的Ceph存储<br>2. Ceph的IO性能调优<br>3. Ceph的纠删码配置 |
| Lustre | 1. Lustre的并行文件系统原理？<br>2. Lustre的性能调优？<br>3. Lustre的部署与维护？ | 1. 超大规模LLM训练的Lustre存储<br>2. Lustre的客户端调优<br>3. Lustre的故障恢复 |
| BeeGFS | 1. BeeGFS的核心架构？<br>2. BeeGFS的性能调优？<br>3. BeeGFS的扩展性？ | 1. 中小规模LLM训练的BeeGFS部署<br>2. BeeGFS的缓存策略优化<br>3. BeeGFS的动态扩容 |
| Weka | 1. Weka的核心特性？<br>2. Weka的性能调优？<br>3. Weka与GPU的集成？ | 1. 高性能LLM推理的Weka存储<br>2. Weka的GPU direct storage配置<br>3. Weka的多租户隔离 |

##### 优化重点
| 核心优化方向 | 面试高频问题 | 工业界落地场景 |
|--------------|--------------|----------------|
| IO吞吐 | 1. 如何提升分布式存储的IO吞吐？<br>2. 并行IO的优化策略？<br>3. 存储带宽的测试方法？ | 1. LLM训练数据的IO吞吐优化<br>2. 并行文件系统的IO调度<br>3. 存储吞吐的监控与告警 |
| metadata性能 | 1. 元数据性能的瓶颈点？<br>2. 元数据缓存策略？<br>3. 元数据服务器的扩展？ | 1. LLM训练的元数据性能优化<br>2. 元数据缓存的命中率提升<br>3. 元数据服务器的高可用部署 |
| GPU direct storage | 1. GPU direct storage的原理？<br>2. 如何配置GPU direct storage？<br>3. 性能提升效果？ | 1. LLM推理的GPU direct storage部署<br>2. 存储与GPU的直接数据传输<br>3. GPU direct storage的性能测试 |

#### 15️⃣ FinOps / Resource efficiency
企业极度重视，需能平衡性能与成本。

| 核心知识点 | 面试高频问题 | 工业界落地场景 |
|------------|--------------|----------------|
| GPU利用率 | 1. 如何提升GPU利用率？<br>2. GPU利用率的监控指标？<br>3. 利用率与性能的平衡？ | 1. LLM推理服务的GPU利用率优化<br>2. GPU利用率的实时监控<br>3. 低利用率任务的自动调度 |
| 成本优化 | 1. GPU集群的成本优化策略？<br>2. 按需计费vs预留实例？<br>3. 闲置资源的释放策略？ | 1. LLM平台的GPU成本优化<br>2. 非工作时间的资源自动释放<br>3. 资源的按需扩缩容 |
| capacity modeling | 1. 容量建模的核心方法？<br>2. 如何预测GPU容量需求？<br>3. 容量模型的验证方法？ | 1. LLM平台的GPU容量建模<br>2. 基于业务增长的容量预测<br>3. 容量模型的动态调整 |

## 三、学习优先级路线图（面试+工业界落地导向）
### Phase 1 基础设施底座（必须，面试必考）
1. Linux internals：重点掌握内核级内存/进程/网络/cgroup，能回答底层原理+生产问题排查
2. 网络基础 TCP/IP：重点掌握TCP拥塞控制、RDMA原理，能设计GPU集群网络架构
3. container runtime：重点掌握containerd/runc原理，能解决容器启动/隔离问题
4. Kubernetes cluster运维：重点掌握集群部署/故障排查/核心组件调优，有生产集群运维经验

### Phase 2 平台工程能力（面试高频，工业界必备）
5. CI/CD：重点掌握GitOps落地、流水线设计，能搭建端到端的LLM平台自动化流水线
6. Observability：重点掌握Prometheus/Grafana/OpenTelemetry，能设计LLM平台可观测性体系
7. IaC：重点掌握Terraform/Ansible/Helm，能自动化部署GPU集群
8. automation scripting：重点掌握Python/Shell/Go，能编写运维自动化工具

### Phase 3 云原生深水区（面试加分，高级岗位必备）
9. Kubernetes internal architecture：重点掌握源码级理解，能开发Operator/调度器插件
10. Operator开发：重点掌握kubebuilder，能定制GPU资源管理Controller
11. scheduler机制：重点掌握调度器框架，能开发LLM任务定制调度器

### Phase 4 AI集群基础设施（AI infra核心，面试核心区分点）
12. GPU架构：重点掌握CUDA/NCCL/RDMA，能调优GPU集群通信性能
13. distributed training topology：重点掌握并行策略，能设计LLM分布式训练架构
14. HPC network：重点掌握InfiniBand/RoCE，能部署高性能GPU集群网络
15. distributed storage：重点掌握Lustre/Ceph，能优化LLM训练数据存储

### Phase 5 LLM infra specialization（顶级岗位门槛，面试压轴）
16. inference engine：重点掌握vLLM/TensorRT-LLM，能优化LLM推理性能
17. KVCache优化：重点掌握分页KVCache/Prefix Sharing，能设计低延迟推理缓存
18. memory scheduling：重点掌握显存管理/碎片整理，能提升GPU显存利用率
19. serving architecture：重点掌握推理服务架构，能设计高可用LLM推理平台

### Phase 6 顶级平台工程（大厂核心要求，面试深度考察）
20. cluster scheduling algorithms：重点掌握调度算法优化，能设计大规模GPU调度系统
21. performance modeling：重点掌握性能基线/瓶颈分析，能建立LLM平台性能模型
22. reliability engineering：重点掌握SLO/RCA/故障容错，能保障99.99%可用性
23. cost optimization：重点掌握FinOps，能平衡性能与GPU成本

## 四、精简版能力模型（面试导向）
如果压缩成一句话：
```
Linux system engineer
+ Kubernetes platform engineer
+ distributed systems engineer
+ GPU cluster engineer
+ LLM inference infrastructure engineer
```

### 面试核心标签（简历/自我介绍重点）
1. 超大规模K8s集群运维（万节点/GPU集群）
2. GPU集群网络/存储优化（RDMA/并行文件系统）
3. LLM推理性能优化（vLLM/KVCache/TensorRT-LLM）
4. 云原生平台开发（Operator/调度器插件）
5. SRE体系搭建（可观测性/SLO/故障容错）

## 五、面试&工业界核心学习建议（最关键）
### 优先学习顺序（反常识但符合招聘/落地逻辑）
1. Kubernetes内部原理：先懂K8s调度/控制器/网络，再做AI infra定制
2. Linux内核与网络：内核级理解是排查所有生产问题的基础
3. cluster调度机制：调度是GPU集群资源利用率的核心
4. GPU通信架构：NCCL/RDMA是LLM训练性能的关键
5. LLM推理引擎：推理是AI infra落地最广泛的场景
6. KVCache与memory优化：推理性能优化的核心抓手

### 面试准备核心方法
1. 项目经验包装：每个核心技术点对应1个生产级项目案例（STAR法则）
2. 原理+落地结合：不仅懂原理，还要讲清在工业界的落地方式/坑/优化点
3. 技术广度+深度：广度覆盖全栈，深度在AI infra（GPU/LLM推理）有亮点
4. 模拟故障排查：准备5-10个真实故障案例（如GPU通信失败/推理延迟高）

### 工业界落地核心建议
1. 先标准化再优化：基于开源组件（K8s/vLLM/ArgoCD）搭建基础平台，再定制优化
2. 性能与成本平衡：GPU利用率提升1%可能带来百万级成本节省
3. 自动化优先：所有运维/部署操作自动化，减少人工介入
4. 可观测性先行：平台搭建初期就完善监控/日志/追踪，避免后期返工

## 六、行业真实技术栈（面试高频组合，工业界标配）
典型生产环境：
```
Kubernetes
+
GPU cluster (NVIDIA A100/H100)
+
RDMA network (InfiniBand/RoCE)
+
Ceph/Lustre storage
+
Prometheus/Grafana/OpenTelemetry observability
+
ArgoCD GitOps
+
vLLM/TensorRT-LLM inference
+
Milvus/pgvector vector DB
```

### 面试高频技术栈追问
1. 你在生产环境中如何组合这些技术栈？核心挑战是什么？
2. 如何基于这套技术栈保障LLM推理服务的高可用？
3. 这套技术栈的成本优化点有哪些？

## 七、JD本质技术方向分类（面试定位参考）
1. Cloud Native Platform Engineering：面试重点问K8s/容器/CI/CD
2. AI Compute Infrastructure：面试重点问GPU/HPC/分布式训练
3. Distributed System Scheduling：面试重点问调度器/资源管理
4. Performance Engineering：面试重点问LLM推理优化/KVCache/显存
5. Reliability Engineering：面试重点问SRE/可观测性/故障容错

## 八、顶级AI infra团队门槛（面试终极考察点）
### 必须具备的核心能力（面试深度追问）
1. Kubernetes源码级理解：能讲清scheduler/controller的核心代码逻辑
2. GPU集群调优经验：有万卡级GPU集群调优案例，能量化性能提升
3. 分布式训练架构理解：能设计万亿参数LLM的分布式训练架构
4. 推理性能优化经验：能讲清vLLM/TensorRT-LLM的底层优化，量化延迟/吞吐提升
5. 大规模生产系统运维经验：有保障99.99%以上可用性的案例

### 面试终极问题（顶级团队必问）
1. 如何设计一个支撑万卡级GPU、千亿参数LLM训练/推理的云原生平台？
2. 你会如何优化LLM推理的成本（GPU利用率），同时保障延迟SLO？
3. 请设计一个故障自动恢复的LLM训练平台，覆盖节点/网络/存储故障。
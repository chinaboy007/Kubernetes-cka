## 目录
- [第一题: RBAC鉴权](#第一题: RBAC鉴权)
- [第二题: 节点设置不可用](#第二题: 节点设置不可用)
- [第三题: 升级K8s版本](#第三题: 升级K8s版本)
- [第四题: etcd备份与恢复](#第四题: etcd备份与恢复)
- [第五题: 网络策略](#第五题: 网络策略)
- [第六题: SVC暴露应用](#第六题: SVC暴露应用)
- [第七题: Ingress](#第七题: Ingress)
- [第八题: 扩容Pod数量](#第八题: 扩容Pod数量)
- [第九题: nodeSelector](#第九题: nodeSelector)
- [第七题: Ingress](#第七题: Ingress)
- [第十题: 统计准备就绪节点数量](#第十题: 统计准备就绪节点数量)
- [第十一题: Pod配置多容器](#第十一题: Pod配置多容器)
- [第十二题: 创建PV](#第十二题: 创建PV)
- [第十三题: Pod使用PVC](#第十三题: Pod使用PVC)
- [第十四题: 获取Pod错误日志](#第十四题: 获取Pod错误日志)
- [第十五题: 给Pod增加一个容器(边车)](#第十五题: 给Pod增加一个容器(边车))
- [第十六题: 统计使用CPU最高的Pod](#第十六题: 统计使用CPU最高的Pod)
- [第十七题: 节点NotReady处理](#第十七题: 节点NotReady处理)

## 背景
这是一个基于Kubernetes v1.20.0集群来进行CKA认证(Certified Kubernetes Administrator),相关题目练习的集群。

## 第一题: RBAC鉴权
**题目要求:**  
创建clusterrole，只允许创建deployment,daemonset,statefulset资源  
在现有的namespace app-team1中创建一个名为cicd-token的新ServiceAccount  
限于namespace app-team1，将新的ClusterRole deployment-clusterrole绑定到新的ServiceAccount cidi-token  

## 第二题: 节点设置不可用
**题目要求:**  
将名为ek8s-node-1的node设置为不可用，并重新调度该node上所有运行的pods  

## 第三题: 升级K8s版本
**题目要求:**  
现有的Kubernetes集群正在运行版本为1.20.0，仅将主节点上的所有Kubernetes控制平面和节点组件升级到版本为1.20.1  
确保在升级之前drain主节点，并在升级后uncordon主节点  

## 第四题: etcd备份与恢复
**题目要求:**  
首先，为运行在https://127.0.0.1:2379 上的现有etcd实例创建快照并将快照保存到 /data/backup/etcd-snapshot.db  
然后还原位于 /data/backup/etcd-snapshot-previous.db的现有先前快照(提供了TLS证书和密钥路径，连接etcd服务器)  

## 第五题: 网络策略
**题目要求:**  
在现有的namespace my-app中创建一个名为allow-port-from-namespace的新NetworkPolicy  
确保新的NetworkPolicy允许namespace my-app中的Pods来连接到namespace big-corp中的端口8080  
进一步确保新的NetworkPolicy  
  不允许对没有在监听端口8080的Pods的访问  
  不允许不来自namespace my-app中的Pods的访问  

## 第六题: SVC暴露应用
**题目要求:**  
请重新配置现有的部署front-end以及添加名为http的端口规范来公开现有容器nginx的端口80/tcp  
创建一个名为front-end-svc的新服务，以公开容器端口http  
配置此服务，以通过在排定的节点上的NodePort来公开各个Pods  

## 第七题: Ingress
**题目要求:**  
如下创建一个新的nginx Ingress资源：  
名称：pong  
Namespace：ing-internal  
使用服务端口5678在路径/hello上公开服务hello  

## 第八题: 扩容Pod数量
**题目要求:**  
将deployment从loadbalancer扩展至5pods  

## 第九题: nodeSelector
**题目要求:**  
按如下要求调度一个Pod  
名称：nginx-kusc00401  
image: nginx  
Node selector: disk=ssd  

## 第十题: 统计准备就绪节点数量
**题目要求:**  
检查有多少worker nodes已准备就绪(不包括被打上Taint: NoSchedule的节点)，并将数量写入/opt/KUSC00402/kusc00402.txt  

## 第十一题: Pod配置多容器
**题目要求:**  
创建一个名为kucc4的pod，在pod里面分别为以下每个images单独运行一个app container(可能会有1-4个images):nginx+redis+memcached  

## 第十二题: 创建PV
**题目要求:**  
创建名为app-data的persistent volume，容量为2Gi，访问模式为ReadWriteOnce。volume类型为hostPath，位于/srv/app-data  

## 第十三题: Pod使用PVC
**题目要求:**  
创建一个新的PersistentVolumeClaim  
名称：pv-volume  
Class：csi-hostpath-sc  
容量：10Mi  
  
创建一个新的Pod，此Pod将作为volume挂载到PersistenVolumeClaim  
名称：web-server  
image：nginx  
挂载路径：/usr/share/nginx/html  
配置新的Pod，以对volume具有ReadWriteOnce权限  
最后，使用kubectl edit或者kubectl patch将PersistenVolumeClaim的容量扩展为70Mi，并记录此更改  

## 第十四题: 获取Pod错误日志
**题目要求:**  
监控pod bar的日志并：提取与错误file-not-found相对应的日志行。将这些日志行写入/opt/KUTR00101/bar  

## 第十五题: 给Pod增加一个容器(边车)
**题目要求:**  
使用busybox Image来将名为sidecar的sidecar容器添加到现有的Pod legacy-app中。新的sidecar容器必须运行以下命令:  
/bin/sh -c tail -n+1 -f /var/log/legacy-app.log  
使用安装在/var/log的Volume，使日志文件legacy-app.log可用于sidecar容器  

## 第十六题: 统计使用CPU最高的Pod
**题目要求:**  
通过pod label name=cpu-utilizer，找到运行占用大量CPU的pod，并将占用CPU最高的pod名称写入文件/opt/KUTR00401/KUTR00401.txt（已存在）  

## 第十七题: 节点NotReady处理
**题目要求:**  
名为wk8s-node-0的Kubernetes worker node处于NotReady状态。调查发生这种情况的原有，并采取相应措施将node恢复为Ready状态，确保所做的任何更改永久有效  


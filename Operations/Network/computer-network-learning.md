## 一、计算机网络概述
### 分类

- 按交换技术：电路交换、报文交换、分组交换
- 按使用者：共用网、专用网
- 按传输介质：有线网路、无线网络
- 按覆盖范围：广域网WAN、城域网MAN、局域网LAN、个域网PAN
- 按拓扑结构：总线型、星型、环型、网状型

### 性能指标

- 速率：数据量单位（bit）

比特单位计算：8bit=1B KB=210B MB=210x210B ...<br />速率计算：b/s=bps/s Kbps=103bps/s Mbps=103x103bps/s ...

- 带宽：通信线路传输数据能力，单位时间内从某一点到另一点能通过"最高速率"

单位和计算方式 与速率相同

- 吞吐量：单位时间内通过某个网络（信道、接口）的数据量，实际通过网络的数据量，受网络带宽和额定速率影响（小于等于速率）
- 时延：发送时延、传播时延、处理时延 （地理位置相同时，数据较大时发送时延占主导）

发送时延计算：分组长度（b）/ 发送速率（b/s） 发送速率取网卡、信道带宽、接口速率中最小值<br />传播时延计算：信道长度（m）/ 电磁传播速率（m/s） 自由空间：3x108m/s 铜线：2.3x108  光纤：2x108<br />处理时延：包含排队时延（路由器存储转发，计算复杂）

- 时延带宽积：传播时延 x 带宽<br />![image.png](https://cdn.nlark.com/yuque/0/2021/png/21806976/1640269818217-c0d19da3-0486-4c08-85ab-c317badc57c9.png#averageHue=%2378746e&clientId=uf5a0bbd2-c6b2-4&from=paste&id=u3c60407f&originHeight=438&originWidth=1158&originalType=url&ratio=1&rotation=0&showTitle=false&size=235576&status=done&style=none&taskId=u865b2fd8-cce5-4261-a7dc-9ce7bff014e&title=)
- 往返时间：单次双向信息交互的时间（RTT）
- 利用率（主干网ISP一般控制信道利用率不超过50%，超过网络时延迅速增大）

信道利用率：表示某信道有百分之机的时间是被利用的（有数据通过）<br />网络利用率：全网络的信道利用率的加权平均

- 丢包率：分组丢失率，指一定时间范围内，丢失的分组数量与总分组数量的比率

丢包原因：传输过程出现误码或分组到达队列已满的交换机、路由器时被丢弃（通信量较大容易造成网络拥塞）

### 计算机网络体系结构
#### 常见的计算机网路体系结构

1. OSI 7层模型（原始学术结构）
> 应用层
> 表示层
> 会话层
> 运输层
> 网络层
> 数据链路层
> 物理层


2. TCP/IP体系结构（商业驱动）
> 应用层（HTTP、SMTP、DNS、RTP）
> 运输层（TCP、UDP）
> 网际层（IP）
> 网络接口层


3. 原理体系结构（教学结构）
> 应用层
> 运输层
> 网络层
> 数据链路层
> 物理层


#### 计算机网络体系结构分层的必要性

- 物理层（使用何种信号来传输比特）
   - 传输介质
   - 物理接口
   - 使用信号表示比特0/1
- 数据链路层（一个网络或一段链路上传输）
   - 如何标识网络中各主机（主机编码问题，如MAC 地址）
   - 如何从信号所表示的一连串比特流区分出地址和数据
   - 如何协调各主机争抢总线
- 网络层（解决分组在多个网路传输路由的问题）
   - 如何标识各网络以及网络中各主机（网络和主机共同编址问题，如IP 地址）
   - 路由器如何转发分组，如何进行路由选择
- 传输层（解决网络之间基于网络通信问题）
   - 如何解决进程之间基于网络的通信问题
   - 出现传输错误如何解决
- 应用层（解决通过应用进程的交互来实现特定网络应用问题）
   - 通过应用进程间交互来完成特定的网络应用

![image.png](https://cdn.nlark.com/yuque/0/2022/png/21806976/1641213491006-c62dae46-a7c3-4d5a-8923-e7b58de44691.png#averageHue=%23797774&clientId=u38881118-55b0-4&from=paste&height=369&id=uc940d291&originHeight=738&originWidth=1608&originalType=binary&ratio=1&rotation=0&showTitle=false&size=318569&status=done&style=none&taskId=u3e584a85-9f13-4399-a7b8-ff51d8b9131&title=&width=804)

#### 专用术语

- 实体：任何可发送或接收信息的硬件或软件进程。对等实体（收发双方想同层次中的实体，如网卡）
- 协议：控制两个对等实体进行逻辑通信的规则集合（HTTP协议、TCP协议、IP协议等）
   - 语法：定义交换信息的格式（如IP 报文头+数据格式）
   - 语义：定义通信双方所要完成的操作（如HTTP GET 请求与HTTP 响应报文）
   - 同步：定义通信双方的时序关系（TCP 三次连接）
- 服务
   - 协议控制下，两个对等实体间的逻辑通信使得本层能够向上一层提供服务
   - 要实现本层协议，还需要使用下一层所提供的服务
   - 协议是"水平的"，服务是"垂直的"
   - 服务访问点：帧、协议字段（IP）、端口号
   - 服务原语：上层使用下层所提供的的服务必须通过与下层交换一些命令
- 协议数据单元PDU（Protocol Data Unit）：对等层次之间传送的数据包
   - 比特流 bit
   - 帧 frame
   - 数据包 packet
   - 数据包 segment（TCP）/datagram（UDP）
   - 数据包：message
- 服务数据单元SDU：同一系统内，层与层之间交换的数据包
- 多个SDU可以合成一个PDU；一个SDU也可划分为几个PDU

时延与传播时长习题计算：<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/21806976/1641219435817-456d4886-af80-4698-aceb-04047afb7f26.png#clientId=u2cb64076-075c-4&from=paste&height=372&id=u9952ea38&originHeight=744&originWidth=1580&originalType=binary&ratio=1&rotation=0&showTitle=false&size=274202&status=done&style=none&taskId=u658ecac7-9fb9-40ab-9ca9-59e0534e361&title=&width=790)<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/21806976/1641220293330-92e1090a-98a4-4844-b12f-f6330644d9c0.png#clientId=u2cb64076-075c-4&from=paste&height=408&id=u47e37806&originHeight=816&originWidth=1566&originalType=binary&ratio=1&rotation=0&showTitle=false&size=603291&status=done&style=none&taskId=u6e8720ec-2835-43ae-8ee0-f8cc618fa9a&title=&width=783)

## 二、TCP/IP 体系
### 物理层
#### 传输媒体

- 导引型
   - 双绞线
   - 同轴电缆
   - 光纤
- 非导引型
   - 无线电波
   - 红外线
   - 微波通信（2~40 GHz）
   - 可见光
#### 物理层协议主要任务

- 机械特性
- 电器特性
- 功能特性
- 过程特性
> 物理层考虑的是怎样才能在各种计算机的传输媒体上传输数据比特流
> 为数据链路层屏蔽各种传输媒体的差异，是数据链路层只需考虑如何完成本层的协议和服务，而不必考虑网络具体传输是什么

#### 传输方式

- 串行传输：计算机网络
- 并行传输：CPU --> 内存 总线并行传输
- 同步传输：收发时钟同步
   - 外同步：收发双方之间添加一条单独的时钟信号线
   - 内同步：发送端将时钟同步信号编码到发送数据中一起传输（如曼彻斯特编码）
- 异步传输
   - 字节之间同步（起始位 结束位）
   - 字节中每个比特仍然同步
- 单工：收音机
- 半双工：对讲机
- 全双工：电话
#### 编码与调制
![image.png](https://cdn.nlark.com/yuque/0/2022/png/21806976/1641307009504-6f60e6ee-7c04-41cb-ab6f-34d9ae956a32.png#clientId=ua36dbe17-630d-4&from=paste&height=378&id=ua17b3703&originHeight=756&originWidth=1582&originalType=binary&ratio=1&rotation=0&showTitle=false&size=394204&status=done&style=none&taskId=u51d298fd-a4a7-4096-b7bb-09308b9a5d0&title=&width=791)

### 数据链路层
![image.png](https://cdn.nlark.com/yuque/0/2022/png/21806976/1641308542563-5c11a905-b485-415f-a7cd-f59bb21b1c63.png#clientId=ua36dbe17-630d-4&from=paste&height=375&id=uafa7fa27&originHeight=750&originWidth=1544&originalType=binary&ratio=1&rotation=0&showTitle=false&size=550311&status=done&style=none&taskId=u98d5f508-f7a0-4c15-87e1-77afce44bca&title=&width=772)
#### 封装成帧
添加帧头与帧尾：MAC帧<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/21806976/1641391120600-39183574-6df0-465f-bc49-7e9f719e4735.png#clientId=ua36dbe17-630d-4&from=paste&height=404&id=uccc235fa&originHeight=808&originWidth=1526&originalType=binary&ratio=1&rotation=0&showTitle=false&size=378759&status=done&style=none&taskId=u5e6762d6-3875-4146-b5ad-f8aa6fe716c&title=&width=763)
#### 差错检测

- 帧尾检错码
- 奇偶校验
- 循环冗余校验CRC

![image.png](https://cdn.nlark.com/yuque/0/2022/png/21806976/1641391772095-6a24282c-776c-4eba-967f-f1af68e8e565.png#clientId=ua36dbe17-630d-4&from=paste&height=353&id=uc7aa5342&originHeight=706&originWidth=1560&originalType=binary&ratio=1&rotation=0&showTitle=false&size=374502&status=done&style=none&taskId=u159beb03-de2d-4910-b541-df2bcd5af54&title=&width=780)
#### 可靠传输
![image.png](https://cdn.nlark.com/yuque/0/2022/png/21806976/1641392737438-42d324f0-5a75-4e12-968b-227ec9462be3.png#clientId=ua36dbe17-630d-4&from=paste&height=336&id=u56bf4bb7&originHeight=672&originWidth=1492&originalType=binary&ratio=1&rotation=0&showTitle=false&size=342005&status=done&style=none&taskId=ud00c406f-706b-4c25-beb5-4d364a95fe3&title=&width=746)

- 停止等待协议SW
- 回退N帧协议GBN
- 选择重传协议SR
#### 点对点协议PPP
![image.png](https://cdn.nlark.com/yuque/0/2022/png/21806976/1641395894713-ba41a06e-3edf-4582-b53b-bb2f23a8dcd2.png#clientId=ua36dbe17-630d-4&from=paste&height=365&id=u2965c5ad&originHeight=730&originWidth=1560&originalType=binary&ratio=1&rotation=0&showTitle=false&size=485758&status=done&style=none&taskId=uae924c32-f592-4938-88e8-7323f682217&title=&width=780)
#### 媒体接入控制
![image.png](https://cdn.nlark.com/yuque/0/2022/png/21806976/1641396631045-1d9d70cd-b175-4f3b-8f6e-08fc2c896c85.png#clientId=ua36dbe17-630d-4&from=paste&height=398&id=u36a42ed3&originHeight=796&originWidth=1546&originalType=binary&ratio=1&rotation=0&showTitle=false&size=721296&status=done&style=none&taskId=u8a1587ae-328a-41a2-9855-df1bf65e642&title=&width=773)<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/21806976/1641817159150-62fce9ca-bbc0-4639-bee1-df5bd9bac6ba.png#clientId=ua614fb9f-b410-4&from=paste&height=362&id=ube47e841&originHeight=724&originWidth=1610&originalType=binary&ratio=1&rotation=0&showTitle=false&size=377077&status=done&style=none&taskId=u98b726e0-d5b2-408d-941c-39a622f6bdc&title=&width=805)
#### 随机接入

- CSMA/CD协议
- CSMA/CA协议

#### MAC地址、IP地址以及ARP协议
![image.png](https://cdn.nlark.com/yuque/0/2022/png/21806976/1641823870029-83b5a2a0-e156-403c-94cc-55ab7fa2330f.png#clientId=ua614fb9f-b410-4&from=paste&height=390&id=uea2024da&originHeight=780&originWidth=1576&originalType=binary&ratio=1&rotation=0&showTitle=false&size=512367&status=done&style=none&taskId=u8b9087e2-d119-4b6d-9eea-deab810f523&title=&width=788)	

#### 集线器与交换机
![image.png](https://cdn.nlark.com/yuque/0/2022/png/21806976/1641824872376-ec4d2a9a-8181-426e-9eb9-e2339317af29.png#clientId=ua614fb9f-b410-4&from=paste&height=327&id=u6202759e&originHeight=654&originWidth=1446&originalType=binary&ratio=1&rotation=0&showTitle=false&size=267735&status=done&style=none&taskId=u7e5e282f-b91d-423e-a8ec-2c4102d4708&title=&width=723)<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/21806976/1641825298081-d348633b-8096-4c61-88ed-ffd7f7bcdbc2.png#clientId=ua614fb9f-b410-4&from=paste&height=300&id=u857445ff&originHeight=600&originWidth=1576&originalType=binary&ratio=1&rotation=0&showTitle=false&size=352636&status=done&style=none&taskId=u8e1fa9ad-3940-4f8b-9b22-3fd42e9aed8&title=&width=788)<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/21806976/1641826379357-e44b3048-6850-4bac-b3e3-f8de58e1136e.png#clientId=ua614fb9f-b410-4&from=paste&height=373&id=u7ec0c6d5&originHeight=746&originWidth=1518&originalType=binary&ratio=1&rotation=0&showTitle=false&size=495653&status=done&style=none&taskId=u76511941-ff9b-449b-a62d-e047493e313&title=&width=759)

#### VLAN技术 
![image.png](https://cdn.nlark.com/yuque/0/2022/png/21806976/1641908115477-7b7313c1-53cb-4195-8cf5-8e0a1ccda1c6.png#clientId=uec69a367-c14f-4&from=paste&height=383&id=u49d79309&originHeight=766&originWidth=1312&originalType=binary&ratio=1&rotation=0&showTitle=false&size=593673&status=done&style=none&taskId=uf0c1e998-c11a-476a-82f7-52afacf6e1d&title=&width=656)

### 网络层
#### 概述
![image.png](https://cdn.nlark.com/yuque/0/2022/png/21806976/1641908520735-2bcc6972-db9c-4628-9a9e-f0d2407786f5.png#clientId=uec69a367-c14f-4&from=paste&height=173&id=u14af9afe&originHeight=346&originWidth=1372&originalType=binary&ratio=1&rotation=0&showTitle=false&size=180951&status=done&style=none&taskId=uf6c32260-5b65-4107-a1a9-cfe3de912a0&title=&width=686)
#### IPV4地址

- 分类

![image.png](https://cdn.nlark.com/yuque/0/2022/png/21806976/1641912232227-5e90c725-d34d-48a4-bf34-73a188ed759f.png#clientId=uec69a367-c14f-4&from=paste&height=385&id=u4f3c5d56&originHeight=770&originWidth=1602&originalType=binary&ratio=1&rotation=0&showTitle=false&size=544804&status=done&style=none&taskId=u2d1a4e85-5b3e-4350-920c-73502db8d71&title=&width=801)

- 子网划分（[子网掩码](https://www.bejson.com/convert/subnetmask/)）
- 无分类编址的IPV4地址：CIDR。 如：192.168.10.1/20 的CIDR块为  -->  192.168.0~192.168.15

![image.png](https://cdn.nlark.com/yuque/0/2022/png/21806976/1641914044222-589632eb-0b7f-430c-8a80-6638c7b48bbe.png#clientId=uec69a367-c14f-4&from=paste&height=376&id=u9f91f338&originHeight=752&originWidth=1564&originalType=binary&ratio=1&rotation=0&showTitle=false&size=513279&status=done&style=none&taskId=uac361037-6de0-4e3f-a6bf-69f08e5c1c3&title=&width=782)

- 定长子网掩码FLSM和变长的子网掩码VLSM
- IP数据报的发送和转发过程
- 路由协议概述
   - 静态路由：人工配置网络路由、默认路由、特定主机路由、黑洞路由
   - 动态路由：通过路由协议自动获取路由信息

![image.png](https://cdn.nlark.com/yuque/0/2022/png/21806976/1642079385840-b1beeb3e-4bff-417d-8e66-4e7e9adc4d60.png#clientId=u1e220b39-cf62-4&from=paste&height=281&id=u106bc16f&originHeight=562&originWidth=1536&originalType=binary&ratio=1&rotation=0&showTitle=false&size=645767&status=done&style=none&taskId=u445eda37-6908-4fcf-aa5d-728e3cf5b48&title=&width=768)<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/21806976/1642079504342-c9f17654-a513-45ea-b78d-682554744421.png#clientId=u1e220b39-cf62-4&from=paste&height=363&id=udaa7ed83&originHeight=726&originWidth=1572&originalType=binary&ratio=1&rotation=0&showTitle=false&size=397992&status=done&style=none&taskId=udf4c1427-5501-4c22-97eb-33a6fa651a1&title=&width=786)

- 路由信息协议：RIP协议（基于距离向量）

![image.png](https://cdn.nlark.com/yuque/0/2022/png/21806976/1642080103218-9a633ac1-f653-45de-a3ab-48363da328ca.png#clientId=u1e220b39-cf62-4&from=paste&height=352&id=u029c982d&originHeight=704&originWidth=1536&originalType=binary&ratio=1&rotation=0&showTitle=false&size=452711&status=done&style=none&taskId=ubae6eb65-68c9-4549-b2d0-c27e6ce4495&title=&width=768)<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/21806976/1642080300073-fa912ad7-9cda-4c95-b098-a27510860581.png#clientId=u1e220b39-cf62-4&from=paste&height=369&id=u2c32ddf4&originHeight=738&originWidth=1566&originalType=binary&ratio=1&rotation=0&showTitle=false&size=467835&status=done&style=none&taskId=uda59dd30-1d6a-47f4-b8f3-d07dfd0665d&title=&width=783)

- 路由信息协议：开放最短路径优先OSPF 基本工作原理（基于链路状态）

![image.png](https://cdn.nlark.com/yuque/0/2022/png/21806976/1642081286227-6e5832fd-f955-45eb-92b8-cbd668896349.png#clientId=u1e220b39-cf62-4&from=paste&height=377&id=ue42cdd6e&originHeight=754&originWidth=1386&originalType=binary&ratio=1&rotation=0&showTitle=false&size=322506&status=done&style=none&taskId=u43cc3524-f8ae-465d-8fb0-975ba59a62e&title=&width=693)<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/21806976/1642081406551-e6342218-43e6-4780-8489-cce4f8b67aa6.png#clientId=u1e220b39-cf62-4&from=paste&height=368&id=u913222bb&originHeight=736&originWidth=1226&originalType=binary&ratio=1&rotation=0&showTitle=false&size=322787&status=done&style=none&taskId=ub9448164-838f-4a76-abda-bf44fd777e9&title=&width=613)<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/21806976/1642081767384-3a18f5f8-5d0e-434f-922e-22cb59f9a710.png#clientId=u1e220b39-cf62-4&from=paste&height=317&id=ufc7955f2&originHeight=634&originWidth=1290&originalType=binary&ratio=1&rotation=0&showTitle=false&size=303120&status=done&style=none&taskId=u814524ed-3c30-41ea-b30c-7c4cac18e66&title=&width=645)<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/21806976/1642082197055-34ce96ab-6eac-486e-99a5-b1fb6d38aeee.png#clientId=u1e220b39-cf62-4&from=paste&height=362&id=uff014d9d&originHeight=724&originWidth=1578&originalType=binary&ratio=1&rotation=0&showTitle=false&size=741374&status=done&style=none&taskId=u7188fd97-90b1-48cc-8632-c2eec1dadfd&title=&width=789)

- 路由信息协议：边界网关协议BGP

![image.png](https://cdn.nlark.com/yuque/0/2022/png/21806976/1642083339203-3c9fca83-f82b-40ba-a9de-5448ea4986e3.png#clientId=u1e220b39-cf62-4&from=paste&height=407&id=uabb5449f&originHeight=814&originWidth=1554&originalType=binary&ratio=1&rotation=0&showTitle=false&size=590108&status=done&style=none&taskId=u122e7503-34b7-4a02-b817-c6302ca9b4e&title=&width=777)<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/21806976/1642083497066-417b9054-1d02-4eea-a8cf-1ec7bebf2392.png#clientId=u1e220b39-cf62-4&from=paste&height=209&id=u295c7ed2&originHeight=418&originWidth=1350&originalType=binary&ratio=1&rotation=0&showTitle=false&size=192477&status=done&style=none&taskId=udc3fb66a-ad3a-4702-9912-c1bdc9b98d0&title=&width=675)

- IPV4数据报首部格式

![image.png](https://cdn.nlark.com/yuque/0/2022/png/21806976/1642083717131-173ef5c7-cf59-41b9-a63e-d38470e390b3.png#clientId=u1e220b39-cf62-4&from=paste&height=183&id=u3900d5d3&originHeight=366&originWidth=1018&originalType=binary&ratio=1&rotation=0&showTitle=false&size=79673&status=done&style=none&taskId=ua0c01ef4-ba5a-4b1c-8616-1a3ec9e2ee4&title=&width=509)

- 网际控制报文协议ICMP
   - 终点不可达、源点抑制、时间超过、参数问题、改变路由（重定向）

![image.png](https://cdn.nlark.com/yuque/0/2022/png/21806976/1642086018918-640cd438-b84b-4eb4-afdf-8fa8ab7aff59.png#clientId=u1e220b39-cf62-4&from=paste&height=388&id=u599fb791&originHeight=776&originWidth=1480&originalType=binary&ratio=1&rotation=0&showTitle=false&size=527843&status=done&style=none&taskId=u817909b3-4fa0-4e41-a93e-45b17eb9ed7&title=&width=740)

   - ping、traceroute

![image.png](https://cdn.nlark.com/yuque/0/2022/png/21806976/1642085628013-769984db-fd72-410e-8fa7-bc89badf4c27.png#clientId=u1e220b39-cf62-4&from=paste&height=341&id=u96978c37&originHeight=682&originWidth=1550&originalType=binary&ratio=1&rotation=0&showTitle=false&size=408465&status=done&style=none&taskId=ucb061b3b-bd7b-45a0-ba13-aa32fdb7381&title=&width=775)![image.png](https://cdn.nlark.com/yuque/0/2022/png/21806976/1642085730696-0ad685cd-f514-4557-85e1-6f7511bf86ec.png#clientId=u1e220b39-cf62-4&from=paste&height=311&id=uccb9d922&originHeight=622&originWidth=802&originalType=binary&ratio=1&rotation=0&showTitle=false&size=151153&status=done&style=none&taskId=u378e3fe3-8c71-4596-a143-f9ad13a2bda&title=&width=401)

- 虚拟专用网VPN与网络地址转换NAT

![image.png](https://cdn.nlark.com/yuque/0/2022/png/21806976/1642086647630-fad2618d-00d3-4a54-bd70-a0607915fd0d.png#clientId=u1e220b39-cf62-4&from=paste&height=378&id=uad231ba1&originHeight=756&originWidth=1570&originalType=binary&ratio=1&rotation=0&showTitle=false&size=605982&status=done&style=none&taskId=u3213ba0f-66fb-43e9-9ac4-93aed4b33d8&title=&width=785)
### 传输层
#### TCP 与UDP 对比
![image.png](https://cdn.nlark.com/yuque/0/2022/png/21806976/1642337999907-69c654a8-45b4-4e59-9dbe-c81a4e93f871.png#clientId=u54177276-832c-4&from=paste&height=393&id=u2421f487&originHeight=786&originWidth=1578&originalType=binary&ratio=1&rotation=0&showTitle=false&size=390712&status=done&style=none&taskId=ufda2ffca-6e17-4466-92d0-a1e05a344b9&title=&width=789)
#### TCP原理

- 流量控制（滑动窗口）

![image.png](https://cdn.nlark.com/yuque/0/2022/png/21806976/1642338894633-a2106646-87cc-47da-9a97-7a40854a5349.png#clientId=u54177276-832c-4&from=paste&height=262&id=u91b9c640&originHeight=524&originWidth=1358&originalType=binary&ratio=1&rotation=0&showTitle=false&size=335536&status=done&style=none&taskId=u00a6585e-b56b-4170-84ef-235e402f38a&title=&width=679)

- 拥塞控制
   - Tahoe 版本
      - 慢开始
      - 拥塞避免
   - Reno 版本
      - 快重传（发送方尽快重传，非等待超时计时器）
      - 快恢复

![image.png](https://cdn.nlark.com/yuque/0/2022/png/21806976/1642339885902-198d2957-d8fe-463d-b7e5-6fc13be3048d.png#clientId=u54177276-832c-4&from=paste&height=343&id=uc4eee31d&originHeight=686&originWidth=1578&originalType=binary&ratio=1&rotation=0&showTitle=false&size=539620&status=done&style=none&taskId=ua88520ec-7a96-459b-b3b2-ffa0d9a6082&title=&width=789)<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/21806976/1642340049713-a78a5f8a-957e-4d8a-95b9-85a230ccf5c6.png#clientId=u54177276-832c-4&from=paste&height=322&id=u3b0cedec&originHeight=644&originWidth=1564&originalType=binary&ratio=1&rotation=0&showTitle=false&size=397272&status=done&style=none&taskId=ua8eb8984-2b89-4846-a20c-2e21428f923&title=&width=782)

- 超时重传选择（RTO 重传超时时间取值）
- 可靠传输实现
- 三次握手与四次断开

![image.png](https://cdn.nlark.com/yuque/0/2022/png/21806976/1642342959752-24b64eaf-245d-47e5-8894-6b37bef14b7b.png#clientId=u54177276-832c-4&from=paste&height=374&id=u11862b20&originHeight=748&originWidth=1594&originalType=binary&ratio=1&rotation=0&showTitle=false&size=337405&status=done&style=none&taskId=u2f7ad469-22eb-4278-ab3b-a4b17c141f2&title=&width=797)

- 首部格式

![image.png](https://cdn.nlark.com/yuque/0/2022/png/21806976/1642343737814-81b34fba-336b-4b5d-adb1-d3f1390c4b5b.png#clientId=u54177276-832c-4&from=paste&height=223&id=uc3f70960&originHeight=446&originWidth=1314&originalType=binary&ratio=1&rotation=0&showTitle=false&size=114509&status=done&style=none&taskId=uac536a63-8a67-4e67-9fa5-353c9672ef7&title=&width=657)

### 应用层
#### C/S方式与P2P方式
![image.png](https://cdn.nlark.com/yuque/0/2022/png/21806976/1642427235011-b81b9bfb-77c7-4e3d-b1d1-5cee3df8d8b3.png#clientId=u54177276-832c-4&from=paste&height=409&id=u9b96943f&originHeight=818&originWidth=1586&originalType=binary&ratio=1&rotation=0&showTitle=false&size=996336&status=done&style=none&taskId=u7edda731-0475-4757-a0d4-8ea52191f93&title=&width=793)

#### DHCP、DNS、FTP、SMTP、HTTP 等协议


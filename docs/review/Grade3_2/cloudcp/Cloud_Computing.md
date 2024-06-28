# 云计算(AWS那个文档)
## 云计算简介

### 云计算的三种模式

#### IaaS (Infrastructure as a Service)

> With IaaS (or Infrastructure as a Service), you manage the server, which can be
physical or virtual, as well as the operating system (Windows or Linux). **In general, the
data center provider has no access to your server**.

Basic building blocks for cloud IT include:

+ Networking features （网络）
+ Compute（计算）
+ Data storage space （数据存储空间）

#### PaaS (Platform as a Service)

> With PaaS (or Platform as a Service), someone else manages the underlying
hardware and operating systems. This enables you to run applications **without**
managing underlying infrastructure (for example -- patching修复, updates, maintenance,
hardware and operating systems). PaaS also provides a **framework**框架 for developers
that they can build upon to create customized applications.

#### SaaS (Software as a Service)

> With SaaS (or Software as a Service), you manage your files, while the service
provider takes care of all of the data centers, servers, networks, storage, 
maintenance, patching, etc. All you worry about is the software and how you want to
use it. You are provided with a complete product that is run and managed by the
service provider. **Facebook and Dropbox** are examples of SaaS. You manage your
Facebook contacts and Dropbox files, and the service providers manage the systems. 

### three cloud deployment models 三种云部署模型

#### "All-In" Cloud

> "All-In" Cloud is a cloud-based application that is **fully deployed in the cloud**, and all parts of
the application run in the cloud. Applications in the cloud have either been created in the
cloud or have been migrated from an existing infrastructure. Cloud-based applications can be
built on low-level infrastructure pieces (for example, networking, compute or storage) or can
use higher-level services that provide abstraction from the management, architecting, and
scaling requirements of core infrastructure.

#### Hybrid

> A hybrid deployment is a way to connect infrastructure and applications between cloudbased resources and existing resources that are not located in the cloud. The most common
method of hybrid deployment is between the cloud and existing on-premises infrastructure
(sometimes called on-prem). On-premises本地 infrastructure is located within the physical
confines of an enterprise, often in the company's data center. A hybrid deployment model is
used to extend an organization's infrastructure into the cloud while connecting cloud
resources to an internal system.
混合部署模型将组织基础设施扩展到云中，同时将云资源与内部系统相连接


#### Private Cloud

> When you run a cloud infrastructure **from your own data center**, that’s called on-premises or
private cloud. While this kind of deployment lacks many of the benefits of cloud computing, it
does provide dedicated resources and is a popular choice for organizations who need to meet
certain compliance standards. In most cases, this deployment model is the same as legacy IT
infrastructure while using application management and virtualization to increase resource
utilization.

### 云计算特性

+ **High availability**高可用性：High availability refers to a resource that is accessible when you attempt to access it
+ **Fault tolerance**容错：Fault tolerance is the ability to withstand a certain amount of failure and still remain
  functional. It also refers to the ability of a system to be self-healing and return to full capacity
  despite a failure. It is the ability of a system to fail in some way but still remain functional. 
+ **Scalability**可扩展性：Scalability is the ability to easily grow in size, capacity, and/or scope when required
  particularly in response to demand. If something cannot quickly grow in an easy manner it is
  not scalable.
+ **Elasticity**弹性：Elasticity is the ability to not only grow (or scale) when required, but also to reduce or
  contract in size as needed. A system that is elastic can scale to grow as needed usually based
  on demand and contract as demand decreases.（可以按需增减）

### 云的优势

+ Advantage 1: Trade Capital Expense for Variable Expense 可变费用
+ Advantage 2: Benefit from massive economies of scale. 大规模经济
+ Advantage 3: Stop guessing about r infrastructure capacity. 不用提前估基础设施容量
+ Advantage 4: Increase speed and agility. 高速、敏捷
+ Advantage 5: Stop spending money running and **maintaining data centers**.
+ Advantage 6: Go global in minutes（其实就是让部署变得简单）

## AWS--Amazon Web Services
> The duty of Amazon Web Services (AWS) is to provide secure cloud services to organizations. AWS offers a wide range of cloud computing services, including computing power, database storage, applications, and other IT resources through a cloud services platform via the internet. AWS aims to enable organizations to consume computing and storage resources without the need to build, operate, and maintain infrastructure on their own. Additionally, AWS focuses on providing flexible, scalable, and cost-effective solutions to help businesses innovate and grow.

> The foundation for the AWS infrastructure are the **data centers**. A data center is a location
where the actual physical data resides. AWS data centers are built in clusters in various global
regions.
### Web Service

> Web 服务是任何可以通过 Internet 或其他方式使用的软件在专用（内联网）网络上。 
> Web 服务使用标准化格式**（例如 XML 或 JSON）**用于 API 交互的请求和响应。它不依赖于
任何一种操作系统或编程语言，它都是通过一个自我描述的
接口定义文件并且是可发现的。

### AWS intro
> The AWS cloud provides a broad set of infrastructure services, such as compute power,
storage options, networking, and databases delivered as an on-demand utility that is
available in seconds, with pay-as-you-go pricing. All of these services reside on AWS global
infrastructure. 



![截屏2024-06-28 15.44.59](Cloud_Computing.assets/%E6%88%AA%E5%B1%8F2024-06-28%2015.44.59.png)

![截屏2024-06-28 15.45.49](Cloud_Computing.assets/%E6%88%AA%E5%B1%8F2024-06-28%2015.45.49.png)

![截屏2024-06-28 15.46.57](Cloud_Computing.assets/%E6%88%AA%E5%B1%8F2024-06-28%2015.46.57.png)




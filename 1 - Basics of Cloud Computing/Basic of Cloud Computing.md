# Basics of Cloud Computing, Vocabulary and Terinology-

### What is Cloud Computing?

Cloud Computing is the on demand delivery of computing resources, such as Storage, Servers, Networking, Databases, Software, Analytics and Intelligence, etc, over the internet.

### What is Cloud?

_Accessing a Data Center remotely is called cloud._

Cloud is the platform which provides on demand delivery of computing resources such as Storage, Networking, Databases, Software, Analytics and Intelligence, etc.

### Why do we need cloud?

There are multiple reasons to choose cloud:

- **TO save cost**:
  - If you want to run a website, instead of buying and maintaining your own server (which can be expensive and require dedicated IT staff), you can host your website on a cloud service and pay only for what you use.
 
- **For Scalability and Flexibility**:
  - Imagine you run an online store that suddenly becomes very popular during a holiday sale. With traditional servers, you’d need to buy extra hardware to handle the increased traffic. With cloud computing, you can quickly scale up your resources (more servers, more storage) to handle the surge and scale them down when the traffic drops.

We know that if we have an application we need a server to expose that application to outside world.

- **What is Server?**

  Server is a remote computer which has Local Storage, CPU and RAM. These servers are used to run application.

So, 10 or 15 years back companies like Google, Yahoo procure the servers from vendors like IBM, HP, etc. These companies used to procure 100's of servers from vendors. To manage these servers companies had particular System Administrators which mangage these server. 

After few years back companies have their own servers. Procuring the servers from vendors used to seems expensive. So companies decided get their own servers.

- Example of Google:

  Google installed 100's or 1000's server inside the racks in its server rooms. These servers are connected through High Speed cables, Switches or Routers. This complete setup is called **_Data Center_**.

### Private Cloud Concept

_A Data Center which is dedicated to only one organization is the Private Cloud._

```Ye ek model hai jisme user ka khud ka data centre hota hai.```

**Definition: A company which has their own data center dedicated to them is called Private Cloud.**

If a company have their own data center so that data center is the private cloud for that company.

Nowdays every company has its own data center which we also call private cloud.

Some companies hire the servers from vendors like IBM, HP. So that servers is also the private cloud for companies, which only that company can use no other company can use it.

```
Agar company ke paas khud ka data centre hai to vah data centre us company ke liye private cloud bhi khalaya jata hai.

Aaj ke time par har company ke paas khud ka data centre bhi hota hai jisko hum private cloud bhi bhi kehta hain.

Kuch companies vendors jaise IBM, HP se servers hire karti hain, to vah servers us company ke liye private cloud ho jata hai.
Jisko sirf vohi company use kar sakti hai aur koi company use nahi kar sakti.
```
<br>

### Public Cloud Concept

_A Data Center which is owned by an organization and offered its service to other organization is Public Cloud._

```Ye ek model hai jisme user cloud providers se on-demand service purchase karta hai ya```

**Definition: It is a cloud service that third-party cloud providers like AWS, Azure, etc provide to other companies or people over the internet.**

Now Amazon or Microsoft came into the picture and start AWS and Azure cloud plaforms. Amazon and Microsft have built their data center all over the world and started offering on-demand servers. 

Big companies like Google can afford their own private cloud (Data Center), but mid-scale companies cannot, so this public cloud option has been started for those mid-scale companies.

- **Data Center**: Collection of servers connected with each other is called Data Center.

### Hybrid Cloud Concept.

```Ye ek model hai jisme ek user on-demand services public cloud se use krta hai aur us apne sensitive data ke liye khud ka data centre use karta hai```

**Definition: It is a computing environment that combines on-premises data center (also called private cloud) with a public cloud, allowing data and application to be shared between them.**

There are some companies that purchases on-demand cloud services from cloud provider like Azure or AWS and create their on-premises data center to handle sensitive data. This is called hybrid cloud.

```
   Kuch companies esi hoti hain jo Azure se on-demand cloud services purchase karti hain aur sensitive data ko handle karne
   ke liye khud ka on-premises data centre create kar leti hain, isi model ko hybrid cloud kehte hain.
```

### Vocabulary

**Virtualization**

Virtualization is a technology that allows you to run multiple virtual computers on a single physical computer.

- e.g., Suppose we have a computer with high configuration of 512 GB RAM and 1000 CPU. A developer needs a server to run his application. So we can install a Hyervisor on that computer and logically create 1 CPU or 2 CPU virtual machine or according to the developer's need. On which we can use multiple virtual machines on a single computer.

In case of Azure,  Azure has its own data center with high configuration machine. If a user need a virtual machine then hypervisor logically divide the machine according to the requirement and give it to the user. This is called concept of Virtualization.

Virtualization helps in better utilizing the resources of a single computer by dividing them among multiple virtual machine.

**API**

It stand for Application Programming Interface.

e.g., If we have to create a virtual machine on azure, we can open Azure portal in chrome and click osme buttons can create a virtual machine

What if?

A company wants 1000 virtual machines. So, it is not possible to a user to create 1000 virtual machines by clicking the buttons. So to deal with this, Azure has given the option of API where a user can can run shell, python and terraform scripts with some parameters to create any number of virtual machines.

This is the concept of API here.

**Regions and Avaiability Zones**

- **Availability Zones**: We can consider availability zones as a data center. You can there are mentions like zone 1, zone 2, zone 3. These zones are the data center. It means azure has three data centers (Zone 1, Zone 2, Zone 3) in a single region. It means to distribute your virtual machines across multiple data centers.

- **Regions**: Regions are like geographical identification.  Azure have multiple data center around the world so to identify the particular data center in the world, we have regions to identify which data center in which area in the world.

- **Scalability**: Scalability is the ability to change the size or power of an azure resource when increase in the usage of that resource.

- **Elasticity**: It means automatically scaling your infrastructure.

- **High Availability**: It means making your application avaialable most of the time. e.g, Instagram, Bank Application, etc.

- **Disaster Recovery**: It is a technique or mechanism where we have a plan or action if something goes worng.
  To deal with it in azure there is a backup of service or Creating copy of resource in another region.

- **Availability Set**: To distribute your virtual machines within a single data center(across fault domains and update domains). When you place VMs in an Availability Set, Azure automatically distributes them across both Fault Domains and Update Domains.

  - **Fault Domain**: A Fault Domain represents a group of VMs that share the same physical hardware (racks, power supply, network, etc.).
  - **Update Domain**: An Update Domain is a group of VMs that are updated (e.g., for host OS updates or hardware maintenance) at the same time.
 
  **How Fault Domains and Update Domains Work Together**:
  - When you place VMs in an Availability Set, Azure automatically distributes them across both Fault Domains and Update Domains.

    Example:
    - Suppose you have 6 VMs in an Availability Set.
    - Azure distributes them across 3 Fault Domains and 5 Update Domains:
      - Fault Domain 1: VM1 (Update Domain 1), VM4 (Update Domain 4).
      - Fault Domain 2: VM2 (Update Domain 2), VM5 (Update Domain 5).
      - Fault Domain 3: VM3 (Update Domain 3), VM6 (Update Domain 1).
    - If Fault Domain 1 fails, only VM1 and VM4 are affected.
    - During maintenance, Azure updates one Update Domain at a time, ensuring that at least 5 VMs remain available.

<br>
        
### Cloud Computing Models

Three types of Models - 

1 - Iaas (Infrastructure as a Service).

2 - PaaS (Platform as a Service).

3 - Saas (Software as a Service).

**Iaas (Infrastructure as a Service)**

IaaS is the on-demand access to cloud-hosted computing infrastructure like Servers, Storage capacity and Networking resources.

When you take the resource like VM, Storage and Networking and using these resources according to yourself then you are using azure as Iaas model.

**PaaS (Platform as a Service)**

PaaS is the on-demand access to a platform for developing and deploying your application without worying about the underlying infrastructure.

e.g., When you take the SQL database where you can create, update and delete your data without worying about the storage management.

e.g., When you take the Azure App Service where you can build and host web applications without dealing with server management.

**SaaS (Software as a Service)**

It is a cloud hosted ready-to-use application software. User pay a monthly or annual fee to use a complete application.

e.g., Microsoft Office 365, Microsoft Outlook, Gmail are the software where we use them as a saas model.


<br>
<br>

### Virtual Machine

Virtual machine is a remote computer that behaves like aphysical computer with its own CPU, Memory, Storage and Networking.

**How does Azure assings a vm to a user?**

```
Suppose azure ka ek data centre hai. us data centre main high configuration wala server hai. Azure portal se maine ek
windows vm ki request ki to Azure ke high configuration wale server par ek hypervisor installed hai. Yeh hypervisor logially
VM create karta hai.

To protal par request ke according hypervisor us server par logically virtual machine us user ko assign kar deta hai.
To ek bade server se logically ek requested hissa user ko assign ho jata hai.
```

Note: Azure does not support in-place upgrade os OS.

**Virtual Machine Components**

When we create a virtual machine that need some basic components in azure or on-premises.

- Operating System.
- Disk/Storage.
- Network Interface Card.

Pre-requisite o create azure virtual machine.

- Resource Group.
- Azure Virtual Network.

**Virtual Machine Disks**

Azure Virtual Mchine disks are the storage resource used to store the operating system, application and data for virtual machine running in the azure cloud.

```
Azure VM ki disk ek storage resource hoti hai jo operating system, applications aur data ko store karti hai.
```

Imagine you have a physical computer. It has a Hard Drive where you store all your files, programs and operating system. Azure disks are like virtual hard drives for virtual machines.

There are **Os Disk**, **Data Disk** and **Temprary Disk** in azure vm.

**OS Disk**
OS Disk contains the Opeating System for the virtual machine.

You can only have one os disk attached to a vm.

**Data Disk**

Data disk are additional disk attached to a vm to store data, applications files or other files. 

You can attach multiple data disks to a vm, depending on your storage needs.

It provides persistent storage that persists even if the vm is stopped or deallocated.

**Temporary Disk**

Temporary disks are temporary storage resouce provided by azure vm for temporary data storage.

It is not a persistent and deleted when the vm is deallocated or deleted.

<br>

**Create a duplicate VM from an existing vm**

There are 3 methods to create a duplicate VM from an existing vm:

- Capture Image.
- Snapshot and Create Managed Disk (simple).
- Azure VM Scale Set.

**Method - 1: Capture Image**

- Step-1: Stop the VM -
  ```Before capturing the image stop the vm.```

- Step-2: Capture an Image -
  ```From the portal, select on capture and capture the image.```

- Step-3: Create a new vm from captured image -
  ```Navigate to images page in portal. Select the captured image. Click on create vm from the image.```

<br>

**Method - 2: Sanpshot and Create Managed Disk**

- Step-1: Stop the VM -
  ```Before snapshot stop the vm```

- Step-2: Take OS Disk Snapshot -
  ```Go to VM Disk page, Select the os disk and click on snapshot.```

- Step-3: Create Managed Disk from snapshot -
  ```Navigae to snapshot page. Select the snapshot you created and create a disk from it.```

- Step-4: Create a new VM using that disk -
  ```Navigate to disk page and click on create a new VM. This will attach the disk to a new VM. And your duplicate vm will be created with same login credentials.```

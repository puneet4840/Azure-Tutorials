# Basics of Cloud Computing, Vocabulary and Terinology-

### What is Cloud Computing?

Cloud Computing is the on demand delivery of computing resources, such as Storage, Servers, Networking, Databases, Software, Analytics and Intelligence, etc, over the internet.

### What is Cloud?

_Accessing a Data Center remotely is called cloud._

Cloud is the platform which provides on demand delivery of computing resources such as Storage, Networking, Databases, Software, Analytics and Intelligence, etc.

### Why do we need cloud?

We know that if we have an application we need a server to expose that application to outside world.

- **What is Server?**

  Server is a remote computer which has Local Storage, CPU and RAM. These servers are used to run application.

So, 10 or 15 years back companies like Google, Yahoo procure the servers from vendors like IBM, HP, etc. These companies used to procure 100's of servers from vendors. To manage these servers companies had particular System Administrators which mangage these server. 

After few years back companies have their own servers. Procuring the servers from vendors used to seems expensive. So companies decided get their own servers.

- Example of Google:

  Google installed 100's or 1000's server inside the racks in its server rooms. These servers are connected through High Speed cables, Switches or Routers. This complete setup is called **_Data Center_**.

### Private Cloud Concept

_A Data Center which is dedicated to only one organization is the Private Cloud._

**Definition: A company which has their own data center dedicated to them is called Private Cloud.**

If a company have their own data center so that data center is the private cloud for that company.

Nowdays every company has its own data center which we also call private cloud.

Some companies hire the servers from vendors like IBM, HP. So that servers is also the private cloud for companies, which only that company can use no other company can use it.

### Public Cloud Concept

_A Data Center which is owned by an organization and offered its service to other organization in Public Cloud._

**Definition: It is a cloud service that third-party cloud providers like AWS, Azure, etc provide to other companies or people over the internet.**

Now Amazon or Microsoft came into the picture and start AWS and Azure cloud plaforms. Amazon and Microsft have built their data center all over the world and started offering on-demand servers. 

Big companies like Google can afford their own private cloud (Data Center), but mid-scale companies cannot, so this public cloud option has been started for those mid-scale companies.

- **Data Center**: Collection of servers connected with each other is called Data Center.

### Hybrid Cloud Concept.

**Definition: It is a computing environment that combines on-premises data center (also called private cloud) with a public cloud, allowing data and application to be shared between them.**

There are some companies that purchases on-demand cloud services from cloud provider like Azure or AWS and create their on-premises data center to handle sensitive data. This is called hybrid cloud.

### Vocabulary

**Virtualization**

Virtualization is a technology that allows you to run multiple virtual computers on a single physical computer.

- e.g., Suppose we have a computer with high configuration of 512 GB RAM and 1000 CPU. A developer needs a server to run his application. So we can install a Hyervisor on that computer and logically create 1 CPU or 2 CPU virtual machine or according to the developer's need. On which we can use multiple virtual machines on a single computer.

In case of Azure,  Azure has its own data center with high configuration machine. If a user need a virtual machine then hypervisor logically divide the machine according to the requirement and give it to the user. This is called concept of Virtualization.

Virtualization helps in better utilizing the resources of a single computer by dividing them among multiple virtual machine.


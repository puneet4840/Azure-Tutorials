# Azure Active Directory

### What if there is not Active Directory?

The main function of Active Directory is **Authentication**. It authenticate username and password.

```Suppose आपके पास एक laptop है. तो आप किसी employee को एक laptop issue चाहते हो तो उस employee के लिए आप एक username create और password create करके उसको दे दोगे. जब भी user इस laptop पर अपने username और password से login करेगा तो वहां authentication होगा. तो जो भी authentication हो रहा है वो local authentication हो रहा है.```

```user अपना username और password डालता है और laptop के अंदर login कर लेता है```

 **Note**:- ```लेकिन इसके साथ बोहोत सारे challenges थे:-```

- ```अगर आपकी company छोटी है बस 10 या 15 employees हैं तो आप हर किसी employee के username और password create करके user को दे सकते हो| लेकिन अगर आपकी company बड़ी है और 1000 या 5000 employee काम करते हैं तो आप हर employee के लिए username और password create करके नहीं दे सकते| आप हर laptop पर जाकर username और password create करेंगे तो ये एक बोहोत difficult scenario हो जाता है, इसके लिए आपको एक अलग team बिठानी पड़ेगी|```

- ```दूसरा problem ये है की अगर user को एक दूसरा device दिया जाये तो उसके लिए भी username और password create करके देना पड़ेगा फिर जाकर user उस दूसरे device पर भी लॉगिन कर पायेगा|```

- ```तीसरा problem ये भी है की अगर user remote location पर काम करने जाता है और अपने username और password भूल जाता है तो ऐसे मैं आप as a administrator उसके device पर remotely access करके admin password के through उसका password reset करेंगे| ```

<br>
<br>

### Active Directory Explaination

Let's understand active directory here-

Suppose हमने एक server पर Active Directory install कर दी. जैसे ही किसी server पर Active Directory install हो जाती है तो उस server को **Domain Controller** कहा जाता है. इसको Domain Controller इसलिए कहा जाता है क्युकी ये एक domain यानि logical boundary बना देता है.

**e.g.,**

अगर आपकी कंपनी मैं कोई नया employee आया है तो उसके लिए आप एक laptop लेंगे और laptop को domain मैं join कराएंगे और साथ ही साथ उस employee का जो user account है उसको active directory में जाके create कर देंगे. 
- जैसे जब मैंने Nagarro join की थो तो Nagarro ने मुझे एक laptop अपने Nagarro के domain मैं join करके दिया था. मतलब उस laptop में मैं नगररो के username aur password से hi login कर सकता हूँ बस. 

**How does Active Directory works?**

When you want to login to your system. You type username and password then this information goes to active directory, if your credentials is correct you will be logged in successfully otherwise login will be failed.

**Note**:-

This is I told you about on-premise active directory. On-premises active directory is hectic to manage so then azure comes up with a new solution with **Azure Active Directory**.

<br>
<br>

### Azure Active Directory

Azure Active Directory is the cloud-based authentication and authorization system by Microsoft.

```OR```

Azure Active Directory is the cloud-based directory and identity and access management service.

The key function of Azure Active Directory is **Authentication** (verifying who are you) and **Authorization** (determining what you are allowed to access).

It is now known as **Entra ID**

<br>
<br>

**Why we need it?**

Imagine work in a large company with 1,000 employees. The company uses many different cloud-based services for services for everyday tasks such as:

- Email and Communication (Outlook, Teams).
- Data Storage (Azure Storage, SharePoint).
- Development Tools (Azure DevOps, GitHub).
- Customer Data (SQL Databases, CRM Tools).

In a scenario where there is a no centralized system like **Azure Active Directory**, each employee would need seperate username and password for each service they use. For Example:

- **Ram** in the sales department has one login for outlook, another login for sql database, and yet another for Azure DevOps.
- **Shyam** in the IT department has his own set of logins for same services, plus even more for tools he uses in the developement.

This approach having seperate credentials for every service creates a major issues such as:

- Employees has too many usernames and passwords to remember.
- Administrators must manually create and manage thousands of seperate logins for seperate services.
- People might write down passwords or use weak ones, which could lead unauthorized access or security breaches.

**How Azure Actice Directory solves this problem**

Let's introduce Azure AD to simplify the situation.

- **Single Sign-On (SSO)**: Ram, Shyam and every employee only need one username and password to access all the services they use. They log into Azure AD and it take care of sigining them into each services automaticlly without seperate logins.

- **Easier Access Control**: The administrator can setup groups (e.g., Sale, IT, Marketing) in Azure AD and assign the appropriate permission to each group.

Azure Active Directory is not limited to just Microsoft services. It can be used to manage and access any services.

<br>
<br>

### Azure Active Directory Hierarchy Architecture

Architecture of Azure AD revolved around three main components: **Directory**, **Tenant** and **Subscription**.

**Diagram**

<img src="https://github.com/user-attachments/assets/18e6228e-5f70-4c44-a209-79ed705d8c84" width="350" height="450">

<br>
<br>
<br>

**Basic Diagram**

<img src="https://github.com/user-attachments/assets/9d37748d-74b0-4de7-9266-b00fff40e81f" width="350" height="450">

<br>
<br>
<br>

**Explaination of AD Architecture components**

- **Directory**: Azure Active Directory is a container where all Users, Groups, Devices, Applications and Service Principal resides. Tenant is also created with it by default, this tenant is also called directory.

  e.g.,
  
  ```जब हम अपने Gmail से Azure पर एक account create करते हैं तो वहाँ एक default directory create हो जाती है. इसके साथ एक tenant भी create हो जाता है.```

- **Tenant**: A tenant is the instance of your active directory. A tenant is like the boundary for your directory. Within the tenant you control users, groups, roles and  applications.

  e.g.,

  ```Tenant एक तरह से boundary होती है directory की मतलब आपने एक account create किया जिससे एक directory create होगयी फिर साथ ही एक tenant भी create हो जायेगा जो आपकी organization को represent करेगा.```


- **Management Group**: A management group is a container to organize and manage the multiple subscription. You can create and apply policies at the management group level for managing multiple subscription.

- **Subscription**: A subscription the billing and management entity in azure. It is the layer where you manage Azure resources, usage, and billing. Multiple subscription can exists within a single tenant. The organization is billed based on resource usage under the subscription.

  - Types of Subscription:
     - Free Trial.
     - Pay-As-You-Go.
     - Reserved Instance.
     - Enterprise Agreement.

- **Resource Group**: A Resource Group is the logical isolation of the reosurces.

- **Resource**: A resource is the service which we use from azure.

<br>
<br>

### Role Assignment and Access Control

Azure Active Directory uses a flexible way to manage user access to resources. It uses Azure _AD Roles_ and _Role Based Access Control_ (**RBAC**) to manage user access.

There are two types of roles in Azure Active Directory:
- Azure AD Roles (Directory Roles).
- Azure RBAC Roles (Resource Roles).

<br>

**1 - Azure AD Roles (Directory Roles)**

These roles control the access to the identity and directory management features of Azure Active Directory (for users, groups, devices, apps). These roles are applied at the directory(tenant) level.

```Azure AD roles directory level पर access provide करने के लिए use किये जाते हैं. Suppose किसी user को directory level पर access देनी है तो हम AD roles से ही access दे सकते हैं. मतलब ये roles tenant level पर access देने के लिए होते हैं.```

Azure AD Roles are:

- **Global Administrator**: This roles has full access to manage Azure AD service, users, and groups including all administrative features. Can assign roles to other users. You can assign this role if a user needs full control over azure AD.

  e.g., A company's IT Admin who manages Users, Groups and Application access.

<br>

- **User Administrator**: This role can create and manages all aspects of users and groups, inclusing resetting passwords and assigning licesnces. You can assign this roles to users who will manage user accounts and group memberships but don't need full administrative rights.

  e.g., An HR admin who needs to add or remove employees and manage groups.

<br>

- **Application Administrator**: This role can manage application registrations, app proxy settings, and enterprise apps. Cannot manage azure AD itself.

  e.g., A developer managing API registrations for internal applications.

<br>
<br>
<br>

**2 - Azure RBAC Roles (Resource Roles)**

RBAC (Role Based Access Control) is the method to assign roles (permissions) to users, groups or application for access azure resources (such as VMs, Storage, Databases). These roles are applies at different level such as **Subscription**, **Resources Group** and **Resource**.

**Key concepts of RBAC**

- **Roles**: It is the collection of permission that a user can perform (e.g., Read, Write, Delete).
  
    - There are three types of roles in RBAC:
      
        - **Owner**: Full control over everything (e.g., create, delete, manage).
          
        - **Contributor**: Can create and manage resources not delete also cannot assign roles.
          
        - **Reader**: Can only view resources but cannot make any changes.
          
- **Scope**: It is the area where the role applies (e.g., Subscription, Resource Group, Resources).
- **Principals**: Users, Groups or Applications that receive the roles.

<br>
<br>

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

<img src="https://github.com/user-attachments/assets/18e6228e-5f70-4c44-a209-79ed705d8c84" width="350" height="600">

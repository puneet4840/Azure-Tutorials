# Active Directory Overview

<br>

### Directory Kya Hoti Hai?

Directory ka matlab hai ek database jisme kuch information stored hai aur vo information easily search ki ja sakti ho.

Directory = organized data + jise tum easily search kar sako

Directory ek database hota hai jisme data ek organized way mein store rehta hai jisme se data fast aur easy search kiya ja sakte.

Directory = ek list / record system jahan cheezein organized tarike se rakhi hoti hain, taaki tum unhe easily dhoondh sako.

<br>

**Example 1 — Phone Contacts**:

Socho tumhare phone mein contacts saved hain:

Contact-1:
- Naam: Puneet
- Number: 9876543210
- Email: puneet@gmail.com

Contact-2:
- Naam: Rahul
- Number: 9876894563
- Email: rahul@gmail.com

Contact-3:
- Naame: Aman
- Number: 9245637821
- Email: aman@gmail.com

To ye ek phone directory hai. 

To phone directory mein contact ek organized way mein stored hain. Aur contact ko easily search kiya ja sakta hai.

Tum kya karte ho: Agar kisi ko call lagana ho to tum directly naam search karte ho aur number mil jata aur call laga dete ho.

To data yahan ek organized way mein rakh hai jise tum easily search kar sakte ho. Isi ko bolte hain directory.

Ek esa record system, jaha:
- Data stored rehta hai.
- Organize way mein stored rehta.
- Aur easily search kiya ja sakta hai.

Isi ko bolte hain directory.


Directory ka matlab ek esa storeage system jaha data organize way mein store rahe aur easy search ho sake usi ko bolte hain directory.

<br>
<br>

### Active Directory Kya Hoti Hai?

Active Directory (AD) Microsoft ka ek Directory Service hai jo Windows network mein user, computer, printers, policies, permissions, aur resources ko centrally manage karne ke liye use hoti hai.

**Simple words mein**:

Socho ek badi company hai jisme 5000 employees hain. Har employee ke paas ek computer hai, aur har computer pe alag-alag software hain. Ab agar IT admin ko har computer pe manually jaake settings karna pade, passwords manage karna pade — toh yeh toh nightmare ho jaayega!

Is situation mein Active Directory kaam aata hai.

Active Directory ek central system deta hai jahan se:
- User login manage hota hai.
- Password control hota hai.
- Kaun kya access karega decide hota hai.
- Computer policies apply hoti hain.
- Security centralized hoti hai.

Active Directory ke ander user, computer, printers, policies, permissions, aur resources ki detailes stored rehti hai.

Active Directory ka main kaam hai **Authentication** aur **Authorization** karna.

<br>

**AD kaam kaise karti hai?**:

Jab koi employee apne office computer par login karta hai, to AD:
- **Authenticate** karti hai — क्या यह सही user है?
- **Authorize** karti hai —  इसे कौन-कौन सी files/resources access करने की permission है?
- **Apply** करती है — company policies automatically लागू करती है.

<br>

**Authentication**: “Tum kaun ho?”

Example:

Username: ```puneet```
Password: ```********```

AD verify karega:
- User exist karta?
- Password correct?
- Account locked?
- Expired?
- Disabled?

**Authorization**: “Tum kya kar sakte ho?”

Example:

Puneet DevOps team mein hai:
- AWS docs access ✅
- HR salary folder ❌
-s Production server SSH ✅
- Finance reports ❌

<br>

### Problem Without Active Directory

Example:

Company mein 1000 employees hain.

Har employee ko:
- Login chahiye.
- Email access chahiye.
- Printer access chahiye.
- Shared drive access chahiye.
- Department-specific permissions chahiye.

Agar AD nahi ho:

IT admin ko har computer pe manually:
- User banana.
- Password set karna.
- Permissions dena.
- Software install karna.
- Security configure karna.

Solution = Active Directory

Active Directory ek centralized identity aur management system hai.

Iska matlab, Ek central server decide karega:

WHO:
- Kaun user hai?

WHAT:
- Kya access kar sakta hai?

WHERE:
- Kis machine ya resource par jaa sakta hai?

HOW:
- Kaunsi policies apply hongi?

<br>

### Active Directory Ki History:
- 1999 mein Microsoft ne AD ko Windows Server 2000 ke saath launch kiya.
- Pehle sirf on-premise tha (matlab physical servers pe).
- Aaj Azure Active Directory (AAD) bhi hai — jo cloud-based version hai.
- Modern naam: Microsoft Entra ID (Azure AD ka naya naam).

<br>

### Active Directory ke main components:

- **Domain** — एक organization का network group (जैसे company.com).
- **Domain Controller (DC)** — वह server जो AD को run करता है, यह network का "brain" होता है.
- **Users & Groups** — employees के accounts और उनके groups.
- **Organizational Units (OU)** — departments को organize करने का तरीका (HR, IT, Finance)
- **Group Policy (GPO)** — rules जो automatically सभी computers पर apply होती हैं (जैसे password policy).


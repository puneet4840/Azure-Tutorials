# Azure Traffic Manager Overview

Azure Traffic Manager ek DNS-based global traffic routing service hai jo users ko best endpoint par direct karti hai.

<br>

Traffic Manager ek routing service hai jo user ko uske paas wale server ki IP deti hai, matlab user ki request ko uske paas wale server ke paas bhejta hai.

Isko ese samjho jaise aapne 4 alag-alag regions jaise US, UK, India, Singapore mein apna application host karne ke liye server banaye hain, in servers ke front mein ek traffic manager hai, ab agar user ki request traffic manager par jayegi to traffic manager, user ki request ko dekh ke uske paas wale server uski request ko bhej dega.

Example:

Jab aap google.com apne browser mein access karte ho, Google ne har country mein apne servers banaye hue hain, google ne traffic manager host kar rakha hoga jo in servers ke front mein chal rha hoga, ab jaise me google.com browser mein hit karta hu, to traffic manager mujhe india wale server pe bhej dega aur google page bohot fast khulega. 

<br>
<br>

### Sabse Pehle Problem Samjho – Global Applications

Internet ke early days mein applications simple hoti thi.

Example:
```
Ek company ka ek server hota tha
Ek hi data center mein
Ek hi country mein
```

User request karta tha:
```
User → Server
```
To user ki request direct server par jaati thi.

Sab simple tha.

<br>

**Problem kab start hui?**:

Jab global users aane lage.

Example:

Ek company hai jiska server US mein hai.

Us company ki website par users alag-alag countries se aate hain, jaise:
```
India
Europe
Australia
Africa
```
Sab users request bhejte hain US server par.

To jab company ka ek hi server hoga US mein aur users alag-alag countries se aane lagenge. To is case mein server par issue aane lagenege.

<br>

**Issues kya aane lage?**:

**1 - High latency**:

Agar India se koi user US server par request karne lagega to uski request server tak pahuchne mein time le legi, jisse hoga ye user ko website bohot slow load hone lagegi.

User bolega:
```
Bohot slow website hai
```
Isi slowness ko hum latenct bolte hain, Latency ka matlab request ko aane aur jaane mein lagne wala time.

Example:
```
India → US server = 250ms latency
```
Website slow ho gayi.

<br>

**2 - Server overload**:

Agar company ka US ke ander sirf ek hi server chal rha hai, company ne apni website par sale chalu ki, aur website par million users aa gaye:

To server overload ho jayega aur crash ho jayega, jisse website down ho jayegi.
```
1 server overload
```

<br>

**3 - Single point of failure**:

Agar server crash ho gaya:
```
Entire website down
```

<br>

**4 - Disaster**:

Agar kisi disaster ki wajah se jaise, Earthquake, Tsunami, Power Failure, Fire, etc. Kisi bhi wajah se jis datacenter mein server chal rha hai, agar vo down ho gya to server bhi down ho jayega, Company ki website down, business down, revenue loss.

Example:
```
US data center down
Entire application unavailable
```

<br>

To single server ka use karne par ye uper likhi hui problems aati hain. To iske liye kuch na kuch solution chaiye tha, To ab aage solution dekhte hain.

<br>
<br>

**Solution kya nikla?**:

Companies ne multiple regions mein servers deploy karna start kiya.

Ab companies ne socha ki hum ek region mein apna server run karne ke bajaye alag-alag regions mein server run karenge. Obiously issue cost to badhni thi lekin company ko apna loss nhi chaiye tha.

Example:
```
US
Europe
India
Australia
```

In sabhi server par company ki same website chalti.

Architecture:
```
Users → ??? → Best server
```

Ab question tha:
- Ki company ne alag-alag regions mein apne server to chala diye, lekin user ki request ko konse best server par le jaya jaye.
- Itne server chalane ke baad bhi agar user ki request US ke server par hi aayegi to ye itne server chalane ka koi fayda nhi.
- To question yahi tha ki **User ko kaunsa server diya jaye?**.

Yahi problem solve karta hai **Azure Traffic Manager**.

<br>
<br>

### Traffic Manager Kya Hai?

Traffic manager azure ki ek service hai jo user ki request ki request ke hisab se user ke paas wale server ka IP de deti hai.

Traffic Manager decide karta hai:
```
User ko kis region ke server ka IP dena chahiye. Jisse user ko website fast access ho.
```

Yeh DNS level par kaam karta hai.

<br>

Sabse pehle simple language mein samjho.

Maan lo tumhari website hai:
```
www.mycompany.com
```

Aur tumhari application 3 regions mein deployed hai:
- East US.
- West Europe.
- Southeast Asia.

Ab duniya bhar se users aa rahe hain.

Problem kya hai?

Agar:
- India ka user US server par chala gaya.
- Europe ka user Asia server par chala gaya.

To:
- latency badh jayegi.
- performance slow ho jayegi.
- user experience kharab ho jayega.

Isi problem ko solve karne ke liye Azure Traffic Manager bana hai.

Traffic Manager kya karta hai ki user ki reqeust ke hisab se, in sabhi server mein se jo user ke paas wala server hoga, us server ki IP ko browser ko de deta hai.

Yahi traffic manager ka role khatam ho jata hai.

Browser ko IP mil jati hai aur browser website se direct connect karta hai.

Iska matlab traffic manager DNS browser ki request ka DNS resolution karta hai aur best server ki IP browser ko de deta hai.

Isi ka matlab hai DNS-based global traffic routing.

<br>
<br>

### Traffic Manager Kaam Kaise Karta Hai?

Traffic Manager Actual Traffic Ko Route Nahi Karta. Ye bahut important concept hai jo beginners confuse kar dete hain.

Traffic Manager:
- ❌ Traffic ko proxy nahi karta.
- ❌ request ko forward nahi karta.
- ❌ packet ko route nahi karta.

Instead:
- ✅ DNS response change karta hai.

<br>

**Isko aur detail mein samjhte hain**:

<br>

Sabse pehle, jab aap Azure Portal mein Traffic Manager profile banate hain, toh aapko teen main cheezein define karni hoti hain:
- **Endpoints**: Ye wo destination hain jahan aap traffic bhejna chahte hain. Ye Azure App Service ho sakti hai, Public IP ho sakta hai, ya fir aapke office ka koi on-premise server.
- **Routing Method**: Aap Traffic Manager ko batate hain ki faisla kaise lena hai (Priority, Performance, Weighted, ya Geographic).
- **Health Probe**: Aap ek "Monitor" set karte hain jo har 30 second mein endpoints ko check karta rehta hai ki wo "Alive" (Healthy) hain ya nahi.

<br>

**Step-by-Step Workflow (The Journey of a Request)**:

Maante hain ki aapki ek website hai ```www.simplyexplains.com``` aur aapne ise Traffic Manager ke saath set kiya hai.

Step A: User ka Request:

- Jab ek user apne browser mein ```www.simplyexplains.com``` type karta hai, toh browser ko ye nahi pata ki iska IP address kya hai. Browser sabse pehle DNS Recursive Resolver (aapke Internet Provider ka DNS) ke paas jata hai aur puchta hai— "Bhai, is website ka IP kya hai?"

<br>

Step B: DNS Chain Reaction:

- DNS resolver request ko ghumate-ghumate Azure ke Traffic Manager Name Server tak pahunchata hai. Kyunki aapne apni website ka CNAME record Traffic Manager ke URL (jaise ```myapp.trafficmanager.net```) se connect kiya hua hai.
  
- Jab tum Traffic Manager create karte ho to Azure ek DNS deta hai:
```
simplyexplains.trafficmanager.net
```

- Tum apni domain ko is par map karte ho:
```
www.simplyexplains.com → CNAME → simplyexplains.trafficmanager.net
```

<br>

Step C: Traffic Manager ka Faisla (The Brain):

Ab Traffic Manager picture mein aata hai. Wo niche di gayi teen cheezein turant check karta hai:
- Routing Rule: Agar aapne 'Performance' rule set kiya hai, toh wo dekhega ki user ki location se sabse kam latency wala server kaunsa hai.
- Endpoint Health: Kya wo server up hai? (Health probe se pata chalta hai).
- Current Status: Agar primary server down hai, toh wo backup server ko dhoondhega.

<br>

Step D: IP Address Delivery:

Traffic Manager user ko data nahi bhejta. Wo sirf Selected Server ka IP Address DNS resolver ko wapas bhej deta hai.

<br>

Step E: Browser Connection:

Ab browser ko IP address mil gaya hai. Browser ab directly us server (e.g., Azure App Service in East US) se connect hota hai aur website load karta hai. Is point ke baad Traffic Manager ka kaam khatam ho jata hai. Browser aur Server ke beech hone wali saari baatein (Images, Videos, Data) seedhi hoti hain, Traffic Manager ke through nahi jati.

<br>
<br>

**Important Point: DNS Caching aur TTL (Time-To-Live)**:

Ye sabse important point hai. DNS records computer mein "Cache" ho jate hain.
- Azure Traffic Manager ka default TTL 300 seconds (5 minutes) hota hai.
- Iska matlab agar koi server down ho gaya, toh shayad 5 minute tak users ko purana IP hi milta rahe kyunki browser sabse pehle locally DNS check karta hai aur DNS ke records local hosts file mein save ho jate hain. Aap ise kam karke 30-60 seconds bhi kar sakte hain fast failover ke liye.

<br>
<br>
<br>

### Traffic Manager ke components


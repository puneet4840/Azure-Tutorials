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

**Flow**:
```
User Browser
     |
     | DNS Query
     v
Azure Traffic Manager
     |
     | Select best endpoint
     v
Endpoint IP returned
     |
     v
User directly connects to endpoint
```

<br>
<br>

**Important Point: DNS Caching aur TTL (Time-To-Live)**:

Ye sabse important point hai. DNS records computer mein "Cache" ho jate hain.
- Azure Traffic Manager ka default TTL 300 seconds (5 minutes) hota hai.
- Iska matlab agar koi server down ho gaya, toh shayad 5 minute tak users ko purana IP hi milta rahe kyunki browser sabse pehle locally DNS check karta hai aur DNS ke records local hosts file mein save ho jate hain. Aap ise kam karke 30-60 seconds bhi kar sakte hain fast failover ke liye.

<br>
<br>

### Global Load Balancing ke liye Azure Front Door tha to Azure Traffic Manager ki Jarurat kyu hui

Front Door aur Traffic manager dono alag-alag problems ko solve karte hain.

<br>

**Sabse Pehle Ek Internet Reality Samjho**:

Jab bhi koi user website open karta hai, actual HTTP request se pehle ek aur important step hota hai.

Wo hai DNS resolution.

Complete process kuch aisa hota hai:
```
User types URL in browser
↓
DNS lookup hota hai
↓
IP address milta hai
↓
User server se connect karta hai
↓
HTTP request jati hai
```

Yahan ek important baat samjho.
- Front Door HTTP request send karne ke baad kaam karta hai.
- Traffic Manager HTTP request send karne ke pehle kaam karta hai.

<br>

**Traffic Manager Ka Kaam Kis Stage Par Hota Hai**:

Traffic Manager ka kaam DNS stage par hota hai.

Maan lo tumhari website hai:
```
www.shopworld.com
```

User India se website open karta hai.

Browser sabse pehle DNS se puchta hai:
```
shopworld.com ka IP kya hai?
```

DNS request Traffic Manager tak pahuchti hai.

Traffic Manager check karta hai:
- user ka location.
- endpoints ki health.
- routing method.

Phir Traffic Manager bolta hai:
```
Asia server ka IP = 20.40.50.60
```

User directly connect karta hai:
```
User → Asia server
```

Traffic Manager ka kaam yahi khatam ho jata hai.

Wo data traffic ko touch bhi nahi karta.

<br>

**Front Door Ka Kaam Kis Stage Par Hota Hai**:

Front Door DNS stage par kaam nahi karta.

Front Door ka role tab start hota hai jab user ki request ko server ki IP mil jati hai aur request server par pahuchne wali hoti hai, To request server par pahuchne se phle Front Door ke paas pahuchti hai.

Kyuki server se pehle Front Door work kar rha hota hai, Front Door ke backend mein server laga hota hai.

Example.

User DNS resolve karta hai:
```
www.shopworld.com
↓
Front Door ka IP milta hai
```

Ab request flow aisa hota hai:
```
User
↓
Nearest Microsoft Edge POP
↓
Front Door
↓
Backend Server
```

Front Door user request ko receive karta hai aur phir backend ko forward karta hai.

Traffic Manager ka kaam hota hai:
```
DNS level routing
```

Front Door ka kaam hota hai:
```
Layer 7 proxy routing
```

<br>

**Ab Sabse Important Difference Samjho**:

Front Door ek proxy service hai.

Proxy ka matlab:
```
User
↓
Proxy
↓
Server
```

Traffic Manager proxy nahi hai.

Wo bas DNS response change karta hai.

<br>

**Ek Aur Practical Difference**:

Maan lo tumhare paas ek gaming server hai.

Protocol:
```
UDP
```
Front Door use nahi kar sakte.

Kyuki Front Door sirf support karta hai:
```
HTTP
HTTPS
```

Traffic Manager use kar sakte ho.

Kyuki Traffic Manager protocol se independent hai.

Wo sirf IP return karta hai.

<br>

**Ek Real Production Architecture**:

Bahut bade enterprises dono ko saath use karte hain.

Example:
```
User
↓
Traffic Manager
↓
Regional Front Door
↓
Backend cluster
```

Yahan:

Traffic Manager decide karta hai:
```
Kaunsa region
```

Front Door decide karta hai:
```
Kaunsa backend service
```

<br>
<br>

**Lekin front door bhi to request ko nearest server tak le ja rha hai**:

Azure Front Door bhi request ko nearest / fastest backend tak pahucha deta hai. Is wajah se bahut log confuse ho jaate hain aur sochte hain ki phir Azure Traffic Manager ki zarurat kyu hai.

Ab Samjho:

Jab koi user internet par kisi website ko open karta hai, to sabse pehle browser ko ye pata karna padta hai ki server ka IP address kya hai. Browser directly URL se server tak nahi pahuch sakta. Pehle DNS se IP milta hai, phir connection establish hota hai.

Isi stage par Traffic Manager ka role start hota hai. Traffic Manager basically ek intelligent DNS system hai. Jab DNS query aati hai, to wo decide karta hai ki user ko kaunsa server ka IP diya jaye. Ye decision user ke location, endpoint health aur routing policy par depend karta hai.

Iska matlab ye hua ki Traffic Manager user ko bas ek direction deta hai:
“Tum is server par connect karo.”

Uske baad user ka browser directly us server se connect ho jata hai. Traffic Manager ka kaam wahi khatam ho jata hai. Wo actual request ke data path mein nahi aata.

<br>

Front Door ka behaviour completely different hai. Front Door DNS response dene ke baad disappear nahi ho jata. Balki user jab connect karta hai to request sabse pehle Front Door ke global edge network par aati hai.

Microsoft ke world-wide edge POPs hote hain (points of presence). Jab user connect karta hai, to request automatically nearest Microsoft edge location par land karti hai. Wahan Front Door request ko receive karta hai, inspect karta hai, optimize karta hai, aur phir backend server ko forward karta hai.

Iska matlab ye hua ki Front Door actual traffic path ke beech mein baitha hota hai.

Request ka path kuch is tarah hota hai:
```
User → Microsoft Edge POP → Front Door → Backend Server
```
Yahan Front Door ek proxy / gateway ki tarah behave karta hai.

<br>

Ab tumhari confusion ka core point yahi hai:

Tum keh rahe ho ki Front Door bhi nearest backend choose karta hai.

Bilkul karta hai.

Lekin difference ye hai ki Front Door nearest backend choose karta hai apne network ke andar, jabki Traffic Manager nearest backend choose karta hai DNS stage par.

Matlab ek decision connection banne se pehle hota hai, aur doosra decision connection banne ke baad.

<br>

Ek aur important cheez samajhni zaroori hai.

Front Door sirf HTTP aur HTTPS traffic ke liye design kiya gaya hai. Matlab web applications ke liye. Agar koi service web protocol par nahi chal rahi, jaise gaming server, SMTP service, FTP service ya custom TCP/UDP protocol, to Front Door ka use nahi kiya ja sakta.

Traffic Manager par ye limitation nahi hai. Kyunki wo actual traffic ko route hi nahi karta. Wo sirf DNS response deta hai. Isliye wo kisi bhi protocol ke saath kaam kar sakta hai.

<br>

Ek aur subtle difference latency aur architecture flexibility ka hai.

Front Door mein traffic hamesha ek extra hop se guzarta hai. Pehle Microsoft edge network, phir backend. Ye usually beneficial hota hai kyunki Microsoft ka network optimized hota hai. Lekin kuch ultra-low latency applications mein companies prefer karti hain ki client directly server se connect kare.

Traffic Manager exactly ye allow karta hai.

<br>

Large enterprise architectures mein kabhi kabhi dono ko ek saath bhi use kiya jata hai.

Traffic Manager global level par decide karta hai ki request ko kis continent ya region mein bhejna hai. Us region ke andar Front Door request ko receive karta hai aur wahan ke backend clusters mein distribute karta hai.

Is tarah ka architecture global scale systems mein kaafi common hai.

<br>
<br>


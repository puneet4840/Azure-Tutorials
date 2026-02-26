# Azure Application Gateway Overview

Azure Application Gateway ek Layer-7 (Application Layer) load balancer hai jo incoming requests ko receive karta hai aur uske peeche maujood multiple Virtual Machines (VMs), Scale Sets, ya kisi bhi backend service par distribute karta hai.

Lekin, ye sirf traffic "baantta" nahi hai, balki ye bahut smartly decide karta hai ki kaunsi request kis server ke paas jani chahiye.

Jab koi user aapki website ka URL enter karta hai, toh request sabse pehle Application Gateway ke paas aati hai. Gateway ke peeche ek Backend Pool hota hai. Is pool mein aapki:
- Virtual Machines.
- Virtual Machine Scale Sets (VMSS).
- App Services (PaaS).
- Ya phir kisi on-premise server ka IP address ho sakta hai.

Application Gateway in different backends par smartly traffic ko distribute karta hai.

<br>

Azure Application Gateway essentially ek smart traffic controller + security guard + SSL terminator hai.

Ye teen main roles play karta hai:
- Load Balancer (Layer 7 aware).
- Reverse Proxy.
- Web Application Firewall (optional but powerful).

<br>
<br>

### Ye Layer-7 Azure Application Gateway ka kya matlab hai.

Networking mein hum **OSI Model** use karte hain jisme 7 layers hoti hain. OSI (Open Systems Interconnection) model ek conceptual framework hai jo ye samajhne mein madad karta hai ki ek computer se dusre computer tak data kaise travel karta hai. Ismein 7 layers hoti hain, aur har layer ka apna ek specific kaam hota hai.

OSI Model koi hardware nhi, balki rules hote hain. Jo batate hain, Jab ek computer se dusre computer tak data jata hai, toh wo in 7 steps (Layers) se guzarta hai.

Aur inhi layers mein se ek layer hoti hai **Layer-7**, jisko **Application Layer** bhi bolte hain.

**Azure Application Gateway** isi **Layer-7** yani **Application Layer** par kaam karta hai. Iska matlab hai ki Azure Application Gateway ke paas Layer-7 ka data pahunchta hai isliye Azure Application Gateway ko Layer-7 ya fir Application Layer load balancer kehte hain.

<br>

**Application Layer (Layer-7)**:

Application Layer OSI model ki sabse upar wali layer (Layer 7) hoti hai. Ye wo layer hai jisse hum (users) direct interact karte hain. Jab aap Chrome ya Safari mein koi website kholte hain, toh aap actually Application Layer ka use kar rahe hote hain.

To ye layer background mein kaafi saara "raw data" aur "instructions" generate karti hai taaki networking process shuru ho sake.

Jab aap browser mein koi URL type karke hit karte hain, toh browser ek HTTP Request Packet taiyar karta hai server ko bhejne ke liye. Ye HTTP request mein ye data hota hai:

- Request Line.
- Headers.
- Body (optional).

**Request Line**:

Yeh packet ka sabse pehla hissa hota hai. Isme 3 major cheezein hoti hain:
- Method: Browser batata hai ki wo kya karna chahta hai (e.g., ```GET``` page dekhne ke liye, ```POST``` data bhejne ke liye). Website se data lena hai ya data dena hai.
- Path/URI: Website ka kaunsa hissa chahiye (e.g., ```/index.html``` ya ```/login```).
- HTTP Version: HTTP protocol ka Kaunsa version use ho raha hai request bhejne ke loye(e.g., HTTP/1.1 ya HTTP/2).

Example: ```GET /profile HTTP/1.1```.

**HTTP Headers (Browser ki detail)**:

Yeh sabse bada aur important hissa hai. Headers mein browser bahut saari details "Key-Value" pairs mein pack karta hai. Ye browser ke baare mein extra information hoti hai:
- Host Header: Isme aapki website ka naam hota hai (Host: ```www.puneet-website.com```). Gateway isi ko dekh kar samajhta hai ki request kis website ke liye hai.
- User-Agent: Browser ki details (e.g., Mozilla/5.0, Chrome/120). Isse Gateway ko pata chalta hai ki request mobile se hai ya laptop se.
- Accept: Browser batata hai ki use kaisa data chahiye (e.g., text/html, image/webp).
- Cookie: Agar aapne pehle login kiya hai, toh browser Session ID bhejta hai. Gateway isse dekh kar aapko purane wale VM (Server) par hi bhejta hai (jise hum Sticky Session kehte hain).
- Authorization: Agar website password-protected hai, toh login credentials isi header mein jaate hain.
- Referer: Ye batata hai ki aap kis purani website se link click karke yahan aaye hain.

**Message Body (The Payload)**:

Ye packet ka last hissa hota hai. Isme aap website ko apna data bhej rahe hote hain. Toh browser us saare data ko Message Body mein daal deta hai. Application Gateway (agar usme WAF enabled hai) is body ko scan karta hai taaki koi hacker galat code (SQL Injection) na bhej raha ho.

Agar aap sirf website "open" kar rahe hain (GET request), toh ye body aksar khali (empty) hoti hai, Lekin agar aap:
- Koi form bhar rahe hain.
- File upload kar rahe hain.
- Login button daba rahe hain.

To ye HTTP request packet **Azure Application Gateway** ke paas pahunchti hai aur **Azure Application Gateway** is detail ko dekh pata hai.

<br>
<br>

**Ab complete end-to-end samjhiye ki kaise ek Http request server ke paas jati hai**:

Browser mein URL daal kar 'Enter' hit karna ek simple step lagta hai, lekin parde ke peeche (behind the scenes) ek pura networking protocol ka mela chalta hai.

Jab aap ```https://www.example.com/index.html``` likhte hain, to browser seedhe server se baat nahi kar sakta. Use pehle rasta dhoondna padta hai aur phir ek formal document (HTTP Request) taiyar karna padta hai.

Isko step-by-step detail mein samajhte hain:

**Step-1: URL Parsing (Structure Samajhna)**:

Sabse pehle browser aapke URL ko todta hai taaki wo samajh sake ki jaana kaha hai aur mangna kya hai.
- Protocol: ```https``` (Matlab data secure tarike se jayega).
- Domain: ```www.example.com``` (Ye server ka naam hai).
- Path: ```/index.html``` (Ye wo specific file hai jo aapko chahiye matlab browser ko chaiye jisko render karne se website dikhegi).

**Step-2: DNS Lookup (Address Dhoondna)**:

Internet par servers ko unke naam se nahi, balki IP Address se pehchana jata hai. Browser ko ab ```www.example.com``` ka IP address pata karna hoga.
- Browser IP ko pehle apne Cache mein dekhta hai.
- Agar wahan nahi mila, to wo OS se poochta hai.
- OS phir DNS Resolver (ISP) ke paas jata hai.
- Ant mein, browser ko ek IP address mil jata hai, jaise: ```93.184.216.34```.

**Step-3: TCP/IP Handshake (Connection Banana)**:

IP milne ke baad browser server ko ek TCP connection request bhejta hai. Isse TCP Three-Way Handshake kehte hain:
- SYN: Browser kehta hai, "Kya main connection start kar sakta hoon?".
- SYN-ACK: Server kehta hai, "Haan, main ready hoon.".
- ACK: Browser kehta hai, "Theek hai, main request bhej raha hoon.".

**Step-4: HTTP Request Create Karna (The Main Part)**:

Ab browser ek text-based message likhta hai jise HTTP Request kehte hain. Iske teen main parts hote hain:
- Request Line:

  Isme teen cheezein hoti hain:
  - Method: ```GET``` (Kyuki hume data mangwana hai).
  - Path: ```/index.html```.
  - Version: ```HTTP/1.1``` ya ```HTTP/2```.

- Request Headers:

  Ye browser ke baare mein extra information hoti hai:
  - Host: ```www.example.com```.
  - User-Agent: Aapka browser kaunsa hai (Chrome, Safari, etc.).
  - Accept: Browser kis type ki file handle kar sakta hai (text/html).
  - Cookie: Agar aapne pehle visit kiya hai, to purani identity details.
 
- Request Body:

  GET request mein body aksar khali hoti hai. Lekin agar aap koi form bhar rahe hote, to wo data yahan hota.

Example of a Real HTTP Request:

Jab aap enter marte hain, to parde ke peeche ye text message server ko bheja jata hai, isi ko http request kehte hain:

```
GET /index.html HTTP/1.1
Host: www.example.com
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64)
Accept: text/html,application/xhtml+xml
Accept-Language: en-US,en;q=0.9
Connection: keep-alive
```

**Request Ka Safar (OSI Model Application)**:

Browser is request ko Application Layer par banata hai. Aur ye hi request Azure Application Gateway ko pass pahuncti hai, isi information ko Application Gateway dekh sakta hai Layer-7 par. Isliye Azure Application Gateway ko Layer-7 load balancer kehte hain.

<br>
<br>

### Jab Load Balancer tha to Azure Application Gateway kyu use kiya gaya?

Load balancer ek Layer-4 service hai, jo multiple vms ya backend servers par distribute karti hai, Jab user ki request load balancer ke paas aati hai to load balancer us request mein se OSI Model ke Layer-4 ki details hi dekh pata hai, jaise:
- Source IP.
- Source Port.
- Destination IP.
- Destination Port.
- Protocol (TCP/UDP).

To load balancer sirf inhi details ko dekh pata hai ek request mein. To in request ki ek 5-tuple hash banakar (```matlab uper list mein likhi gayi 5 details ko combine karke ek hash function ko deta hai aur hash function ek output deta hai, us output se ek backend server select karta hai traffic waha bhejne ke liye```) ek backend server par us request ko behj deta hai.

Ye simple kaam hota hai load balancer ka. Agar ek saath jyada requests aaye to un requests ko efficiently backend server par distribute karna jisse ek server overload na ho.

Ye kaam hota hai load balancer ka.

<br>

Lekin dheere dheere application bohot advance hoti gyi, Chizo ko ek server par na rakhkar alag alag servers par rakha jaane laga, jaise, videos ke liye alag server, alag database server, backend server alag ho gye, frontend server alag ho gye, to in sabhi server ko milakar ek application chalne lagi.

Example:

Maine ek project pe kaam kiya tha jiska naam tha ```Schrack For Students```. Ye project engineering students ke liye ek website aur ek andriod application provide karta tha.

To is application ke multiple server the jaise, frontend react pe chal rha tha to uske liye alag server, backend java mein tha to uske liye alag server, cms (content management service) ke liye alag server, aur couchbase database ke liye alag server. Iska andriod application alag chal rha tha. 

To suppose android application ko database ya content access karna hai to vo inhi servers par access karega.

To inke frontend mein azure par ek azure application gateway hosted the jiska ek domain name tha ```schrackforstudents.com``` aur sabke liye routing rules banaye hue the, jaise ```/cms```, ```/couchbase```, ```/backend``` is tarike se. To agar internally agar andriod app couchbase ya backend use karna chahe to uski request application gateway se hoke couchbase pe chali jaye.

<br>

To is tarike se complex application banane lagi. To in application ke traffic ko route karne ke liye Azure Application Gateway ka use kiya gaya.

Load balancer sirf layer-4 ke data jaise, Source IP, Source Port, Destiantion IP, Destination Port aur Protocol ko dekh ke traffic ki routing karta hai. Ye sirf IP address aur Port number (TCP/UDP) dekhta hai. Isse ye matlab nahi ki packet ke andar kya data hai.

Lekin Azure Application Gateway layer-7 ke data ke ander URL, Hostname aur headers ko dekh ke traffic ki routing karta hai. Jab ek http request application gateway ke paas aati hai to application gateway us request ke ander ka sara data dekh sakta hai, Jaise, URL, Hostname, Header, sab chiz. Isi data ko dekh kar routing rules ke hisaab se application gateway traffic ko sahi backend server pe behjta hai.

Application Gateway packet ke andar ka HTTP/HTTPS data padh sakta hai. Ye dekh sakta hai ki URL kya hai, cookies kya hain, aur header mein kya likha hai. Isi data ko dekh kar ye traffic ki routing karta hai.

Ye hi difference hota hai load balancer aur application gateway.

<br>

**Problem Without Application Gateway**:

Assume karo tumhare paas ek production web system hai:
- Multiple backend servers.
- HTTPS required.
- Microservices / APIs.
- Security threats (bots, injections).
- Scaling needs.

Agar Application Gateway na ho:
- ❌ Har backend ko public expose karna padega.
- ❌ Certificates har server pe manage karne padenge.
- ❌ No smart routing.
- ❌ No central security inspection.
- ❌ Difficult scaling & failover

System fragile ho jata hai.

Normal Load Balancer decision leta:
- IP + Port.
- URL + Path + Host + Headers.

**Example Without Gateway**:

Separate sub domains required:
- api.contoso.com.
- images.contoso.com.
- app.contoso.com.

**Example With Gateway**:

Single domain possible:
- contoso.com/api.
- contoso.com/images.
- contoso.com/app.

Gateway request inspect karke route karta.

Ye microservices & APIs ke liye extremely important hai.


<br>
<br>

### Azure Application Gateway Kaam Kaise karta Hai?

Azure Application Gateway ek Layer 7 (Application Layer) Load Balancer hai.

Matlab:
- Ye HTTP / HTTPS traffic ko understand karta hai.
- URL, Hostname, Headers ke basis pe routing karta hai.
- SSL terminate kar sakta hai.
- Web Application Firewall (WAF) provide karta hai.
- Autoscale hota hai.

Layer 4 Load Balancer (TCP/UDP based) sirf port aur IP dekhta hai.

Lekin Application Gateway:
```
https://example.com/api/users
https://example.com/images/logo.png
```
Ye dono ko alag backend pe bhej sakta hai.

<br>

**High Level Working Flow**:

Chalo ek simple real example lete hain:

Tumhari company ki website hai:
```
www.mycompany.com
```

Aur backend architecture kuch aisa hai:
- ```/api/*``` → API Server (VMSS).
- ```/images/*``` → Storage Server.
- Baaki sab → Main Web App.

Ab dekhte hain request ka journey.

<br>

**Step-by-Step Request Flow (Internal Working)**

**Step 1: DNS Resolution**:

User browser me type karta hai:
```
https://www.mycompany.com
```

Broeser DNS resolve karta hai:
```
www.mycompany.com → Public IP of Application Gateway
```

Important: Direct backend IP expose nahi hota.

<br>

**Step 2: Request Hits Public IP**:

Request aata hai:
```
Client → Internet → Public IP → Application Gateway
```
Yahan se actual processing start hoti hai.

<br>

**Step 3: Listener Trigger Hota Hai**:

Application Gateway me hota hai: ```Listener```.

Listener ek process hoti hai jo incoming traffic ko "check" karti hai. Ye request mein teen cheezein monitor karta hai:
- Protocol: (HTTP ya HTTPS).
- Port: (80, 443, ya koi custom port).
- Host Name / IP Address: (e.g., ```www.simplyexplains.com```).

Jab koi user aapki website ka URL browser mein dalta hai, toh wo request Application Gateway ke Public IP par jati hai. Wahan baitha Listener dekhta hai ki: "Kya ye request wahi protocol aur port use kar rahi hai jo mujhe allow karne ko bola gaya hai?".

Jab traffic aata hai, Listener ye 3 chize dekhta hai:
- IP Address aur Hostname Check (Gateway ka wo address jahan request hit karegi).
- Port Check: 80 or 443 (Agar user ```http://``` use kar raha hai, toh Port 80, Agar user ```https://``` (secure) use kar raha hai, toh Port 443.).
- Protocol Check: HTTP or HTTPS/SSL.

Agar ye teeno match ho jate hain, toh Listener us request ko pakad kar "Routing Rule" ko de deta hai. Rule phir decide karta hai ki isse kis Backend Pool (Server) par bhejna hai.

Types of Listeners:
- Basic Listener: Ye sirf ek single domain ko listen karta hai.

  Example: Example: Agar aapki sirf ek hi website hai ```app.com```, toh aap Basic listener use karoge jo port 80/443 par dhyaan dega.

- Multi-site Listener: Ye tab use hota hai jab aap ek hi Application Gateway par multiple websites chalana chahte ho.

  Example: Ek hi gateway par ```site1.com``` bhi chal rahi hai aur ```site2.com``` bhi. Listener host header dekh kar pehchan lega ki request kis site ke liye aayi hai.

<br>

Ek Real-Life Example se Samajhte Hain:

Maano aapne ek App Gateway set kiya hai apni website ke liye.

Scenario:
- Aap chahte ho ki jab koi ```https://www.mycompany.com``` khole, toh wo aapke web servers tak pahunche.

Listener ki Configuration:
- Name: MyWebsiteListener.
- Frontend IP: Public IP of Gateway.
- Port: 443.
- Protocol: HTTPS.
- Certificate: (Kyunki HTTPS hai, toh SSL certificate yahan upload hoga).
- Host Name: https://www.mycompany.com.

Process:
- User Request: User ne type kiya ```https://www.mycompany.com```.
- Listener Action: Listener ne dekha ki request Port 443 par aayi hai aur Hostname https://www.google.com/url?sa=E&source=gmail&q=mycompany.com hai.
- SSL Handshake: Kyunki ye HTTPS listener hai, toh yahi par SSL Termination hoga (certificate check hoga).
  - Agar HTTPS request hai:
    - TLS handshake hota hai.
    - Certificate validate hota hai.
    - Traffic decrypt hota hai.
  - Ye backend ko traffic plain http mein bhejta hai.
  - Isi ko SSL Termination kehte hain.
- Forwarding: Sab sahi raha, toh Listener ne traffic Routing Rule ko pass kar diya, jisne aage Backend Server ko bhej diya.

<br>

**Step 4: Ab Sabse Important Part – Routing Rules**:

Jab Listener ne request accept kar li aur check kar liya ki port aur protocol sahi hai, tab wo request ko Routing Rule ke haath mein de deta hai. Routing Rule ka kaam hai ye decide karna: "Ye request ab konse backend server pe jayegi?"

Routing Rule ek aisi "Condition" hai jo do cheezon ko aapas mein jodti hai:
- Source (Listener): Jahan se request aayi.
- Destination (Backend Pool / HTTP Settings): Jahan request ko bhejna hai.

Bina Routing Rule ke, Listener ko ye nahi pata hoga ki request ko Backend Pool (servers) tak kaise pahunchana hai.

<br>

Routing Rule Kaise Kaam Karta Hai?

Routing Rule do main types ke hote hain, jo define karte hain ki traffic ka "route" kya hoga:
- Basic Routing Rule:
  - Ye sabse simple hai. Ismein aap bolte ho: "Jo bhi traffic is Listener par aaye, use seedha is Backend Pool mein bhej do." Ismein koi filter nahi hota.
  - Example: Agar koi ```www.example.com``` par aaye, toh use ```Web-Server-Pool``` par bhej do.
 
- Path-based Routing Rule (Advanced):
  - Ye Application Gateway ki asli taqat hai. Ismein aap URL ke "Path" ko dekh kar traffic ko alag-alag raste par bhej sakte ho.
  - Example:
    - Agar URL hai ```example.com/images/*``` → Toh traffic jaye Storage Server par.
    - Agar URL hai ```example.com/videos/*``` → Toh traffic jaye Media Server par.
    - Baqi sab (Default) → Jaye General Web Server par.

<br>

Routing Rule Ke 3 Main Components:

Jab aap ek Rule banate ho, toh ye 3 cheezein configure karni hoti hain:
- Listener: Wo listener select karo jisse traffic uthana hai.
- Backend Target (Pool): Wo servers ka group jahan traffic jayega (VMs, App Services, etc.).
- HTTP Settings: Ye batata hai ki traffic backend tak kaise jayega.
  - Kya traffic ko Port 80 pe bhejna hai ya 443 pe?
  - Kya Cookie-based affinity (session) on karni hai?
  - Backend server ko check karne ka Request Timeout kitna hoga?

<br>
 
Real-Life Example: Ek Streaming App

Maano aapka ek platform hai "Simply Stream". Aapne Application Gateway par ek Routing Rule banaya hai:

Scenario:
- Aapke paas do backend pools hain: Static-Pool (for images/CSS) aur Video-Pool (for movies).

Rule Configuration (Path-based):
- Listener: Jo ```https://simplystream.com``` ko sun raha hai.
- Path Map:
  - Agar path ```/static/*``` hai → Target: Static-Pool.
  - Agar path ```/watch/*``` hai → Target: Video-Pool.
  - Default Rule: Agar koi sirf home page par hai (```/```), toh use Main-Website-Pool par bhej do.

```
Backend Pool:
10.0.1.4 - Static
10.0.1.5 - Watch
10.0.1.6 - Main Website
```
Application gateway in teeno mein load balancer karega.
 
Example:
- Jab koi user movie dekhta hai (```simplystream.com/watch/movie123```), toh Routing Rule use turant Video-Pool wale high-capacity servers par bhej deta hai.
- Isse aapka main website server load se bach jata hai.

Ek aur Example:

Suppose:
```
/api/* → API Backend
/images/* → Image Backend
/admin/* → Admin Backend
/* → Default Backend
```

Application Gateway request ka URL dekhta hai:
```
https://www.mycompany.com/api/users
```

Wo check karega:
```
Match: /api/*
```

Aur request API backend pe bhej dega.

<br>

**Step 5: Health Probes – Backend Healthy Hai Ya Nahi?**

Backend par request bhejne se pehle health probes backend server ki health check karte hain.

Application Gateway continuously check karta hai:
```
http://10.0.1.4/health
```

Agar:
- 200 OK → Healthy.
- 500 error → Unhealthy.

Agar VM unhealthy ho jaye: ❌ Usko traffic nahi milega.

Yeh automatic hota hai.

Ab user ki request backend server jaha application chal rha waha pahunch chuki hai.

<br>
<br>

### Internal Flow Diagram (Logical)

Flow internally kuch aisa hota hai:
```
Client
   ↓
Public IP
   ↓
Listener (HTTPS 443)
   ↓
SSL Termination
   ↓
Routing Rule
   ↓
Path Matching
   ↓
Backend Pool Selection
   ↓
Health Check Verify
   ↓
Backend VM
```

<br>
<br>

**Ab WAF Ka Role (Agar tumne WAF enable kiya hai)**

WAF ek security rule hai jo incoming request ko scan karta hai. Ye routing se pehle kaam karta hai.

Standard Firewall (jo port aur IP block karta hai) aur WAF mein bahut farak hota hai. WAF specifically HTTP/HTTPS traffic ko scan karta hai. Ye packet ke andar ka data padhta hai aur dekhta hai ki kahin koi hacker aapki website ko nuksan pahunchane ki koshish toh nahi kar raha.

Azure mein WAF, Application Gateway ke upar ek extra layer ki tarah kaam karta hai. Ye OWASP (Open Web Application Security Project) ke core rules par chalta hai, jo duniya bhar ke top cyber attacks ko pehchante hain.

WAF Kaise Kaam Karta Hai? (The Scanning Process):

Jab koi request aapki website par aati hai, toh Backend Server tak pahunchne se pehle wo WAF se guzarti hai. WAF teen cheezein karta hai:
- Inspection: Ye request ke headers, cookies, aur query strings ko scan karta hai.
- Matching: Ye dekhta hai ki kya request ka pattern kisi "Hacker Attack" se milta-julta hai (jaise SQL Injection).
- Action: Agar request saaf hai, toh use aage bhej deta hai. Agar suspicious hai, toh use Block kar deta hai.

WAF kin Khatron (Attacks) se bachata hai? (Examples):

1 - SQL Injection (SQLi):

Hacker aapki website ke login box mein username ki jagah ek SQL query daal deta hai: ' OR 1=1 --. Iska maqsad aapke database se password chori karna hota hai.
- WAF Action: WAF dekhta hai ki URL ya form mein SQL commands hain, wo turant request ko drop kar deta hai.

2 - Cross-Site Scripting (XSS):

Hacker aapke comment section mein ek script daal deta hai: ```<script>alert('Hacked')</script>```. Jab koi aur user wo page kholta hai, toh unka browser wo script run kar deta hai.
- WAF Action: WAF script tags (<script>) ko pehchan leta hai aur block kar deta hai.

3 - Bot Protection:

Kayi baar hackers "Bots" ka use karte hain aapki site se data chori karne ya site ko slow karne ke liye.
- WAF Action: WAF pehchan leta hai ki ye request insaan ki nahi, machine ki hai, aur use block kar sakta hai.

<br>
<br>

### Real Production Example (DevOps Perspective)

Suppose tum ek E-commerce site deploy karte ho:

Architecture:
- Frontend → VMSS.
- API → AKS.
- Admin → App Service.
- Images → Blob Storage.

Application Gateway karta hai:
```
/ → VMSS
/api/* → AKS
/admin/* → App Service
/images/* → Blob
```

Aur saath me:
- WAF.
- Autoscaling.
- SSL.
- Health monitoring.



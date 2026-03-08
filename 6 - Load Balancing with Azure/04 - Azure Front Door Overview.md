# Azure Front Door Overview

Azure Front Door ek global load balancing service hai jo multiple regions mein hosted application ke beech load ko balance karti hai.

Azure Front Door ek global entry point hai jo duniya ke kisi bhi user ko nearest Azure edge location se connect karta hai, aur unki request ko best backend tak intelligently route karta hai.

<br>
<br>

### Sabse Pehle Samjho Load Balancing Kya Hoti Hai

Load balancing ek aisi technique hai jo incoming network traffic ko multiple servers ke beech mein barabari se baant deti hai.

Jab koi website ya application popular ho jati hai, to ek akela server saara traffic handle nahi kar paata. Incoming request ke load ko handle karne ke liye hum application ko multiple web server par host karte hain aur unke front mein ek load balancing service lagi hoti hai jo traffic ko servers par aadha aadha behjti hai jisse ek web server par load na aaye.

To uper humne dekha ki load balancing kya hoti hai, Ab dekhte hain ki load balancing kitne type ki hoti hai:

<br>

**Load Balancing ke Types**:

Load balancing do type ki hoti hai:
- Regional Load Balancing.
- Global Load Balancing.

<br>

**Regional Load Balancing (Local Level)**:

Regional load balancing ka matlab hai ki aapka load balancer aur aapke servers (VMs) ek hi Azure Region (jaise Central India) ke andar bane hue hain. Aur load balancer unhi VMs par load ko distribute kar rha hai.

To Azure Regional Load Balancing ke liye **Load Balancer** aur **Azure Application Gateway** ye do service provide karta hai.

Ab Samjho:
- Azure Load Balancer aur Application Gateway ek hi region mein kyu kaam karte hain aur different regions ke VMs ko directly load balance kyu nahi kar sakte?

Answer:
- Azure Load Balancer aur Application Gateway "Regional Services" hain kyunki wo ek specific Virtual Network (VNet) ke andar deploy hote hain. Ek VNet by default ek hi region tak limited hota hai.
- Kyunki ye devices VNet ke private IP addresses ke sath interact karte hain, ye us boundary se bahar ke servers (jo dusre region mein hain) ko directly nahi dekh sakte.
- Jab aap ek VNet banate hain, to wo ek specific region (jaise Central India) tak hi limited hota hai.
- Load Balancer ko un VMs ka Private IP chahiye hota hai jin par wo traffic bhej sake. Ek Regional Load Balancer sirf usi VNet ke VMs ko "dekh" sakta hai, jis VNet mein vo load balancer aur application gateway deploy hain.

Maan lijiye Microsoft aapko allow kar bhi de ki aap Central India ke Load Balancer se East US ki VM connect kar dein, to kya hoga?
- Request pehle Central India ke Load Balancer par aayegi.
- Phir wo Load Balancer request ko East US bhejega (samundar ke niche wali cables ke zariye).
- US ka server respond karega wapas India ko.
- India ka Load Balancer phir user ko dikhayega.

Is process mein itni Latency (delay) aa jayegi ki user ko website bohot slow lagegi. Isliye, standard Load Balancer ko design hi aisa kiya gaya hai ki wo "Local" traffic ko handle kare taaki speed bani rahe.

Note:
- Regional Load Balancing Solution jaise Load Balancer aur Azure Application Gateway, High Availability to provide karte hain lekin Disaster recovery provide nahi karte.

Inke saath ek problem hai:
- Problem: Agar poora Central India region hi down ho jaye (due to earthquake or power failure), to ye regional load balancer bhi down ho jayega.

<br>

**Global Load Balancing**:

Global Load Balancing (GLB) ek aisi technique hai jisme aane waale internet traffic ko duniya bhar mein faile hue multiple regions mein data centers ya servers par distribute kiya jata hai.

Iska main maqsad ye hota hai ki user ko sabse fast response mile aur agar ek poora regions (jaise Mumbai) down ho jaye, toh traffic apne aap doosre region (jaise Singapore) par shift ho jaye.

Azure Global Load Balancing ke liye do services provide karta hai:
- Azure Front Door.
- Traffic Manager.

<br>
<br>

### Ab Samjho Azure Front Door Kya Hota Hai:

Azure Front Door ek Modern Cloud Content Delivery Network (CDN) aur Global Load Balancer hai. Ye Layer 7 (HTTP/HTTPS layer) par kaam karta hai.

Iska sabse bada fayda ye hai ki ye Microsoft ke Global Edge Network ka istemal karta hai. Iska matlab hai ki jab user aapki website access karta hai, toh wo seedhe internet ke bheed-bhad wale raste se nahi jata, balki apne kareebi Microsoft "Edge POP" (Point of Presence) mein ghustaa hai aur wahan se Microsoft ki apni fast fiber cables ke zariye server tak pahunchta hai.

<br>

**Ye Kaise Kaam Karta Hai? (The "Split TCP" Magic)**:

Maano aapka server USA mein hai aur user India mein:
- Normal Internet: User ki request hazaaron public routers se hote huye USA jayegi. Isme bahut "Latency" (delay) hota hai.
- Azure Front Door: User ki request India ke hi kisi kareebi Microsoft Edge node (jaise Mumbai ya Chennai) par "terminate" ho jati hai. Wahan se Microsoft ka private network us request ko rocket ki speed se USA server tak le jata hai. Is technique ko Anycast kehte hain.

<br>
<br>

### Azure Front Door ko detail mein samjhne se pehle, Microsoft ka private global fiber network samjho

<br>

**Sabse pehle samjho: Internet normally kaise kaam karta hai**:

Internet simple ek data ka exchange hi hai.

Jab koi user browser mein website open karta hai, Data is path pe jata hai:
```
User → ISP → Internet routers → Multiple networks → Data center
```

Example:
```
User (Delhi)
   ↓
Local ISP (Jio / Airtel)
   ↓
Internet Exchange
   ↓
Multiple ISPs
   ↓
Destination server
```

Yahan problems hoti hain:
- Latency:
  - Jab traffic multiple networks se pass karta hai to data ko end server tak pahuchne mein time lagta hai. Jisko latency bolte hain.
- Packet loss:
  - Beech mein kahi bhi packet loss bhi ho sakta hai.
- Slow routing:
  - Internet best routing choose nahi karta.
- Public internet unstable hota hai:
  - Isliye large cloud providers apna private network banate hain.
 
Aur Microsoft ne bhi apna ek private network bana rakha hai.

<br>

**Microsoft Global Network kya hai**:

Microsoft ne poori duniya mein khud ki **private fiber optic cables** bichai hui hain.

Isko kehte hain:
- **Microsoft Global Network Backbone**.

Duniya bhar mein jo normal internet chalta hai, wo alag-alag ISPs (Airtel, Jio, AT&T) ke beech data exchange (peering) se chalta hai. Isme data ko bahut saare "hops" matlab routers lene padte hain, jisse latency badhti hai aur security kam hoti hai.

Microsoft ne iska solution nikaala: Unhone samundar ke neeche (Submarine cables) aur zameen ke niche apni khud ki Fiber Optic lines bicha rakhi hain.
- Lakhon miles ki fiber cables.
- Kyunki ye unka apna private network hai, wo decide karte hain ki data kaise move hoga.
- Ye network terabits per second (Tbps) ki speed handle kar sakta hai. Matlab ek tarah se light ki speed se data transfer hota hai.

Ye basically Microsoft ka worldwide private backbone infrastructure hai jiske through Azure services ka traffic internet par random routes se nahi balki Microsoft ke khud ke high-speed fiber network par travel karta hai.

Is private netork ye chize hoti hain:
- Undersea fiber cables.
- Land fiber cables.
- Global datacenter connectivity.
- Edge POP locations.

Iska kaam:
```
Azure Regions ko connect karna
+
Edge locations ko connect karna
+
Traffic ko fastest path se route karna
```

Matlab:
- Public internet se ek baar traffic Microsoft network mein enter ho gaya → phir wo Microsoft ke private fiber network par travel karta hai.

<br>

**Edge Locations Kya Hain?**

Edge location jisko (POP — Point of Presence) bhi kehte hain.
- Ye microsoft ka ek mini data center hota hai jo duniya bhar ke bade cities mein bane hue hain hain. In mini datacenter ke ander **Caching servers**, **Security firewalls (WAF)**, aur **Smart Routers** hote hain.
- Edge location ka kaam simply user ko microsoft ke private network mein enter karwana. Iska matlab hai ki user ki request uske nearest edge-location par jati hai fir edge location se microsft ke private network mein chali jati hai.
- Aaj ki date mein Microsoft ke paas 190+ Edge Locations hain jo 170 se zyada countries mein faili hui hain.
- Inka kaam "Azure Region" (jaise Central India - Pune) banna nahi hai, balki internet users aur Azure regions ke beech ek bridge banna hai.
- Azure Region mein aapki VMs aur databases hoti hain. Edge Location mein sirf Caching servers, Security firewalls (WAF), aur Smart Routers hote hain.

<br>

Edge Locations ka asli kaam isi latency ko khatam karna aur user experience ko "fast" banana hai. Inke 3 mukhya kaam hote hain:

Static Content Caching (Speed Up):
- Problem: Agar har baar user ko website ki images, videos, ya CSS files US se mangwani pade, toh site slow load hogi.
- Solution: Edge Location in files ki ek copy apne paas save (cache) kar leti hai. Jab agla user wahi cheez mangta hai, toh Edge location usey wahan se hi pakda deti hai, US tak jaane ki zarurat hi nahi padti.

Traffic Routing & Acceleration (Front Door):

Sirf static files hi nahi, balki dynamic data (jaise login requests) ko bhi Edge locations fast karti hain.
- SSL Offloading: Encryption/Decryption ka heavy kaam Edge par hi ho jata hai, jisse main server (Region) par load kam padta hai.
- TCP Optimization: Edge location user ke saath connection jaldi setup karti hai (TCP handshake), jisse user ko "lag" mehsoos nahi hota.
- Iske liye Azure Front Door ka use hota hai.

Security:
- DDoS Protection: Agar koi attacker aapki site par fake traffic bhejta hai, toh Azure usey Edge par hi block kar deta hai, taaki aapka main Azure Region (jahan database hai) safe rahe.
- WAF (Web Application Firewall): Hacking attempts ko border (Edge) par hi rok diya jata hai.

<br>

Azure ke regions aur Egde locations dono alag alag chize hain, ab in dono ke beech difference samjho:

Azure Regions:
- Ek Azure Region ek geographical area hota hai jisme kayi saare Data Centers hote hain jo aapas mein high-speed network se jude hote hain.
- Inka kaam hai aapki applications ko host karna, heavy computing power dena (Virtual Machines), aur data store karna (Databases).
- Ye bahut bade hote hain. Har region mein hazaron servers hote hain.
- Jab aap koi VM ya SQL Database banate hain, toh aap ek specific Region (jaise Central India ya East US) select karte hain.
- Regions ko is tarah design kiya jata hai ki wo High Availability aur Disaster Recovery dein.
- Ek region ke andar 3 ya usse zyada alag-alag data centers hote hain jinhe Availability Zones kehte hain. Har zone ki apni power, cooling, aur networking hoti hai. Agar ek building mein aag lag jaye, toh dusri building (Zone) se aapka kaam chalta rahega.

Edge Locations:
- Edge Locations (jinhe Azure Points of Presence ya PoPs bhi kehta hai) wo jagah hain jahan Azure ka network internet service providers (ISPs) ke sath connect hota hai.
- Edge location ka main kaam "Peering" hai. Jab aap apne ghar ke internet se Azure access karte hain, toh aapka data internet provider se nikal kar sabse pehle Edge Location par Microsoft ke "Global Network" mein enter karta hai.
- Ek baar data Edge par pahunch gaya, toh wo public internet se hat kar Microsoft ki apni private fiber-optic cables (Jo samundar ke niche se jati hain) par travel karta hai.
- Edge locations (PoPs) aksar Microsoft ke apne data centers mein nahi, balki Shared Facilities (jaise Equinix ya Global Switch) mein hote hain jahan saare bade Internet Service Providers (Jio, Airtel, AT&T) aapas mein connect hote hain.
- Inka kaam computing nahi, balki Content Delivery aur Latency kam karna hai.
- Ye regions ke muqabale bahut chote hote hain, aksar sirf kuch racks hote hain jo third-party data centers mein lage hote hain.

Workload aur Services:

In dono par chalne wali services mein zameen-aasman ka farq hai:
| Feature         | Azure Region                                           | Edge Location (CDN/Front Door)                               |
|-----------------|--------------------------------------------------------|--------------------------------------------------------------|
| Main Services   | VM, Kubernetes (AKS), SQL DB, Storage Accounts.        | Azure CDN, Azure Front Door, WAF (Web Application Firewall). |
| Data Processing | Heavy processing aur complex logic yahan run hota hai. | Sirf request routing aur caching hoti hai.                   |
| Storage         | Permanent data storage (Terabytes/Petabytes mein).     | Temporary caching (taki baar-baar region tak na jana pade).  |

<br>
<br>
<br>

### Microsoft par Jab aap Front Door Service create karte ho to Backend par kya kya hota hai

<br>

**Sabse Pehla Step — Azure Control Plane Request**:

Jab tum Azure Portal / CLI / Terraform se Azure Front Door create karte ho, to tum actually Azure Control Plane API ko call kar rahe hote ho.

Example:

Tum portal mein jaake create karte ho:
```
Create Resource
→ Azure Front Door
→ Backend pool
→ Routing rule
→ Domain
```

Jab tum Create button press karte ho to backend mein:
- Request Azure Resource Manager (ARM) ko jati hai.
- ARM request ko validate karta hai.
- Configuration store karta hai.

Example configuration:
```
Frontend Domain
example.com

Backend Pool
vm1-eastus
vm2-westus

Routing Rule
/* → backend pool
```

ARM isko store karta hai Azure Resource Provider (Microsoft.Cdn) mein.

Iska matlab:
```
Azure Control Plane
       │
       ▼
Azure Resource Manager
       │
       ▼
Front Door Resource Provider
```

Abhi tak traffic handling start nahi hui.

<br>

**Global Edge Configuration Propagation**

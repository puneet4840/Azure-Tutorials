# Azure Load Balancer Overview

Azure Load Balancer ek Layer-4 (Transport Layer) ki service hai jo incoming network traffic ko multiple virtual machines ya backend resource ke beech mein distribute karti hai.

Ye ek Azure ki service hai jo incoming network traffic ko multiple backend servers par distribute karta hai.

<br>
<br>

### KYU ZAROORI HOTA HAI Azure Load Balancer?

Traffic load ko evenly distribute karne ke liye hota hai Load Balancer.

Socho agar:
- Tumhari ek website hai jo sirf 1 VM par hi chal rahi hai.
- Aur ek din tumhari website par traffic jyada aa gya, to jyada traffic aane ki wajah se VM load ko handle nhi kar payega aur server crash ho jayega, to apki aapki application down ho jayegi.
- Ya fir VM kisi bhi reason se crash ho gyi ya fir maintenance chal rahi hai.
- To application down ho jayegi.

Isliye application ko multiple VMs par deploy kiya jata hai aur in VMs ke front mein load balancer service deploy hoti hai jo incoming network traffic matlab requests ko in VMs par distribute karti hai.

<br>

**REAL LIFE EXAMPLE**:

Example: Online Shopping Website 🛒

Tumhari website:
- Diwali sale pe.
- 1 lakh users ek saath open kar rahe hain.

Backend mein:
- VM-1.
- VM-2.
- VM-3.

Ab agar:
- Saare users VM-1 pe aa gaye ❌.
- VM-1 overload ho jaayegi ❌.

Azure Load Balancer:
- Traffic ko evenly distribute karega.
- Har VM ko equal ya required load dega.

<br>
<br>

### Azure Load Balancer KAAM KAISE KARTA HAI?

Step-by-Step Flow:
- Client (User) request bhejta hai.
- Request aati hai Load Balancer ke Frontend IP pe.
- Load Balancer mein ek backend pool bana hua rehta hai, is backend pool ka matlab hai VMs ka group, vo VMs jinpar load aayega.
- To load balancer ke backend mein VMs running hote hain. User ko sirf Load balancer ka public IP dikhta hai, jisko user browser mein hit karta hai.
- Load Balancer:
  - Har VM ki health check karta hai.
  - Kaun-si VM healthy hai.
- Fir Load Balancing rule se VM select karta hai request bhejne ke liye fir request bhejta hai:
  - VM-1 ya VM-2 ya VM-3.

Agar koi VM unhealthy hai → usko traffic hi nahi milega.

<br>
<br>

### Ye Layer-4 Load Balancer ka kya matlab hai?

Networking mein hum **OSI Model** use karte hain jisme 7 layers hoti hain. OSI (Open Systems Interconnection) model ek conceptual framework hai jo ye samajhne mein madad karta hai ki ek computer se dusre computer tak data kaise travel karta hai. Ismein 7 layers hoti hain, aur har layer ka apna ek specific kaam hota hai.

OSI Model koi hardware nhi, balki rules hote hain. Jo batate hain, Jab ek computer se dusre computer tak data jata hai, toh wo in 7 steps (Layers) se guzarta hai.

<br>

**Application Layer (Layer 7)**:
- Ye wo layer hai jisse hum (users) direct interact karte hain.
- Kaam: User ko network services provide karna.
- Example: Aapne browser khola aur Amazon ki website pe "Order" button dabaya. Aapka action Application layer se start hua.

**Presentation Layer (Layer 6)**:
- Is layer ka kaam data ko "readable" banana hai.
- Kaam: Data compression, Encryption (security), aur translation (jaise EBCDIC se ASCII).
- Example: Aapki payment details ko encrypt kiya jata hai taaki koi beech mein na padh sake. Laptop ki details ko ek standard format (jaise JSON ya XML) mein convert kiya jata hai.

**Session Layer (Layer 5)**:
- Ye do computers ke beech "connection" banati aur khatam karti hai.
- Kaam: Ye Session Start, Manage, aur Terminate karti hai.
- Example: Amazon ke server aur aapke computer ke beech ek connection banta hai. Agar payment ke waqt net kat jaye, to ye layer track rakhti hai ki process kahan ruka tha.

**Transport Layer (Layer 4)**:
- Iska main kaam hai end-to-end communication aur reliability.
- Kaam: Data ko segments mein divide karna aur ye check karna ki data sahi se pahuncha ya nahi (Error recovery).
- Example: Laptop ko ek bade box mein pack kiya jata hai. Agar box bada hai, to uske 2-3 parts kiye jate hain aur har part pe "Sequence Number" dala jata hai taaki wahan pahunch kar wapas sahi se jud sake.

**Network Layer (Layer 3)**:
- Ye layer decide karti hai ki data kis raste (path) se jayega.
- Kaam: IP Address ka use karke routing karna. Data ko yahan "Packets" kaha jata hai.
- Example: Is layer pe aapka "Address" (IP Address) likha jata hai. Router decide karta hai ki parcel kis raste (Air, Road, ya Train) se jayega.

**Data Link Layer (Layer 2)**:
- Ye layer physical layer ke upar hoti hai aur error-free transmission ensure karti hai.
- Kaam: Data ko "Frames" mein todna aur MAC Address ka use karke sahi device tak pahunchana.
- Example: Jab parcel aapke shehar ke warehouse mein pahunchta hai, to local delivery boy aapke "Ghar ke Number" (Physical Address/MAC) ko dekhta hai.

**Physical Layer (Layer 1)**:
- Ye sabse niche ki layer hai jo hardware se judi hoti hai.
- Kaam: Data ko electrical signals, light pulses, ya radio waves (bits - 0s and 1s) mein badal kar wire ya wireless medium se bhejna.
- Example: Ye wo asli sadak ya truck hai jispe parcel physically move kar raha hai.

<br>
<br>

**Ek aur example se samjho**:

Jab aap apne browser (client) mein www.google.com likhte hain aur 'Enter' dabate hain, toh OSI model ki har layer apna-apna role play karti hai, Dekho Kaise:

Step 1: Application Layer (L7):
- Aapne browser mein URL dala aur enter hit kiya. Browser ne ek HTTP/HTTPS Request generate ki.
- Hota kya hai: Browser Google ke server se kehta hai, "Mujhe apna Home Page chahiye."

Step 2: Presentation Layer (L6):
- Browser ensure karta hai ki data sahi format mein ho.
- Hota kya hai: Agar aap koi login detail bhej rahe hain, toh wo Encrypt hoti hai (HTTPS/SSL). Data ko Compress bhi kiya jata hai taaki jaldi travel kare.

Step 3: Session Layer (L5):
- Ye layer aapke computer aur Google ke server ke beech ek "Talk Session" shuru karti hai.
- Hota kya hai: Ye manage karti hai ki aapki request aur Google ka response ek hi session ka hissa rahein.

Step 4: Transport Layer (L4):
- Ab data ko bade chunks se chhote Segments mein toda jata hai.
- Hota kya hai: Kyunki ye web browsing hai, yahan TCP Protocol use hota hai. Har segment par ek Port Number (HTTPS ke liye 443) dala jata hai. Ye ensure karta hai ki data bina kisi error ke pahunche.

Step 5: Network Layer (L3):
- Ab asli pata (Address) lagne ki baari hai.
- Hota kya hai: Is segment par Google ka IP Address (Destination) aur Aapka IP Address (Source) chipkaya jata hai.

Step 6: Data Link Layer (L2):
- Ab data aapke computer se nikal kar aapke Wi-Fi Router tak jayega.
- Hota kya hai: Packet ke upar MAC Address dala jata hai. Router ka MAC address use hota hai taaki local network mein pata chale ki data physically kahan ja raha hai.

Step 7: Physical Layer (L1):
- Ab data binary (0, 1) mein badal jata hai.
- Hota kya hai: Ye 0s aur 1s electrical signals (Ethernet cable), light pulses (Fiber optics), ya radio waves (Wi-Fi) ban kar internet par daudne lagte hain.

Is tarike se OSI model ka concept kaam karta hai.

<br>
<br>

**Ab samjho ki Load balancer mein Layer-4 ka kya matlab hai**:

Jab user browser mein application ka url hit karta hai,
```
https://myapp.com
```
To browser is DNS ko Load Balancer ki Frontend IP (Public IP) mein resolve kar deta hai jisse request load balancer pe jaati hai.

To Load Balancer ke paas user ki request pahuchti hai, request packets ke form mein load balancer ke paas pahunchti hai.

Ek packet mein OSI Model ki multiple layers ke headers hote hain, jaise:
```
[ Ethernet Header ]
[ IP Header ]
[ TCP / UDP Header ]   ← Layer 4 yaha hai
[ Actual Data Payload ]
```
Layer 4 LB yaha tak hi dekhta hai.

Load Balancer sirf Layer 4 ki details ko dekhta hai, baaki load balancer ko kisi bhi detail se koi matlab nhi hota.

Layer-4 mein ye details hoti hai:
- Source IP.
- Source Port.
- Destination IP.
- Destination Port.
- Portocol (TCP/UDP).

To Load Balancer aane wali request mein sirf Source aur Destination ke IP aur port aur protocol ko dekhta hai. Wo payload ko open hi nahi karta.

Payload encrypted ho, compressed ho, HTTP ho, DB query ho — LB ko fark nahi.

Isliye Load Balacner ko Layer-4 LB bolte hain kyuki Load Balancer ko Source Ip, Destination IP, Source Port, Destination Port aur Protocol milte hi Load Balancer request ko backend par chal rahe VMs mein se ek vm par bhej deta hai.

Example incoming flow:
- Client IP → 49.x.x.x (User ki IP jisne request send ki hai).
- Source Port → (Client ke computer ka wo temporary port jahan se request nikli).
- Destination IP → 20.20.20.20 (Load Balancer ki IP).
- Port → 443 (Jis service ke liye request aayi hai (e.g., 443 for HTTPS)).
- Protocol → TCP

Jab packet Load Balancer ke paas aata hai, toh load balancer directly packet ko backend vms par nhi behjta, Usme 2 chize karta hai:

1 - Destination IP Matching:
- Pehle check karega ki packet ki destination ip kya load balancer ki public ip se match karti hai ya nhi, matlab apni public ip ko packet ki destination ip se match karta hai, agar dono ips same hoti hain to iska matlab vo packet load balancer ke liye hi aaya hai to us packet ko load balancer accept kar leta hai.
- Agar IP match nahi hui, toh LB us packet ko discard (phenk) dega.

<br>

2 - Change Destination IP with Backend Server's IP:


Kya LB Directly Backend par bhej deta hai?

Nahi, LB usse "as-it-is" (waisa ka waisa) nahi bhej sakta. Socho kyun:
- Packet par likha hai Destination: 20.20.20.20 (LB ki IP).
- Agar LB ne yahi packet Backend Server (jiski IP 10.0.0.5 hai) ko bhej diya, toh Backend Server packet kholte hi dekhega: "Arre, ispe toh destination 20.20.20.20 likha hai, lekin meri IP toh 10.0.0.5 hai! Ye packet mere liye nahi hai." * Aur server us packet ko Drop kar dega.


LB Packet ke saath kya karta hai? (NAT Process):

Isliye, backend server par bhejne se pehle LB ek bahut zaroori kaam karta hai jise Destination NAT (DNAT) kehte hain:
- Header Rewrite: LB packet ka header kholta hai (sirf Layer 3 aur Layer 4).
- IP Change: Wo Destination IP (20.20.20.20) ko mita kar wahan Backend Server ki IP (10.0.0.5) likh deta hai.
- Checksum Recalculation: Kyunki IP badal gayi hai, toh packet ka math (checksum) bhi badalna padta hai taaki error na aaye.
- Forwarding: Ab ye naya packet (jisme destination ab backend server hai) backend par bhej diya jata hai.

<br>

Response Ka Kya Hota Hai? (The Return Journey):

Ye sabse interesting part hai. Jab Backend Server jawab (Response) bhejta hai:
- Server ko lagta hai ki request Client (49.x) se aayi hai, lekin packet LB ke raste wapas jana chahiye.
- Jab response packet LB ke paas wapas aata hai, toh LB uska Source IP (Server ki IP 10.0.0.5) badal kar wapas LB ki IP (20.20.20.20) kar deta hai.
- Kyun? Taaki Client ko lage ki use jawab Google/Load Balancer se hi mila hai, kisi internal server se nahi.

To request ke packet mein ye sab changes karke Load Balancer, backend pool par chal rhe VMs mein se ek vm **Load Balancing Algorithms** se select karta hai aur us vm par request bhej deta hai.

<br>
<br>
<br>

### Components of Azure Load Balancer

Ek Layer 4 Load Balancer ke andar typically ye components hote hain:
- Listener / Frontend:
  - Ye Load Balancer ka public ip aur port hota hai jisko user browser mein hit karta hai.
    
- Backend Pool / Target Group:
  - Internally Load Balancer ek virtual machines ka ek group bana deta hai jisko backend pool kehte hain, in vms par application chal rhi hoti hai, to load balancer user ki request ko in vms mein se kisi ek par forward karta hai.

  Example:
  - 10.0.0.10
  - 10.0.0.11
  - 10.0.0.12
    
- Load Balancing Algorithm.
  - In algorothm ki help se load balancer ye decide karta hai ki konsi vm select karni hai request ko uspe forward karne ke liye, ye kuch rules hote hain jo batate hain ki ye vo vm hai jispe traffic bhejna hai.
 
  Common algorithms:
  - Round Robin → Sequential distribution.
  - Least Connections → Jis pe kam load.
  - Hash Based → IP/Port hash.
    
- Connection Table.
  - Layer 4 LB usually stateful hota hai. Ek table maintain karta hai:

| Client         | Backend Server | State       |
| -------------- | -------------- | ----------- |
| 49.x.x.x:50432 | 10.0.0.11:443  | ESTABLISHED |

  - Yeh ensure karta hai:
    - Same connection same server pe jaye.
    - Packet mix-up na ho.
   
<br>
<br>

### Ek Real World Flow Example

Assume karo:

Load Balancer IP → 20.20.20.20

Backend servers:
- Server A → 10.0.0.10.
- Server B → 10.0.0.11.

Client browser se:
```
https://myapp.com
```

Behind the scenes:
- DNS resolve → 20.20.20.20
- TCP Connection:
  - Step 1 – SYN ```Client → “Hello server, connection banana hai.”```.
  - Step 2 – SYN-ACK ```Server → “OK, ready hoon.”```.
  - Step 3 – ACK ```Client → “Confirmed.”```
- Isko bolte hain: Three-Way Handshake.
- Matlab uper three way handshake User aur LB ke beech mein ho rha hai.
- LB receives SYN (iska matlab hai ki LB ke saath user ka three way handshake ho gya hai).
- LB ka logic:
  - TCP? ✅.
  - Port 443? ✅.
  - Public IP Matching.
- Algorithm run:
- Example Least Connections:
  - Server A → 120 connections.
  - Server B → 45 connections.
- LB chooses → Server B.

Ab:
- Entire TCP session → Server B.
- Multiple packets → Same server.
- Matlab request Server B ko forward kar di hai Load Balancer ne.



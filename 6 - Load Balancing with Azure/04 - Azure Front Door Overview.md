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

Ye basically Microsoft ka worldwide private backbone infrastructure hai jiske through Azure services ka traffic internet par random routes se nahi balki Microsoft ke khud ke high-speed fiber network par travel karta hai.


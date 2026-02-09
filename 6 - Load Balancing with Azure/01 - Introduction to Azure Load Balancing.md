# Introduction to Azure Load Balancing

Yahan hum dekhenge ki Azure mein load balancing ke liye kon kon se resources ka use hota hai, vo resources kaise kaam karte hain aur kaise unko implement karn hai.

<br>
<br>

### Azure Load Balancing Services – Big Picture

Azure mein load balancing ko broadly 2 major categories mein divide kiya jaata hai:
- Regional Load Balancing.
- Global Load Balancing.

Azure mein ye kuch services hoti hain jo Load Balancing provide karti hain:
- Azure Load Balancer.
- Azure Application Gateway.
- Azure Front Door.
- Azure Traffic Manager.

Azure mein maine ye 4 services hoti hain load balancing ke liye.

<br>
<br>

### Regional Load Balancing kya hoti hai

Azure Regional Load Balancing ka matlab hai ek hi Azure region ke andar multiple backend resources (VMs, App Services, AKS pods, etc.) ke beech traffic ko smart tareeke se distribute karna.

Iska matlab ek hi azure region jaise Central India, isi mein services ke beech mein load balance karna matlab traffic ko distribute karna.

Regional Load Balancing ka matlab hota hai traffic ko ek hi specific region (jaise Central India ya East US) ke andar distribute karna. Jab aapki application ek hi geographical area mein hosted hoti hai, tab aap regional load balancers ka use karte ho taaki traffic multiple Virtual Machines (VMs) ya containers ke beech barabar bat sake.

**Example**:

Jaise Central India region hai, usme 2 virtual machine bani hui hain, un VMs par web application chal rha hai, to in dono virtual machines par load balance karna, kyuki ye vms ek hi region mein hain isliye regional load balancing.

<br>

**Azure mein Regional Load Balancing ke main components**:

Azure mein regional load balancing ke liye mainly ye services use hoti hain:
- Azure Load Balancer.
- Azure Application Gateway.
- Azure Front Door (ye global bhi hai, par region ke andar bhi kaam karta hai).


<br>

**"Regional" hone ka asli fayda kya hai?**:

Aapne pucha "Ye regional kyu hota hai?" Iska sabse bada reason hai Availability Zones (AZ).

Central India ke andar 3 alag-alag datacenters (Zones) ho sakte hain jo ek dusre se thodi doori par hote hain lekin same city/region mein hote hain.

- Scenario A (No Regional LB): Aapne ek hi VM banaya. Agar us datacenter ki bijli chali gayi, toh aapki app band.
- Scenario B (Regional LB with 2 VMs):
  - VM 1 ko aapne rakha Zone 1 mein.
  - VM 2 ko aapne rakha Zone 2 mein.
  - Aapka Regional Load Balancer in dono zones ke upar baitha hai.
  - Agar Zone 1 pura ka pura flood ya power cut ki wajah se down ho gaya, toh aapka Regional Load Balancer turant detect kar lega ki VM 1 mar chuka hai. Wo saara traffic VM 2 (Zone 2) par shift kar dega.

<br>
<br>

### Global Load Balancing kya hoti hai

Global load balancing ka kaam traffic ko alag-alag geographical regions ke beech mein distribute karna hai.

Jab aapki application itni badi ho jati hai ki aap use multiple regions (jaise Central India, East US, aur West Europe) mein deploy karte ho, tab aapko ek aise master system ki zarurat padti hai jo ye decide kare ki user ko kis region mein bhejna hai. Wahi hai Global Load Balancing.

Global Load Balancing ka matlab hai poori duniya (multiple Azure regions) ke users ka traffic best, nearest aur healthy region mein bhejna.

Yaani:
- India ka user → India region.
- Europe ka user → Europe region.
- US ka user → US region.

Aur agar koi region down ho jaye ❌ ➡ traffic automatically dusre region mein shift ho jata hai ✔️.

**Example**:

Agar koi user America se aapki site open kare, toh use India wale server par kyu bhejna? India ka server door hone ki wajah se site slow chalegi. Global Load Balancer use automatically East US wale region mein bhej dega.

<br>

**Azure mein Global Load Balancing ke main components**:
- Azure Front Door.
- Azure Traffic Manager.

<br>

**Global Load Balancing Kyun Use Karein?**:
- **Lowest Latency**: User ko hamesha sabse paas wala region milta hai.
- **Centralized Security**: Aap ek hi jagah (Front Door) par firewall lagakar poori duniya ke regions ko secure kar sakte ho.
- **Seamless Upgrades**: Agar aapko India region mein maintenance karni hai, toh aap Global LB se traffic temporary US shift kar sakte ho bina "Site Under Maintenance" dikhaye.

<br>

**Global vs Regional: Ek Saath Kaise Kaam Karte Hain?**

Aapke High Availability (HA) aur Disaster Recovery (DR) project ke liye ye sabse important part hai. Asli corporate setups mein dono ka combo use hota hai:
- Level 1 (Global): Sabse upar Azure Front Door baitha hoga. Ye check karega ki user New York se hai ya Delhi se.
- Level 2 (Regional): Maan lo user Delhi se hai, toh Front Door ne traffic Central India region mein bhej diya.
- Level 3 (Local): Central India ke andar aapka Application Gateway ya Standard Load Balancer baitha hoga, jo us traffic ko Central India ke 2-3 alag-alag VMs par distribute karega.

<br>

**Disaster Recovery (DR) Mein Iska Role**

Maano aapka Central India region pura ka pura "down" ho gaya (Major Azure outage):
- Regional LB ka kya hoga? Wo toh region ke sath hi khatam ho jayega.
- Global LB (Front Door) kya karega? Front Door continuously "Health Probes" bhejta rehta hai har region ko. Jaise hi use lagega ki India region respond nahi kar raha, wo 1 minute ke andar saara traffic West US ya jo bhi aapka secondary DR region hai, wahan divert kar dega.
- User ka experience: User ko shayad 1-2 second ka lag mehsoos ho, lekin site band nahi hogi.


<br>
<br>
<br>

## Ab aage ki slides mein hum dekhenge Load Balancer ke baare mein.

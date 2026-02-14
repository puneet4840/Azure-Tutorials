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
<br>

### Ye Layer-4 Load Balancer ka kya matlab hai?

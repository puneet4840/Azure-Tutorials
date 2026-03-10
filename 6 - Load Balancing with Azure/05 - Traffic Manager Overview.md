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

Yeh ek Level 7 (DNS-based) service hai. 

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


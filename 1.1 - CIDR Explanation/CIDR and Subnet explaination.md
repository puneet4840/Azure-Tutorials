# CIDR Explaination

### What is Computer Networking?

Computer Networking is the collection of devices connected with each other which share the data or information between them.

<br>

### IP Address

IP Address is the unique number assigned to a device to identify a device on a network.

**Two Types of IP Addresses**

- IPv4.
- IPv6.

**- IPv4**:

An IPv4 address is a series of four number seperated by dots.

e.g., - ```198.168.10.26```

e.g., - ```10.1.2.4```

Each number ranges between 0 - 255.

<img src="https://github.com/user-attachments/assets/c7464fd6-9028-40f4-b194-bf64bc59e1b1" width="400" height="180">

<br>

**Why does the IP Address ranges from 0 to 255?**

```172.16.3.4```

```
IP address hamare liye ek number hota hai lekin computer is number ko nahi samajh pata hai.
Computer sirf bits yani 0 aur 1 ko hi samjhta hai. IP Address ka har ek path jaise uper diye gaye ip main 172 jo part hai.
Vo 1 byte ka hai aur 1 byte main 8 bits hoti hain.

An IP address range goes from 0 to 255 because each part of an IP address is represented by a single "octet"
which is made up of 8 binary digits (bits), and the maximum value that can be represented with 8 bits is 255

1 byte = 8 bits
8 bits can be represent using either 0 or 1.

Minimum number using 8 bits = 00000000 => 0
2^8*0 + 2^7*0 + 2^6*0 + 2^5*0 + 2^4*0 + 2^3*0 + 2^2*0 + 2^1*0 + 2^0*0 = 0

Maximum number using 8 bits = 11111111 => 256
2^8*1 + 2^7*1 + 2^6*1 + 2^5*1 + 2^4*1 + 2^3*1 + 2^2*1 + 2^1*1 + 2^0*1 =>  128 + 64 + 32 + 16 + 8 + 4 + 2 + 1 = 255

IP address ke ek part minimum 0 aur maximum 255 ho sakta hai kyuki ek part 8 bits ka hota hai aur 8 bits ko add karne par 255 maximum number aata hai.
```

<br>

### Subnet

A subnet is the small network divided from a large network.

subnetting is the process of creating a subnet.

e.g.,

```
Suppose एक कंपनी का नेटवर्क है उस कंपनी मैं multiple departments हैं जैसे- Finance , Payroll , Sales , Development.
अगर कंपनी इन सभी departments को एक ही network assign कर देती है|
अगर किसी सेल्स department के employee ने कोई malicious वेबसाइट access कर ली और hacker के पास device का access आ गया|
तो हैकर उन सभी device को access कर सकता है तो ये एक company के लिए danger हो सकता है|

तो company इससे बचने के लिए subnetting का उसे सकती है हर department के लिए अलग से एक subnet बना सकते हैं  
```

**Two types of subnetting :-**

- **1 - Private Subnet**: The subnet which does not have access to Internet. Resources launched in the private subnet do not have public ip address.

- **2 - Public Subnet**: The subnet which has access to internet. It allows resources in the subnet to access the public internet.

<br>
<br>

### CIDR (Classless Inter-Domain Rounting)

It is a technique to create a subnet inside a network.

```
                     OR
```

CIDR is a way of explaining how many IP Addresses are available in a particular subnet.

```
                     OR
```

It is a technique used for allocating IP Addresses more efficiently.

<br>

**CIDR Notation**

CIDR notation uses format: _IP_Address/Prefix_length_.

e.g.,  192.168.10.26/24

<img src="https://github.com/user-attachments/assets/c9f38301-027f-4779-91ea-1a361d789387" width="400" height="180">

```Prefix length (e.g., 24) indicates the number of bits set to 1 in the subnet mask OR How many bits are used for the network protion.```

```In this example /24 means the first 24 bits are reserved for the network, and leaving the last 8 bits for host addresses within that network```

```With CIDR, you can assign the network size based on the needs of the organization.```

<br>

**History of CIDR**

CIDR was introduced in 1993 to slow down the exhaustion of Ip Addresses. Before CIDR was introduced, IP addresses were allocated based on IP classes. These classes had fixed sizes for networks, and they led to inefficiencies, such as wasted IP addresses.

**The Old-Class based system**

- **Class A**: Very large networks (e.g., 10.0.0.0), with around 16 million IP addresses available per network.

- **Class B**: Medium-sized networks (e.g., 172.16.0.0), with around 65,000 IP addresses per network.

- **Class C**: Small networks (e.g., 192.168.0.0), with 256 IP addresses per network.

This class-based system know as **Classful Networking**. It has several problems:

- **Wasted IP Addresses**: कुछ organizations को कम IP Addresses चाइये होते थे और उस टाइम पर सिर्फ class-based ip addressing technique उसे होती थी तो ऐसे मैं high class को उसे करके ip addresses assign होते थे जिससे ip addresses waste ho jate the होते थे. Suppose a small business allocated a Class B network with 65,000 addresses might only need 500, resulting in a huge waste of addresses.

- **Growing Routing Tables**: The increasing number of networks meant that routers had to maintain very large routing tables, slowing down the internet.

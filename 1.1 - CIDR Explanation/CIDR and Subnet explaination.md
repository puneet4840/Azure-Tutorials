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


# Azure Active Directory

### What if there is not Active Directory?

The main function of Active Directory is **Authentication**. It authenticate username and password.

```Suppose आपके पास एक laptop है. तो आप किसी employee को एक laptop issue चाहते हो तो उस employee के लिए आप एक username create और password create करके उसको दे दोगे. जब भी user इस laptop पर अपने username और password से login करेगा तो वहां authentication होगा. तो जो भी authentication हो रहा है वो local authentication हो रहा है.```

```user अपना username और password डालता है और laptop के अंदर login कर लेता है```

 **Note**:- ```लेकिन इसके साथ बोहोत सारे challenges थे:-```

- ```अगर आपकी company छोटी है बस 10 या 15 employees हैं तो आप हर किसी employee के username और password create करके user को दे सकते हो| लेकिन अगर आपकी company बड़ी है और 1000 या 5000 employee काम करते हैं तो आप हर employee के लिए username और password create करके नहीं दे सकते| आप हर laptop पर जाकर username और password create करेंगे तो ये एक बोहोत difficult scenario हो जाता है, इसके लिए आपको एक अलग team बिठानी पड़ेगी|```

- ```दूसरा problem ये है की अगर user को एक दूसरा device दिया जाये तो उसके लिए भी username और password create करके देना पड़ेगा फिर जाकर user उस दूसरे device पर भी लॉगिन कर पायेगा|```

- ```तीसरा problem ये भी है की अगर user remote location पर काम करने जाता है और अपने username और password भूल जाता है तो ऐसे मैं आप as a administrator उसके device पर remotely access करके admin password के through उसका password reset करेंगे| ```

<br>
<br>

### Active Directory Explaination

Let's understand active directory here-

Suppose हमने एक server पर Active Directory install कर दी. जैसे ही किसी server पर Active Directory install हो जाती है तो उस server को **Domain Controller** कहा जाता है. इसको Domain Controller इसलिए कहा जाता है क्युकी ये एक domain यानि logical boundary बना देता है.

**e.g.,**

अगर आपकी कंपनी मैं कोई नया employee आया है तो उसके लिए आप एक laptop लेंगे और laptop को domain मैं join कराएंगे और साथ ही साथ उस employee का जो user account है उसको active directory में जाके create कर देंगे. 
- जैसे जब मैंने Nagarro join की थो तो Nagarro ने मुझे एक laptop अपने Nagarro के domain मैं join करके दिया था. मतलब उस laptop में मैं नगररो के username aur password से hi login कर सकता हूँ बस. 

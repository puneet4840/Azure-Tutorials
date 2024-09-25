# Azure Active Directory

### What if there is not Active Directory?

The main function of Active Directory is **Authentication**. It authenticate username and password.

```Suppose आपके पास एक laptop है. तो आप किसी employee को एक laptop issue करते थे तो उस employee के लिए आप एक username create करते थे और password create करके उसको दे देते थे. जब भी user इस laptop पर अपने username और password से login करेगा तो वहां authentication होगा. तो जो भी authentication हो रहा है वो local authentication हो रहा है.```

```user अपना username और password डालता है और laptop के अंदर login कर लेता है```

 **Note**:- ```लेकिन इसके साथ बोहोत सारे challenges थे:-```

- ```अगर आपकी company छोटी है बस 10 या 15 employees हैं तो आप हर किसी employee के username और password create करके user को दे सकते हो| लेकिन अगर आपकी company बड़ी है और 1000 या 5000 employee काम करते हैं तो आप हर employee के लिए username और password create करके नहीं दे सकते| आप हर laptop पर जाकर username और password create करेंगे तो ये एक बोहोत difficult scenario हो जाता है, इसके लिए आपको एक अलग team बिठानी पड़ेगी|```

- ```दूसरा problem ये है की अगर user को एक दूसरा device दिया जाये तो उसके लिए भी username और password create करके देना पड़ेगा फिर जाकर user उस दूसरे device पर भी लॉगिन कर पायेगा|```

- ```तीसरा problem ये भी है की अगर user remote location पर काम करने जाता है और अपने username और password भूल जाता है तो ऐसे मैं आप as a administrator उसके device पर remotely access करके admin password के through उसका password reset करेंगे| ```

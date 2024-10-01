# Multi Factor Authentication

Multi Factor authentication is the Multi Layer Authentication.

```
OR
```

Multi Factor authentication is the method to secure the accounts from unauthorized access.
```
OR
```
Multi Factor authentication adds an extra layer of security when user log into their accounts. Instead of relying on single factor like password. MFA requires additional proof of identity.

<br>

```Multi Factor authentication login करने का एक ऐसा method है जिसके through हम unauthorized access से अपने accounts को secure रखते हैं.```
<br>

e.g., **Without Multi Factor Authentication**

```Suppose हम Outlook मैं login कर रहे हैं और Outlook के account पर Multi Factor Authentication नहीं लगा हुआ है तो इससे हम सिर्फ Username/Gmail और Password के through login कर सकते हैं. जो एक simple login method होता है और बिना Multi Factor Authentication के कोई भी person हमारे account पर username और password लेकर login कर सकता है. ```

e.g., **With Multi Factor Authentication**

```Suppose हम Outlook मैं login कर रहे हैं और Outlook के account पर Multi Factor Authentication लगा हुआ है तो इससे हमको Username और Password के साथ साथ एक और code या pin की जरुरत होती है ये code या pin हमारे Gmail, Phone Number या Call के thorugh send किया जाता है और जिसको enter करने के बाद लॉगिन कर सकते हैं.```

<br>

### How does MFA works?

MFA typically works when logging into an Azure AD-secured application

**1 - User Logs In**:
  
  - A user opens an application or service secured by Azure AD, such as Outlook, Teams, or an internal company portal.
 
    - The user enters their username and password (the first factor).

**2 - Verification Prompt**:

  - Azure AD recognizes that MFA is required for this user and sends a second authentication request.
 
  - The user receives a prompt for the second factor. This could be:
        - A **text message** with a code sent to the user’s mobile phone.
        - A notification in the **Microsoft Authenticator** app.
        - A call to a **mobile** or **landline phone**.
        - A request for a **biometric scan** (fingerprint, facial recognition).

**3 - Second Factor Confirmed**:

  - The user confirms their identity by entering the verification code, approving the app notification, or using the biometric scan.
 
  - Once the second factor is verified, the user is granted access to the application.

**4 - Access Granted**:

  - The user is now logged into the application securely.

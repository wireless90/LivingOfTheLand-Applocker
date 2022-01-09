# LivingOfTheLand-Applocker
Preventing LOTL attacks using Applocker

# Introduction

Living off the Land (LOTL) refers to attackers using either operating system features or binaries to fly under the radar when performing sophisticated attacks. A legitimate tool is less likely to raise suspicions and less likely to trigger an antivirus detection. With attackers and employees using the same tools and processes, malicious activity becomes a needle in the haystack, hidden among the vast and growing legitimate activity on the victim’s network.

This article focuses at some LOTL Binaries (LOLBins) whose function enables an attacker to execute his Scripts/executables, by passing AppLocker's default rules. We will also then look at Applocker rules that will mitigate them.

# Applocker Default Rules

The Applocker by default only allows scripts/executables to be ran in the `Program Files` or `Windows` folder.

![image](https://user-images.githubusercontent.com/12537739/148684205-60f25867-0b5c-43a7-ae81-852885688cc8.png)


# MSHTA.EXE

Used by Windows to execute html applications. (.hta)

We can execute `javascripts` or `vbs` by masking them under `.hta` files.

Below we have a javascript file that opens up a calc.exe

```js
<script LANGUAGE="JScript">
  new ActiveXObject("WScript.Shell").run("calc.exe");
</script> 
```

If we were to double click it or open it using `wscript` or `cscript`, Applocker blocks it.

![image](https://user-images.githubusercontent.com/12537739/148684092-35c5d2c6-37ff-4236-a965-b6d286a6e42b.png)

This is because the script is not in the `Program Files` or `Windows` folder.

If we were to rename the extension to `.hta`, windows uses `mshta.exe` to open it which is allowed by Applocker as it is in `C:\Windows\System32\`, which is a subdirectory of the `windows` folder.


![image](https://user-images.githubusercontent.com/12537739/148684354-e550616f-6ebe-425e-a178-c1753c2996cb.png)


# Credits

https://seminda.wordpress.com/create-custom-installation-applications-by-using-the-installer-class/
https://lolbas-project.github.io

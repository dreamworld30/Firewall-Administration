# **Intro to Firewalls** 

A concise, beginner‑friendly overview of firewalls: what they are, how they evolved, the major types (packet‑filtering, stateful, application/WAF, and NGFW), deployment models (hardware, software, cloud), and hands‑on management basics for Windows and Linux.

**TL;DR:** A firewall monitors and controls network traffic using rules. Think of it like a building’s fire wall: it prevents “flames” (malware) from spreading between “rooms” (networks/hosts).

---

## **What Is a Firewall?**

A **firewall** is a network security control that monitors and filters **incoming and outgoing** traffic to prevent unauthorized access and cyberattacks.

**Analogy:** 

* **House** \= Network   
* **Fire** \= Malware/threats   
* **Firewall** \= Barrier that limits the spread

---

## **A (Very) Short History**

* **1988:** Digital Equipment Corporation (DEC) ships the first **packet filter** firewall.   
* **Late 1990s:** **Application‑layer firewalls** appear for deeper inspection.   
* **2009:** Gartner coins **Next‑Generation Firewall (NGFW)** — adds application awareness, IPS, and malware detection.

Firewalls remain a **first line of defense** and should be enabled on endpoints and networks.

---

## **Core Types of Firewalls**

### **1\) Packet‑Filtering Firewall**

Simple rule‑based filtering on packet headers (no payload inspection).  

Typical criteria: **source/destination IPs**, **ports**, **protocols**.

**Analogy:** Security at a private event checking the **guest list**. 

* Visitors \= traffic   
* Security \= firewall   
* Guest list \= rules/ACLs

**Pros:** Lightweight, fast, easy for small networks.  

**Limitation:** Can’t detect malicious **content** hidden inside allowed packets.

---

### **2\) Stateful Firewall**

Tracks **connection state** (e.g., new/established/closing) and uses context to allow **return** traffic automatically.

**History:** Introduced by **AT\&T Bell Labs (1989)**.    
**Analogy:** If a guest inside invites their partner, security verifies the relationship and lets them in—even if not on the original list.  

**Example:** **Microsoft Defender Firewall (Windows 11\)** is stateful.

**Key difference vs. packet filter:** 

* **Packet filter**: Static, per‑packet rules only.   
* **Stateful**: Dynamic, uses **connection history/context**.

---

### **3\) Application Firewall (Layer 7\) / WAF**

Operates at **OSI Layer 7**; inspects **headers \+ content** (deep packet inspection). Can enforce **per‑application** policies.

**Protects against:** SQL injection, XSS, command injection, etc.  

**Types:** 

* **WAF** (HTTP/HTTPS for web apps)   
* **Database firewall**   
* **Email firewall** (spam/phishing)

---

### **4\) Next‑Generation Firewall (NGFW)**

Adds **app awareness**, **malware detection**, and **intrusion prevention (IPS)** to traditional firewalling. Often integrates with broader security tooling.

**Great for:** Highly regulated or threat‑targeted environments (finance, healthcare, etc.).

---

### **Quick Comparison — App Firewall vs. NGFW**

| Feature | Application Firewall | NGFW |
| ----- | ----- | ----- |
| **OSI Layer** | Layer 7 | Multiple (incl. L7) |
| **Focus** | Specific applications | Whole network & threats |
| **Deep Packet Inspection** | ✅ | ✅ (more advanced) |
| **Stops App Attacks** | ✅ | ✅ |
| **Malware Detection** | ❌ | ✅ |
| **Intrusion Prevention** | ❌ | ✅ |
| **Ecosystem Integration** | Sometimes | Often |

---

## **Hardware vs. Software Firewalls**

### **Hardware Firewall**

Physical appliance protecting whole networks (perimeter/DMZ/segments).  

**Best for:** Medium–large orgs; centralized control. *(Often licensed.)*

### **Software (Host) Firewall**

Installed on a specific device (e.g., **Windows Defender Firewall**).    
**Best for:** Individual systems, small offices, or additional host‑level control.  

Includes **container** and **virtual/cloud** firewalls.

**Comparison**

| Feature | Hardware | Software |
| ----- | ----- | ----- |
| **Form** | Physical device | Application |
| **Scope** | Entire network | Single host |
| **Placement** | Perimeter/DMZ/segments | On the device |
| **Best For** | Medium–large orgs | Individuals/small offices |
| **Examples** | Cisco ASA, Fortinet, Palo Alto | Windows Defender Firewall |

---

## **Deployment Models**

### **1\) Network‑Based Firewalls**

* **Purpose:** Protect an entire network.   
* **Placement:** Perimeter, DMZ, or between **internal segments**.   
* **Functions:** Packet filtering, DPI, NAT.   
* **Pros:** Broad protection. **Cons:** Complexity, cost/training.

### **2\) Host‑Based Firewalls**

* **Purpose:** Protect a single device/VM.   
* **Functions:** Often **application‑aware**, GUI‑friendly.   
* **Pros:** Granular control. **Cons:** Per‑host management (unless centralized via **Group Policy**, etc.).

### **3\) Combined (Layered) Use**

* **SOHO/home:** Router firewall \+ host firewalls may be enough.   
* **Enterprises:** Network firewall at the perimeter **plus** host firewalls on critical systems.

**Summary**

| Feature | Network‑Based | Host‑Based |
| ----- | ----- | ----- |
| **Scope** | Entire network | Single device |
| **Placement** | Perimeter/DMZ/segments | On device/VM |
| **Complexity** | High | Low–Medium |
| **Cost** | Higher | Lower |
| **Resources** | Separate hardware | Uses host CPU/RAM |

### **4\) Cloud‑Based Firewalls & FWaaS**

* Lives in **Azure/AWS/GCP** or similar.   
* Helpful for **remote work** and **cloud apps** (traffic doesn’t need hair‑pinning through on‑prem).   
* Managed centrally; can protect cloud resources and connected sites.   
* **FWaaS:** Third‑party manages deployment/updates for you.

---

## **Key Components & Best Practices**

1. **Use a firewall** (endpoint \+ network). Keep it **enabled**.   
2. **Harden config:** No default creds; understand your architecture; back up rules.   
3. **Monitor & log:** Review logs; enable logging on drops/accepts.   
4. **Seek expertise** where needed (MSPs/MSSPs).   
5. **Layered security:** Firewalls **≠** anti‑malware. Use **AV/EDR**, **VPN**, **IDS/IPS**, and keep systems **patched**.

---

## **Managing Firewalls: Windows Client**

### **Network Profiles**

* **Private:** Trusted (home/office). Allows discovery/sharing.   
* **Public:** Untrusted (cafés/airports). Stricter rules, hide device.   
* **Domain:** Corporate AD domain.

**Tips:** Choose the correct profile; keep firewall **ON** for all profiles; consider **“Block all incoming”** on public networks.

### **Allowing/Blocking Apps**

* *Settings → Privacy & Security → Windows Security → Firewall & network protection → Allow an app through firewall.*   
* Choose app \+ profile(s).

### **Advanced Settings (WFAS)**

* *Control Panel → Windows Defender Firewall → Advanced settings.*   
* **Inbound/Outbound rules**, **Connection Security rules**, **Monitoring**.   
* **Logging:** Enable logging for dropped/successful connections.   
* **Stateful:** Return traffic for established connections is allowed automatically.

**Example — Allow TCP Port 80 (Outbound):** 

1. Outbound Rules → **New Rule** → **Port**.   
2. **TCP**, **Specific port**: `80`.   
3. **Allow the connection** → select **Domain/Private/Public**.   
4. Name it (e.g., “Allow TCP 80”).

---

## **Managing Firewalls: Linux (Ubuntu/Debian)**

Linux uses **netfilter** in the kernel; common tools: **iptables**, **firewalld**, **UFW** (default Ubuntu), **GUFW** (GUI).

### **Install (if needed)**

sudo apt install ufw       \# CLI

sudo apt install gufw      \# GUI

### **Status / Enable / Disable**

sudo ufw status

sudo ufw enable

sudo ufw disable

### **Defaults (choose policy)**

sudo ufw default deny incoming

sudo ufw default allow outgoing

\# or:

sudo ufw default reject incoming

### **Open a Port / Service**

sudo ufw allow 22/tcp          \# SSH

sudo ufw allow 80,443/tcp      \# HTTP/HTTPS

sudo ufw delete allow 22/tcp   \# remove rule

**GUFW Notes:** Profiles (Home/Office/Public), logging toggle, and simple **Allow/Deny/Reject** actions.

---

## **Glossary**

* **ACL:** Access Control List — rules that permit/deny traffic.   
* **DPI:** Deep Packet Inspection — looks beyond headers into payloads.   
* **DMZ:** Demilitarized Zone — isolates public‑facing services.   
* **IPS/IDS:** Intrusion Prevention/Detection Systems.   
* **NAT:** Network Address Translation — remaps IP addresses/ports.   
* **State Table:** Tracks connections for stateful filtering.

**Certificate of Completion:**   
[![][image1]](https://www.linkedin.com/learning/certificates/25f57f7247ff02834b31b2a59a936a3594619495bd4770fcef0a8aac4f7b4996?trk=share_certificate)

Link: [https://www.linkedin.com/learning/certificates/25f57f7247ff02834b31b2a59a936a3594619495bd4770fcef0a8aac4f7b4996?trk=share\_certificate](https://www.linkedin.com/learning/certificates/25f57f7247ff02834b31b2a59a936a3594619495bd4770fcef0a8aac4f7b4996?trk=share_certificate)

[image1]: <data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAc0AAAFlCAYAAACJCrOeAABYjklEQVR4XuydB3gUVduGCVX5FBABgSBYAAu/haYogiKioCjwWVBREBBEKaJIDYQivVdpgvReDF0ghEDoSCgJCSYEgglJkJBIiEnM7vf+c87szM6cnU12hwAJ89zX9Vw7c2bmzOzs7tx7phZ67LHHCEEQBEGQ3FPo5607CUEQBEGQ3ANpIgiCIIiHgTQRBEEQxMNAmgiCIAjiYSBNBEEQBPEwkCaCIAiCeBhIE0EQBEE8DKSJIAiCIB4G0kQQBEEQDwNpIgiCIIiHgTQRBEEQxMNAmgiCIAjiYSBNBEEQBPEwkCaCIAiCeBhIE0EQBEE8DKSJIAiCIB4G0kQQBEEQD5Nn0gQAAADyM6K3zATSBAAAYAlEb5kJpAkAAMASiN4yE0gTAACAJRC9ZSaQJgAAAEsgestMIE0AAACWQPSWmUCaAAAALIHoLTOBNAEAAFgC0VtmAmkCAACwBKK3zATSBAAAYAlEb5kJpAkAAMASiN4yE0gTAACAJRC9ZSaQJgAAAEsgestMIE0AAACWQPSWmUCaAAAALIHoLTOBNAEAAFgC0VtmAmkCAACwBKK3zATSBAAAYAlEb5kJpAkAAMASiN4yE0gTAACAJRC9ZSaQJgAAAEsgestMIE0AAACWQPSWmUCaANxC/smy0ahV50xn48F4sUoAgElEb5kJpAnALeStQSH0zJe7byp/XE4TqwUAmED0lplAmgDcQl7ts89Fgt4m5GyyWC0AwASit8wE0gT5jiZ996v53//+Jw4mVvT+j0e4UP7NtomD3fKu/0G13rzmQlK6WveKoD/VckWaDb/dS2n/ZFOU1GoUpZhbjKTJ3v+vhy+LxQCAHBC9ZSaQJsh3aIVhJM3YK+nq8FXBceJgt7wsiUuZLq+JTrih1v3z9otquSLNMxdS1bJv55xyEWNOMZLmaz9Icg52yjk/8d7Qg3T5WoZYDMAdR/SWmUCaIN+hFYaRNLNtdnV4VLznx/vupDSHLYtQyxp9H+wixpxS0KTJlnkTWsEgHyJ6y0wgTZDv0ArDSJqMjH9tdDw6RSzOkTspTRYmyzpfB7pIMbcUNGn+m20XiwDIF4jeMhNIE+Q7tMJwJ01leNTlG5SYkqn2Lw6MpRd7BKn9b/sdILujDlGarO5G3zlbfT1/OsnLGmvKlOwKTVLnzaSgnY5l+d5LareRNKcHnFfLXnFMa7fLy/XaD/von6xsdXh88j/0XNebl2aWtJwLd16kQYvDadfJK+Jg/l7ZMdYxayJp+/FE3p+a/i+Fxf7Nh2dKf0zYJTPX0rJo7f44PjxaGp/temXLPnx5BM3ZGiON55Tk6YupPMo6D7/0N58+2/Y/WrTrIvlJy8KWS+Rfm52WBF6imZvP040MeV3wehzrCIC8QPSWmUCaIN+hlZG30jTKtE2ysERpfjLmqNrf0v8gn1e36aFqWX2NfJVpGC9p6jGKt9K0GYhhf/hVtT4z0pz/2wU+bacpJ2jyxmhq3CeYhiw5qw5n75WdGPX8V4E06Jdw+mj0Eaotda/c9ye92DOIj3PxSjr9sjuWC7zlUHn9tJXWWXfpz8WzUtmgReHUYvABPp9zjt3krYYfpga9glQxsvfqL8332S676Stp3faee5qelcZPSnEe8ww4fJnX8eGoI1yqbJnm75CXPyPL8xO9AMgN0VtmAmmCfIdWQGakueFAvE46rCXH0EpzmNRKUrpZOeO8Yxcr28CzVhbjn0ybOl781X/oYESy2s827sFhf1HcVX3L0FtpXknNpGYDQuiraSd071epz1tpJkgtQTYda+FpYe9r75m/ePc3M0Kp8ffBuuHKdFpp1ukWqGvtMWnW675Htwu250+nqLY0nkKf+Wd00mQtd5vdOf7HUh3NB4Xw7pQb//J5XkxKV4cz2GfGyiFNkJeI3jITSBPkOxRZsHgrzS8m/e4yDpMbQytNJc9JImEnFjEG/BLGy9iGfsSKSDX1JUmw8p9/u0hdpp5Qp2WSVYj487pa7q00m/bbr07LBKyglHkrzTZSa2+g1AoUYa23pn33k81xIlXsFee8FJi4tdJctCtWN5xJc+zaP3RlbDcqq09BlObGA/qTgn47kUgNpFY842up9ckkKsL+oLA6IU2Ql4jeMhNIE+Q7FFmweCvNiRucG3SlLCdpdpsZqo7/4Sjn7lqj9JNk8IZGcNpjc9ozer2VpnYehyKdglTKvJUmk/xbA0Pov5I8tWk55CCv7+90uXWn/FnQsk9qOWuleSrGeakMw0iakXHytacKuUmTHR9WpPnq9/to85EE3XAGWzesTkgT5CWit8wE0gT5Dq1EvJXmtE3RLuMYSZOVKd2nHddQ9nJcP/nKd3t5q1JM4Mkr1HaUfFMFlkTNcbnziTmfPXs7pflC9yBaHxLPd3ka5XoO0txyNEEnzfDY67rheS3N13/YR6v2ub4P5U8IpAnyEtFbZgJpgnyHViKfjjtG7TTp6Nj9qgw3K80zF//WzYdtnP+Id96th11CwmBiazXsEBcmg7WKlHHqfbOHTkotsSRp/uyYnlJ+p6X55ZQTfF2J/PV3Jtls/+NntrLjm9p5KbSW3uvtlOaIZRHUtL/rHZqORV1TPxcA8grRW2YCaYJ8h1YiYup/vUc3jllpMk5Ep+jqTr3xL5eEOE/tNIyRKyNdhr3c21n37ZJm56knaOKGKF3mbL/Ah7NdsfUlqQef+YvikzNotdSaYycrpWfKl3OwV9b/yeij/MzX3dKfAnbSz9AVEbdVmoxOk3/nZ+7ulMpZi/1TaR7/HXGY1wlpgrxE9JaZQJog38Eu+3AXdqamdpzLkhDYWaJK/6Yjzg20UvbNzJO8/7t5p9UyBf+lZ9WyH34+w8sORCRLrcvDvPXIzhRll0GIG+/TUku1zQh5nLcGHVAvV2H57XfnNZ2KNFn5muA4HuXEolV7/+T9WmmOW3NOHS8nafZbEKZbL0rYyUwKS/dc4tJiy/iOJNEsxxnBCuw99Zl/mupIf0RYa5q1tNkNI3rPldcx+zPCblmoZYy0fGtD9I8r+/PqP7p1yk44Unb9snV6KEK//CfOp/BbCWr57UQSNRsYwi/nWR50iZ9tC2mCvEb0lplAmgDcQvCUE3NExsktfnamLwB5hegtM4E0AbiFvO/YzXgzYS25u5n3hh3kklRO+jr753W+63jYUufNGADIC0RvmQmkCcAthB23PBx5zXRiEvS7R+9GpgVE82Oayp+E5yVhLt4d6/bMaQDMInrLTCBNAAAAlkD0lplAmgAAACyB6C0zgTQBAABYAtFbZgJpAgAAsASit8wE0gQAAGAJRG+ZCaQJAADAEojeMhNIEwAAgCUQvWUmkCYAAABLIHrLTCBNAAAAlkD0lplAmgAAACyB6C0zgTQBAABYAtFbZgJpAgAAsASit8wE0gQAAGAJRG+ZCaQJAADAEojeMhNIEwAAgCUQvWUmkCYAAABLIHrLTCBNAAAAlkD0lplAmgAAACyB6C0zgTQBAABYAtFbZgJpAgAAsASit8wE0gQAAGAJRG+ZCaQJAADAEojeMhNIEwAAgCUQvWUmkCYAAABLIHrLTCBNAAAAlkD0lplAmgAAACyB6C0zgTQBAABYAtFbZgJpAgAAsASit8wE0gQAAGAJRG+ZCaQJAADAEojeMhNIEwAAgCUQvWUmkCbwnMxgatOmDU/v5eeVQrWM5U4QvWU6jR49juziAACAW8a0vbO/2zuB6C0zgTS9oEWLFrnmq4Xn1PFtlwNpwdFrmhoKOOlLqVChQjzP+B1TCsnHUcbiLUPavM3X20+nssVBHrOp40PSvIuRTRyQhwRO7UXXbtbKtsv02cdf3Hw9dxQb9frsYzqaL95Ehsvvzyj+O9LECQs87PvYf8FRsdgrWt/jY/p3W1ARvWUmkKYXsC+XT+EiVKSI+zwz0PlFrlNM+kL6lLjrWkC7v66qkaZM5u6vTfz4kqmw40db9Mm+4kCPueXSzD7Nl7HEG7PEIV4xtE6xPKnnTnJ6aB35d1DiDXHQHSCNL4v4GxTzzs930R9XB7LsfCjhpjcumVTE699twUX0lplAml7AvqjPDj4hFrslcFAD8m0+WSwu8OSVNJOX/Zf/8Ge3ryS9FhUHe8wtl6b0t6fBg0Vo8vF0cYBXJAcOklrlPqbq2dG1ivQei0ibuNuBvCGt+vVucQDZkwOpiE8haj75uDjoDiBL0/w+ivxN1ypFqFCRqmIxh30fi/s2F4tNAGl6G0jTC7yV5t1KXkmzTOFCdE/jSVJXKm9xmhXCrZfmnSe/SDN/YV1p5h2QpreBNL0gr6UZGbiM+vf3F4s5qTGHaNzwweQ3dAyFRKWIg/OejMs0d+KP1HegPwUcUE7yMSZPpHllMR9/QrSsug/LFqavdmYII7lycvca8h/Ql0ZPW0Spjl1Tnkjz0qFfacSgfjRx3lqX8c7sWkmD+v5AY2cto9yXwBh76jmaMW4o+Q2fSBHJ3m/G445tld/X5NmUYLAQnkpz2sjBNH7hPrGYs2buROrbdyAtCjggDhK4OWke37GSf49W7woVB7nl3N61NFR6/3sjksVBOWBemluXzKChoyfTKaOVzUmnJTPGSO9jKC3fcUocqMeeSstmjaOhY6ZTVIr47XKDNM3CGeOon99wt8t/M9I0+p0YA2l6G0jTCzyXpvPkmCJVv9YNCehQQSovQdcP/ciHG4lmUFNfdZgan2K0MSZLM9Y1Po8yH6zQlDFsVMxHnmajcP6D/fJsXt59j37T+1yZwgbzK0LLIzP5PF6dEqsbPy+kuah1GX68V9nEXF3ahor4dtaNo+XEvI66E46ULDyT7kaaGbws/dwqvjtRnI6Ne+3IDMM6r2tqSV/1oVr+9W79eqsgtZSLNZpIO4a+5VJHiUf0ZyTer1kGXT32OCpV2HUZfEo8zAdnbOnkMozFSQZvpb+3KI0alZU/x8Jl22mGS3/ATsyjwi7rwIe+Wh6pvj+FigbLUvTxXnzYh/c7TxwxEuomv2Yu07K0GRMkjkodKkjLWqwRxe8Y6vIZ+JR4hDzbge29NOMCerosH/seBiU5zRLQs7brOFKa/xjkrIiTRU19i7uM51OsMul+qoyMAD5sojTgrWr3uEzTZrZWzPJnKo7zeK9gPlT9LhkKNdVlfbI8UPcrYtulQoWKC+dYQJreBtL0Avbl80yaMlkh37uRZjEqIUnQiHaPspNFfEj/m8ui9x4pwcu1vFhM2ogVe0ZXZo+dzscrKW38HusRpBu2q9vDfJj2tIjwmc25IJedSdWUEoUt78WPv90aadqptPTDL/7SGE1RkjR9YTI6z5Evo1R3uQY9hSFsA+FDwz5xJ022/D7U9RftBslOr5UvTA82YKLzoY5ztGcg2ql55aJU7Mk+mjKZ72sWNZSmj09h8ilcRld+cl5bvrw1e+/VlUtfCF6uraeTr9SaKFyarmq2ZLbEg/RAMV9nAeXU0pQ3sE8+X4uqtJwoDqSs8Jl8nkXKNdCVp4Yt538mhvi3MfjccmppZlFRg2FLP6rK63m171pd+cKudXn5099s1ZVzafpI319p/c095mxdXj85j3/nitXsrRnbHd5KM42/r9IN/JxFtkSq+0Axitesf1ZnAz9ZUApzvqxLbVfGa0ps9Cj7/UnCDYzT/Fqz4uiREqz8Ht1nqkizsPSeyzzXUSeutjXk3/Ze4Z9CTi1N9n10HZbFv5NGv5OXyhWh+xoMIUjT1V3eBtL0AvalL1aqPFWqVMklQa5bsxykWYi+3++6W+haQEc+bFKY+DdV5qX7fGhoqHMTsasb21D5kHaH1uLWpcmn+Es0p/l/JKE+pxlC9EpxSSLFGzoLJFGxDW6gm5MLr+3uJW8I81ia9qSFfNxRZ/WaY2WfbdC282TYMhZ/+luxmKMsoztpLj9vsEnl8vKhDbEGu9KyT/K6RNxKs0QNw432W/+RNpxFa+oLDaRZUhJXiRbzNSMZk5s0CxV9QhxA7E8AX8biT4sDZK7tVlsleryTpj1xBa+jzkDj3b6/dnyMr+/dmn9EsjRLUIzBypv9lvTdLVRU+ONohCxNoxR5TBSHxI1lfNj8XPYAs3FyGYUCOrLPozAZ/1Qz6D72udYdqimSpVnjc3HPkIQ9nn8ONfvo15+30lz+Idu26P9Ya3mqONtTAGnebCBNL2Bf+pK+T1PdunVdctDgx+NemoUNj529UVKS2r1NxGKV7GN+VKRKF2fBFVk+/Q45Z/5QYXYN5XGyRU/gP6Dzqhdu8I1r9d7O410Xp7zGp88JNjyvpbnw3VJ8d7OorP9IG5rC5T4WSu283uMGG1eFZ9mlPYbSLGYoNLbhNxYQI5t/PiLupFms7jBdmcL0Jmy3XQl9oYE035L+CBUqXErfKjEgN2mW7xAgDiD7xSl8foNzWHl+z8qXwejxTpqjG0h1+BR3+TydZPBp/tN8rloi756tqxnHSdz0JnyZXP8+icjSDAwKoiAhew9HiSPzXeFMTqVeGCAO0cHqfGFAkFiswc7/7NzbZJo4QOWY3zP881J/5w5pDjtt9FnYqbg0rMS7v+hKvZOmnUpIy1Ts2cGaMj3Zx/0I0nR1l7eBNL2Afenzaves6wbGRsWk+os/8S59++23xun1hbRx+o9mmmw+zX0tF8i9mXv4MsqtXnnYO/MT5TFPD+PDVmn2wo6szzZ2pZwFBuT97lk7lXI5vqZNYf2/fNvZXJdx5QelDdbpnZXmzKaeSZNSDqrHoB944g3aH2t8NC83aTYcHy0OoLMj6xP742S0y1shbeUHfN56vJPmU0WlPzsVOjhHMaDFvexQwotqf07SvDyzKV8mT6Vp/Bkbc3C0XDdbL0v267/XCqObVpTHkf7YdR6xRBwsfScj+PAn3u3h+ht1pNcXr/BxFiu/t1stTfY7ker4YEWOnzZBmq7u8jaQphewL+Wtk6Ysuf80n0xhYWE5JFw31coPH1DrG1G3mNRS+0Qdtqf7o1IrphLv7ly5iMtGil9sX7isrkyEbZDzUpoJ89/h4+0zaJmT7bx8clPrRc4ydmOBXJZxfbuyBuu0gEhTQ0rEDnr54ZJ8nKIV39QNy02ajSbGiAPoFL8RQeEcT6pJX9/O4HPzTpo1JGkW8e2qGceVNqxFrfn+3Slpavn0ZXaMvxD5FK3oZh3ZaM7ATx27sH1o0gnHWNmn+HTNJ58w+H3qk6hUfKul6VimT9cZvxMZnAgkestMIE0vuLXSJKpbTPoBl9RvLHPDFjWeL9da6Q/mPVKLpeUCuWXJSfuVD2OCYkJ+uOsO5zCJ8B/llkhOsOnzUppvszMwizwiFqs0KclOoiil+WHb+DJGGa0wB6+wEy9c1mnBk6ZCyr5+LuvSjDRt4fIZ2hNyWHnjX2EnoYifm3fS9HuG7bG4T9gYa5HP6C7RyHmiUn6QJidlH5dihfYbxSE6arOWcuEKjj75D27JN3/SjZMjt1qajj1VJV6ZoCnTI28rIM2bDaTpBbdampETG/N5LL1kvPm5tPwj2h59QyiVv/R1hrJ/mj50QZiU3UCgzlD5NnC/XNUPI1s032CEG7X6JLLOyELOS2my+VXpsk0sVrk06w1ezxzN6YxsmtKvuZ4ZylCW0XWdFlxpKp+pdiwz0mQbUnZCSuHSr4kDZLLO5MmJQLYo+dhp64UXNeM5OTW6IR++QnNZR76RpsQjRdycOKQhsPsjfP0rTGzM9ggUITc/VVr+kS91nbzdWXDLpUk0pcl9ht9dhcalcCKQ6C0zgTS94FZLk/14nmY3UfZx/eIfm/sFn/8JgzOI2pT2ocJlWhpuhNiZiD73vGJ44g0j8PtnpX/Q99PxFP1PKYVd2yfNL2+Pacon9QTkdNjFcSbhfzT3Zw3xky9bqPX5HM2IMmwZP36rvME6LRjSrHyPL50T/geFTpEvsdGyt9fjJJ4pLZOTNKXPMfB7Xtf9tT4XBpyg+6Xlb/2JfNKNHlmM97daJJQzXKXJGPYSO67sQ71WRejKT8xrz+t/6O3ZuvI7IU3bxUXk+8YgXVlaqCz8esNPK2PRG4PEVmcaPVSEnYVcz1lkT+Z7dnwKl6Vo4Tc594tneZ2Nx2q2FSak2etxSYw+9+vKFIykKX2odK+P8e+kfa37qUil1gRpurrL20CaXnDrpcnIpBfLFeXzYhsh7UXpj707WhyZI5/wUYie+OGgOEjdfVvkke7iIJXyRdk/UHkeRYsqNzrwoW/WXshTadrjZ0uCLi8Wu/AO24Xrc6/ux715wGvqMrI/FUoLqfPyqBxvbmC0icpP0tSue3ZzcaW74htjNRNKn2PMLPVz0a/nnKXJOL/uW3V9FS6qfLcKUZ1v1rrc3EChWWn5e1C0sI96cwMZY2kyxrepodbNplO6nzHYiOelNHNLi/nX+NjnVvVU14OyHvmyVtTcfD7znHNaHx/yUX5/PkXpsLhAmVFUTvP5OesuRO+O1l/naUaaMbMcN4vwkbcDys0NGMbSlMg6r1l+5++kcJk60jcbxzRFb5kJpJlPCVoxndp90Jrea/MRjZq1OgfJ5g0pkYH0badP6O1325D/tJU5HJ+6k9hpxbRh9H6rd6htx16070JOTdaCQ9bVCBr6XTd6t0UL6vytP51PM1776ReDqdNHreib/qPEQR7h/20nevvtd6mX/zS6YTwLHYtGfUetPvqC5gQorTBPyKKFE/zo7ff+S0MmLXbzp+XOErF3FXXr+Cl90vlbCj5v/B3au2o6dfz0fXq3zSc0daUgQIHUqCD6/st21Oaj9jRrdc7jesvF4EX0kfR9/+iLbyjgtCz/3LHRsin+9P57b/Pfyf4L4iEd6yJ6y0wgTQAAAJZA9JaZQJoAAAAsgegtM4E0AQAAWALRW2YCaQIAALAEorfMBNIEAABgCURvmQmkCQAAwBKI3jITSBMAAIAlEL1lJpAmAAAASyB6y0wgTQAAAJZA9JaZQJrAkmQdGE8tWrTwKD+sTxAnzzMCp/ai/guOisVek1f1AHA3I3rLTCBNYEkyNrbn93rVxXG/VLG88ST393W9WZT7oCZ4cFs7t7BnjjrqAQC4R/SWmUCaADg48MMTt108DR4sQsV9m4vFXmLPo3oAuLsRvWUmkCYADu6ENAEAtw/RW2YCaQLgANIE4O5G9JaZQJoAOMhNmvwZkCXeo0M/NlKfWVi23QbNGKn0XBnleaTOPFD3K2lYusuzSe9XntUoPhfR8ezF+B1Ddc9oVJKuGVV5HqZRPfIzKxsZ1uNT4hFdPQqZ0eupmOYZrkraTDpImbu68e4jWeJUABQMRG+ZCaQJgAOPpFnsSfIpVoWSXU7cyeIPpS7kU4SWnUnVDXmpXBG6r8EQF2kyDB8m7JAme4jw3GPJukFta5SgYjV768oYRvXw5fVhD/TW13P95Dy+LGI99rg1vLzIg/Xpmub9pUcHUHFJpJ0HfQZpggKN6C0zgTQBcOCRNCVp7M8QhxAt/7ACnzbQzXOCnyoun5nrjTRjjJ7gbI+XhhUl0VtG9cjSLGFYz+y3/uNSz+NFfaQ/BE9pSjSkH1Vbq5AmKKiI3jITSBMABx5Js3B5sZhTQmqJFXt2sFiskn3cz2tpGmPnw64LpUb1yC3juroyhbjpTfT1XFvG+wfkYMTxr5SANEGBRvSWmUCaADjwSJrFGorFHCaTD1akicUa0rzePWtM3kjz8symunqS5rzJ33uKbiw9GVs6QZqgQCN6y0wgTQAceCbNRmIxh8mkZ1CmWKwhi4rmY2mGj6wv9RehnN5B9rFBkCYo0IjeMhNIEwAHNyNN1oqsO+y0WOzEcdee/CrNzK2def/hHIQYPb4hpAkKNKK3zATSBMDBzUhzSpP7pGkLU7gboTQu5f2JQMbcGmkyKhYuRD4lX9CUaMg+R4UL4UQgULARvWUmkCYADm5GmkQpdC+7vrHw/XQ8RX89Svta91ORSq3z9TFNRlb4dF52b433yaYpp7QwKiMJ9dW270CaoEAjestMIE0AHNycNCWyzlP5onKLkqVoUfkSlcJl6lC2wc0NGEayu1PSZFzdP15zIwTne3nq84W4uQEo8IjeMhNIE4A8JiUykL7t9Am9/W4b8p+2UhxcIDi47idq90Er6j54EqU6Gs7paz/m0ozUNUMBKDiI3jITSBMA4BH9ahWjQj73kMvNkAAoIIjeMhNIEwAgYztLr3+/SCzlbOzfmLcya/sdEgcBUGAQvWUmkCYAgGO/PEs9hslPCCr1IN1TxHlc84XuK8RJAChQiN4yE0gTAACAJRC9ZSaQJgAAAEsgestMIE0AAACWQPSWmUCaAAAALIHoLTOBNAEAAFgC0VtmAmkCAACwBKK3zATSBAAAYAlEb5kJpAkAAMASiN4yE0gTAACAJRC9ZSaQJgAAAEsgestMIE0AAACWQPSWmUCaAAAALIHoLTOBNAEAAFgC0VtmAmkCAACwBKK3zATSBAAAYAlEb5kJpAkAAMASiN4yE0gTAACAJRC9ZSaQJgAAAEsgestMIE0AAACWQPSWmUCaAAAALIHoLTOBNMEtIJOGdv2Qnv2/56l93ymULQ6+ixjj34+az7sqFt8UP71RSijJoho9g4Sy3Fnp/wOlCmVJe6bThmibUKonuFdN6RO8VWRS/WdrUesvh0rvSqZXzRq6Mbzh3K8T5Y707fTaoLV0+KJN3w2ABtFbZgJpgjynYb8tuv7J71ajY+m6orsHe2Iu0symDLEoF/JKmu0rPkZVO2/WlNipou8z9E1gzkq8ldJsWe45tft0gp2/3ow04/ct46/Zp4fRBseK1nYDoEX0lplAmiBPubb+c7GIU/PBVmp3xMFdFBKWoBnqGbsD1lPMdXlDq7ApYEcOG/gs2hWwgWLT9NNQZpLh/K/HHKYdh6J5d+KZvbT9oNzNscvtokBpGaKSNS0YQZoRB3fSgbNJzuEG0nQdRyIjgTZt2sVb5e6leYO2Bjj/kCRGhKrdjAunwnT97Ss3oPkty9F1R3/Sig9p+9VdgjQzaMemTZp+pzSP7w7QlTMSwkNo16EosZjs12MoYMchtX/j9oOaoU5qPdBSLFKluVv6rETCQ3bQoahksdgFSBN4gugtM4E0QZ7S58lyYpGOyk9/TrLCrlPdyvUcpdfprTlXHN3OVlWvmjWppf9G3v1UtQ/5a0bMFkrjXZnk++RnvOv0gs9pWpiys89JuznH+Ou1U4vohSEHePfRUY1o3gm2EdbMPyuYKtZ8TVKSRHYsvfZcE+IN46xoeqDZTMcovajl2L28OzN2Bz3SVm7hOKUpL4/83lLpqSrN5OE6aRqPc3TkKzT3uCyG8BXf0Gcv3a9OIZNFj7XqQGP2XuZ9r1d5nNeRfXQgrVB9kkmPfaX/HTJpkj1OKt/B+ys/3k0abbcqzfSjI6nd3OO8+5uXX6L7Wy7k3cG9qlOjrr/w7rcqPsRfGa9UepKU/wtsfJksKl2xJkXIK49qlnmemvRj8suiag8o68CJ7eJ68lujl3uv6qWp6y8neXfFh/7rKE2nSk+2I3l216n9y451In1WTd9pQmFX5fcQNfZl/gppAk8QvWUmkCbIU7o8XFUs0mDTH2O7sZW+289k50aa1Z0Cfr58Q92x0bOjXiRt+6NNxdc1fdKcIkbp+jMz2dQ2qvTxGmehMn9pQ9wzyNn68g91zqlVqUb8lUlTS/iPL8gtOIc0xeWhq4tpeixXmypNo3HYMpVrs0RbSh0r36vrZ+ukZONJzl5bGH28hs1dmrbpDF6UsvZTOiscwuPSlFjUuoL0R8NOu9m/DY0065droxn7Bt2rStO5e/ba/Bb81RY2gpbo9kJzS5K463jj5xXVz2lxK7HFLGNLPEiV7q9GyY4dANrds/NbyHIMG1GftLNT14n0WX2yVpk3pAm8Q/SWmUCaIE856V9HLOKM+tKf2K5A3XbdnkAt5smtPkNpCse6jq4eR+WrNeOtrHWfliN/f39nhuolmbHuU12/TAY1HKfZtajMX5DmEI00W7uRZsaWTnSGjeaQpsvySFkTxkZwStNoHLZM9YafcVYsMa2Ja0uzRo8gTX8G1XdMs6ptZS6pN6vKLXEtijTJfpmq1X5e7tZIs0K94Y4x+UialqZTmqkL5d2pbH3y96ui7PLWSzOgg7w8jKWtjaUpY6NSzwziXdrPeWFLeZp1n1bQ/UlS14nwWUGawBtEb5kJpAnymGxadE6/qzRhaw/yC5F3qk4669wUXpjXko7wUTMlKeyRCyUJvTr5Au8UpclJ+ZlmJdills9omh3jVPDoybs1I0lkn9FtdD9t2IO/NnyoiVqmzt9DacrvQKZrjYflDoc0xeXJPreK4rlXnNI0GofRUGpFO7FR2cIlNP2MLCparJbad21bV9qY4ujJDKYeuw5TnxDtcUoZVZpaNNIc/VI59QxWW8wcKpGDNFnrtuEYp9zZ+DLeSdO5lDYq88JI3mUkTbauxpxxfo/UdQJpgptA9JaZQJrglpB2KZRWrd5AF8WTcCROBW+loNBLYjGtWrmGkly3/TIZCbR21Vq6qmvtkFS2hhLcbiBv0Ja1qygqRdhvmR5vOP+ckFuadtq1cZ3+RCCB0KDNtGmvvuW4efUquqxZRqNx6EYcrVu/RZWYIfZU2rhOPsarpYmvdjert9ygzevWi4VuuRQaRFuC9cckvWX1Sml9eHg2NVtXwWGJYjEAphC9ZSaQJgAeIO6ezQ8kJ2fQ5UB/GnFS+CcBADBE9JaZQJoAAAAsgegtM4E0AQAAWALRW2YCaQIAALAEorfMBNIEAABgCURvmQmkCQAAwBKI3jITSBMA4B22C7RZc70pAAUF0VtmAmkCOjrwGSr3vuNeqjeBPSGYRo8eTb2ChasN7UlUrVpl3W3RRNo8UpHCw4/Ru9UfJMfDLygrfBY16buIvm5QiWId2+isiHlUr+MEdVxGRkAH+mHUaD5vlrWnc7zaUSXt/GH1vjZaZr1dhRYFhtKcrxvQSmXGlEbf/rSZwo/upJoVnneZjs23Q937nddZZkVQxXod6WR4OD1Yq5ujMIMeeq07H7fnp02oQS/5+sj25QvTOPEeeFnHDJ5GYqf7m8/T9MbT2z+nUPbZjfJ7H/Wdug6SHAu4aeAb1Pr7yXQ6IoLav1SF5oUqt2/PBXsCr6d6r2BxiMsNBvISZflZyhevKQ7OlSMDatGgY95fgnN4X7hYBO5CRG+ZCaQJqNYjXWh0g/IuIjCLKM1etWrSpelN3EszI4D81A1dKj3VV35axrPllYv2bfRAY/m5iR0qOx8txcZlc2LSFJ3jCaFDars8gYTRZrHzYvpXH2jMX2OnvqaWUcZm6i/fykgHu02eUqq9M07qsv/SIT4gg574PsRRSpS44F3+yu7c82Rp+c5DCkNql/VYmirZ8k3PFc5ObkI7ruo/1aPDGtABD28swLjd0lSY2LSK+ufpdlC7cgexCNyFiN4yE0gTULedGWQ7O4rmXnZupUq9pdwmjahmjZ6OrjSq8VBNmj7/Z3q+83Iq03C8Oo4WrTQzjw2lJXF2istJmpRM4/c7blKXdZjeX36N2FMuFHkyOvtW46+bBrdXy9i4DC7NjGTauGolxRkJwX6NGlR5iN55pxk99bYff/RW9lE/Kla0MBUvXpwGHtYLUBaczJbOvvzWb1n7eqtl2Wd+pDVsESWJ1Szjq8pRK83kTYPV2+4d7l+L+OiCNDO2dOavTJoZIT/Q5HNKc/oENZkSddPSLF/ze12/wuVrYr2SYK/8KxZx3Emzx8ZgavZOcyrl28T5Z0tazy9XrcjX85QQ5V7C2vsKy7foY/Sq+Ryt6fMmlWn9izpMIWRIAzpo0CBmN5jYEDSZajVqQTXKlqXIrBvU+NGq9GiZBymafwhXqOS9xWmN4ztQs0YPqvmi9JlXKEXbHd/t67+8S+pdjqX6mPv9apekwj5FpO9CSV5+fG4XqvnSm9TwSV+ae1x5xICdmlatQM9WrkB7r9xGm4M8RfSWmUCalifTcT9QG5V5Q34MFsNImoOe83VuINMCqViu0rRRtaZTeFfO0nTyUdUq8jxskbqN7agX73NpCbNxGdnhK2ljhKyo86s70eBD+vZjo/Ivafps9GBR+T6mxi1Nm7pRZUSMepESHTMuXcqX6v1fNWo5VX6cFh9++JTarZWmliofKru+M6jGV79SbGwsHdo8h8pUb8dLlXvE1npAflKLf91y/Mb2NydNaV5GwjPAdnkdtXz3c7GY406a7y+VH1Mm/fug/y6TDdfoIblVzoiZ04KO8pXhRpqPF9M/8UbD7s0bqdd7T1Pvrfrb5zHJLVX/2NmpZM3uju5sKt1yAe+yRY1VpVmj0vuO4UT/V0Z+5JiRNBnaluaoU871fnLkyxTHZpk8jxZoVjUomIjeMhNI0+JkBnanJ554gse39H/Up5AYSbOy7qkYRPflIs0VbX3pyMmTdFJKoN+LtP+kviUksvD9ahSmbq9SqP6PzuNMvWvKxy8V9OPqKV9de8s7908RMZYmUbhmV+++3jX5OPFLnRvg1AODafRp1+NmRtKMWuicTmxpKijSzDw8gGacO07NZsbw/puTpo3uazJN058zqcYNTbfSdO6eTaUm0+OIvTfxCTLyc0bdSLNmdbXMHb1rltf1ayXHqFx7iNpdqpG8+14rTeceEqKWpeQb9ecuzQwa5OdHfkoGdaHOW+VvydevVKE9Mc7HkoGCh+gtM4E0LU61ql86e2znqMHoCN75eA35qSBsQ1321cm8a9ab5eWHM7NRo6ZT8VykqUXb0jx6MFI3jHF2biuxiD6p9LjcYU/UPEkjk6o+pn8M1ozXy2geOZZMVTpv0Qwleqmc8VNE3EnzccdDm9l7r+TY8C79b1nnCFmhkiDOOfsdiNJsVfUx3ZNWcpOmiKs0ieqUcT6lxRY5gSZEaQwv7J7NjphJHy3SL2ePZ8vrntaSG55L080TZEjzBBuJ+e/I69HwCTYSa9mT4hy8WVb/mLm8kCb7k7jH8aEnzn+HLjgartqWpvgkGvlpNQop9MasBG0BKECI3jITSNPK3Ngi/YvWHwRsdH9d/pp+ej6VfbwB+T7wMDkPddqpfb1K9Po7LanXykgq/coEdTqG7dwEKlmyJBW7p6T0+oBumFOamVSqSBn9rtbsI+RTrASflqXMqw4Z2+Ko0oPVqWy15ur4A2oVU8djieTbt1R6pnw5avVecyrzeEuX3bhMus89VJ5avvsWPd7kW5r1hvz4qazjI+mZN96jUdqDmBJxm/pQ9ZdbULWyzgclM9k+8Gg9avN2Y3r0deX4po1K+BThu7fZspQo6sNfH3h/KT+Ls4RmOcfzBb15adKNMKr1SnNq0fgZatJbfrSYiiBNRlbsLul9PETvtmlDD9f7wHNhSn+g2HIXLnYPf9VN50aaZL9CdX0f4ut5dKBTLKfnf06PN3iLmjzvS37b5d267qTp/3YNevWd1vRomQfomLD/Ni+kyfj82QfprdZtqKnfdrVs5Etl6b2W8u7xoLEfUY0Xm9Frz1ehz6Ye4GXXT8yhMr7PUdVyjxL20hZcRG+ZCaQJzHF9HzWfEyuW5o79KrVdHC+WAgDALUf0lplAmsBzUk/RO/Wr039KlaHuUwPFoQAAkK8RvWUmkCYAAABLIHrLTCBNAAAAlkD0lplAmgAAACyB6C0zgTQBAABYAtFbZgJpAgAAsASit8wE0gQAAGAJRG+ZSaEzsXG0+Lc9LgO8DQAAAJCfEb1lJoWiE/+iqIQr9Nvxk7TAYARPAwAAAORnRG+ZCZemklMXLtGKwGCXkTwJAAAAkJ8RvWUmOmmy/HE5iQJPnqEF23a5jJxTAAAAgPyM6C0zcZGmNjuOnXSZwF0AAACA/IzoLW+ycPtuOhIZnbM0WdiJQqv3hrhUIAYAAADIz4je8jTbj4VSZHwid2Ku0mRhu2wPRvyR4y5bAAAAID8jeiu3LN8dTKExsTofeiRNJRFxCbTt6AmXilkAAACA/IzorZwSEn6O/ki44uJBr6SpJCw2zmUGAAAAQH5G9JZR2KWX5+KTXLynxJQ0Wdi1nav27Ic0AQAAFAhEQYr57fdT3G2i77QxLU1tDkVGicsGAAAA5CtESbKsCNxH4ZfiXbzmLnkiTRYAAAAgP6OVJbt97OHIaBeX5RZIEwAAgCVQhLkqaL+LwzwNpAksyxK/H6hPnz667LxsF0czT1Yw9QzK1Bed+5Wis4jC146hGiWbq68FhcSf3hCLACgwLNkZJLUuo1z85U0gTWB5TvrXpnSxMC8wkKYtfh8lOLz8RilZlsprQQDSBAUZ0VtmAmkCy2MkzcykCNq0I0RXlsVkl3aR1m/cSTbdECe7A9ZTzHWHFQ2kqcVImvGhu2nHkRi1X0dWEgVsCBAKM2nXpk2UkCEUGxBxcCcdOJskFutIijhIOw6cFUozaIc0j+RsSBMUbERvmQmkCSyPKM1RjSrTiWRZfCu+rkvBqXL5e+2b0d7LWbx7h//rtOyiXp1PVfuQv2bEbKE01uGQpj1xO9X9disfZosaS2scMxOlGdLnKYrh1WfQL4d4DSonJzShOceu8u7nKr/AX9OPjqLP553g3dfDV1C9gcGSQ/dSu3WOBZaoXa4Vf2XTy+8olZ6q0swxNItqNn2HNobJ9TbxfZJSHL7//KkqxBYl/ehIajf3OC9j82j/2UuOaQEoeIjeMhNIE1geUZrjovQybOqQWg+h1dipSj1d/5nFX9MjjdpRzA1HgSTNMlWq087rznFykialn6Eq5R6h+XvElmYGvTz2nFBG9FDDcbr+hFlN+evkV8tyQd7Y9iXt54ucQZVe7UJ+fn5yBnWhzltZ0zSLqvfYw6fJWN+OugxyDOcZRL6dt1KFesOV6jmXpjXR9QNQkBC9ZSaQJrA8ojQ/WeNsqTGq1ezNX1+drJfZCw99rOtXiJzbivYwWTlaml89VVGtP0dpKmRE0uMOmclkU+VP12n6ZepX+kTXv+3LavzVfmUpDT2VTR9UbugYkk1VOoi7dRlZVKNnEO/KPjOcAhTZa6hf/r+6/s2dKuv6AShIiN4yE0gTWB5RmkMbVKJTjv2Ua3rWp8BrcvnbH71GIYnZvHv3j81oqW73bBZNCozjXRE/taRDbN+mekzTTtUryi20nKS5aNgkeUBmBNXqd0judrDfrx4tOCkvyAu+dfjrjUNDqdMvp3h3WuQaer5PoDr+ozU+ptaLEtX+kMH1HbtnbfTJkxXl3ccaaTLqV65NyuHYWZ88SQfT5Hl0WHiSl7F5tP3oRXV8AAoaorfMBNIEwID0+FO0fnOQrowfn0yNoXXuTgTKSKC1q9bSVdmrpti7aS0Fh8vHGF24Ecfr15NOW9evp0sGrUSR0KDNtGnvGbFYx6XQIFqzaa9QeoM2r1tPifLhXAAKLKK3zATSBMBDcjoTFgCQ/xG9ZSaQJgAAAEsgestMIE0AAACWQPSWmUCaAAAALIHoLTOBNAEAAFgC0VtmAmkCAACwBKK3zATSBAAAYAlEb5kJpAm8wm63U1JSEiUkJCAGSUxMpH/++UdcbTfN1atXXeaF3HySk5PFVQ3uYkRvmQmkCXLlr7/+ookTJ9KJEye4NEHO/O9//6M//viDJk+eTFFRUeJgj9m4cSNt3boVG/ZbDFu/mzZt4gF3N6K3zATSBDkybdo0+vfff8Vi4AX79+8Xi3KESXfSJMct9cBtZd++fWIRuIsQvWUmkCZwy+zZs8UiYJKgoCDKzs79/npbtmzxaDxw62B/En/77TexGNwFiN4yE0gTGDJnzhyxCNwkU6dOFYt03Lhxg65cuSIWgztAfHw8ZWR48GRvUKAQvWUmkCZwISsri9LTtc/9AHkFOy7sjpkzZ4pF4A7CjkmDuwvRW2YCaQIXbvvGOz2WgoJPUnBQEHn6II30xGixqEDw008/iUUc1qq5FWfdFizy125p1vLHrvK7C9FbZgJpAhd27NghFnF2dXuEFi1ZQkuknLhqp/XtKlBsHp1M+0mFppS+9hOKF+qLHNOQruuLOPu/e0os0nN9vVgiI5W/9VOsUJhCK87kvnFUxmlXobQwxHMuX74sFnG2b98uFnEyd3WjHxfJ65xF/3hsmZC5I8Qir2Cfo6d0e7gYDT4m/7VpMPKsMFQmJWSuWOQZNv1DvhU613yETgUto5aTI8RBXqF+X1NCyIOPm7Nz506xCBRgRG+ZCaQJXGDXGhqxq9ujmpagnTZu2MgfbBy9fxcdWTaOrrEe+zUaMW2VPEbyGUrkErTTpkOXeNmJBNmK62eOpLlbztKpXUG83500X36kM32yJkXtP7F+Jo2eu0WV5onEGzTOfwidS5OWY/fPNHy6LMtTOzfy1/07TtCBZZNo8sojavlRaSZp57bT0HFz+Ps5ErCAXhu4ms5nSOPvOkXzQuSHPeuW0RYnj5N+hTZs3MyHMzbPG0uTlwbz7uj9OyjuwDIaOnmlOtwIds2lyJgxY8QiDpPmEaH5nZgRR/5+QymRPdRTWq4uz5ahDb/KZ+jOHetPqw7FyyOmR0uf5RH+fqL3baefDYdd5Z8jY/vcUTRn3WF5uMTmuWMpXngaWrfHXqQPfZ/g3Yo07dfCyH/ICMe4NlrQ5Vnafz6dtofK36NjW+RLOewp4cQ+/mthm2nIiMnqg7/ZOl82brgqTfu1MxSp+adU8fGuzh5Spp9GyqIln9kk9U8hfgTSnkwRjn8WFw9udnmf7OsVsKALDVy9gbbuCXfUYKfgKOMHkrJLrcDdg+gtM4E0gQvursVkLc1f+fVssjTiZzTlG76JjSvKI2Ttoy+WHKZjx45Rr+d8ie1ue7jTZoqZ1IQO+9WR+rK4pGr+Xz+lSmr7UB3+aiRN29mR9MHgEfRKubK8v1fN/1OHrW77EH/tECCfrDGzqdJaukIfrJSWyi7L4VXfDnJx5jb6MdzGyz9Zm061K9Wm0CRHc8Mey8sYjSu246+Gy+gYZ4ZjXjU040w8b6OJr7L3zMikF39UNsiunDt3TiyiGTNmiEUcJs0dly5LLdQEtczxlqlz1Rf565TX5OXZ1/sJvu6PHTtCvl9skhw0kTY4xp3YqIzcIUmt0ucbdcPY50iZB6l2+/HqDtInanzB6zqysRdt0pwPw6TJ66g/nEsza19vWnKYzdM5buyU1/i4w+o9zEU44MBhGno6m36oxf7oZKp/vFKWf8BflXXOxu3etKbjj5aekR88TbNOZ/L3eJi/x2O0sddzpK2Pk7Wf/E/K7+Lnt0u7vE/2CdpjpxD7KG9s70pHpVFXf/wol6kRU6ZMEYtAAUb0lplAmsCFP//8Uyzi6FuaGmm+WlUuyA6lzlvkf+yKdzs/0pDeq/WNtDHbS5OPypew1K3WSR4o0ax0bf5qJM0fX6jMX7NPDaVFSXYaWreaOmxWM3kXqSrNN8o7hlyh91fkLk2GPfkgNZkao5Pmq1U781fDZRSkWfsReVzGAmn5PJXm33//LRa5PenEqKWpSPPLanpphvrLcldgwtiqSvM+R2km1egZpBvGpengoP/LFCOtpjrVlPem14ksTWktr23HpZkd6k+Oj5yUcRVppm/tTAfnvcdbhE+/PpmqtF1N7I+UMvrF6a/zV2WdM2nak7bS27OM112lusP4e3TOjs3PWd+NVKl5mnWABh2TpTn3rTIu71MrTSb/RzsF0BNdtjlqcAXSvLsQvWUmkCZwgd2JxohcpSmxZUBTavZCdRoTnMT7E+Y2p8/Wp/HuykVK8Ff75W1UucZLVO/J56lzzbq8zFWa2fTQB8sd3TYq+87P0oQJVN23BjWt+yTN6PokH2JWmjUqP0pv1K1KW/nu4gwq+3hDWi51Kxtwo2VUxlGkaU/aQ1Vrvkx1Hq3G+z2RZmyseDxVZvfu3WIRh0mzXKVKVMmRczZXae79/il6s5n0x0RaT083biGto6dIcrhemtKy1W7SgnwfeY23JkWZZBybRI/WbUJVq7zI1WeL20IPP92Ynmqj322sSJPxgmP37ICm1anFO83UcTP2fk/fLE/gn1eRCp/xss2dKtNkZmOJ956qSi1er0OdF5zm/VppMhICutKMMGXnq43a1KpIL9X0pYN8L72NmlZ/mN5p9gK1GSPvFm/6WGWpvrrU8We5vs61fendtxtT81H7Xd4nd2XGXnq84Zu8bOl/yxL7WrgjJCRELAIFGNFbZgJpAhdWrFghFoE8wt0xMnYXIKNjnXmFU+hAISUrm+pVby8Wq7B707LPBdw9iN4yE0gTuMCOabo7yxOYx2az0aVL8glRRkyYMEEsAncQ3Mrw7kP0lplAmsCQX3/9VSwCN4m745YK7M/K6dPyLkZwZwkNDUUr8y5E9JaZQJrALfinnXcsWLBALDLk7NmzaOXfYdglV5GRkWIxuAsQvWUmkCbIkc2bN7s9eQXkDrurjBkJLlu2TCwCt4GFCxeKReAuQvSWmUCaIFfYbqo1a9bQ6tWr+TWGTATstm+Ia9it8NjNvgMCAmju3Ln8Pr5miYiI4Lt0Dxw4wC9TYXWL80NuLqmpqXz9sktLjK6fBXcXorfMBNIEAABgCURvmQmkCQAAwBKI3jITSBMAAIAlEL1lJpAmAAAASyB6y0wgTQAAAJZA9JaZQJoAAAAsgegtM4E0AQAAWALRW2YCaQIAALAEorfMBNIEAABgCURvmQmkCQAAwBKI3jITSBMAAIAlEL1lJpAmAAAASyB6y0wgTQAAAJZA9JaZQJoAAAAsgegtM4E0AQAAWALRW2YCaQIAALAEorfMBNIEAABgCURvmQmkCQAAwBKI3jITSBMAAIAlEL1lJpAmAAAASyB6y0wgTQAAAJZA9JaZQJoAAAAsgegtM4E0AQAAWALRW2YCaQIAALAEorfMBNIEAABgCURvmQmkCQAAwBKI3jITSBMAAIAlEL1lJpAmAAAASyB6y0wgTQAAAJZA9JaZQJoAAAAsgegtM4E0AQAAWALRW2YCaQIAALAEorfMBNIEAABgCURvmQmkCQAAwBKI3jITSBMAAIAlEL1lJpAmAAAASyB6y0wgTQAAAJZA9JaZQJoAAAAsgegtM4E0AQAAmGZ1wG80ZOZqSr52TVeelpam688PiN4yE0gTAABArlyMvUQDpizn2fxbEC9buHKjWsaSkpLKy+et3s77pywK0NRw5xG9ZSaQJgAAABcOHztBAdt2q/0Dp67QCXL4rNW6fiXieKfDzqp17Np7kIL2H1b7bzeit8wE0gQAAKAj7GykKj2/6Stp2tLNLnL0NAOlzFqib5HeKURvmQmkCQAAQMfQmcatyLxK5Lk/xFneFkRvmQmkCYBJgoODqXHjxmIxAAWOib8ESK3JbfTrtkD6IyraRXI5ZbDUEhXLcsuPs9fSwhUbaPhPa3n/oeOh4iLdEkRvmQmkCSzJ//73P+rSpQs98MADNGHCBN7vDcOHD6eiRYvmmzMEMzMzxSIAPEaUmqcZNmsNzV2zk36cs04ty8z6ly7EJbmMm1tuB6K3zATSBJakevXqave///5LL774Io0bN04zhjH79u2j+vXrk5+fH8XGxoqD7wgjRoygjRs3isX8T8E14TIAAET+iDrvIjAxCX+l8Fd2fPJqynW1fMbybXxX7pzVO9Wy1LR0skt/QpX+WSt30J4jYZR6Pd2lXm1ux3dV9JaZQJrAklSoUEHXb7fbqUmTJhQa6n430bJly+jDDz/krbqGDRuKg+8IMTEx1LdvX7GYEhMTqUePHmIxAJylG3bStKVbeUbNXe8iMDEZmVlqN9sro3Rn22y8ZTlomnzGrN+0lbR+12E6FubcxTtkxipKdEg3p4z7+VfHMm2jmAsXxUXOE0RvmQmkCSzJo48+KhZRdnY2+fr6isUctht2zZo1fIPB5Mpap3caJvratWvzVy3sfVSqVElXBoBC5LkoF2GJ+VtqLf5+9jzNXvUb758qyeyva39TfFKy1LqUr8H0JIOnr6KNgUdp897jvFspT0vP4DIVx1fCWrS3AtFbZgJpAkvy9ttvi0WcrVu3uhzfPHjwIL3yyiu8+/jx4zR+/Hjd8DvF888/b3gss02bNnT9+nWxGADOoaO/u0hKm5krttPoeRt4t/J6MxkptWQXB+xV+5l8WYs06GiYy7ja3ApEb5kJpAksyccffywWqZw7d07tZq3L9957T23NPfbYYy5SvRMMGDCAduzYIRbTb7/9RpMmTRKLAVDJTZpDZ62mk5EXeLd2N2teZMmmYFq38xBvuYrDxNwKRG+ZCaQJLInR7lkF1lJjjBo1ijp27KhKcsiQIZSUlKQd9Y7AjmO2bt1aLObUqVMnX0gd5E+C9h+i6ctyF9aUJVsoPPpPGmXQ0mR3/Fmz4yDfVWtE1r/ZdOR0lMudgZTMX7ebhv20xqVczLgFAbQ2YAfFxceLszCN6C0zgTSBJclJmuwylFatWtHChQt15c2bN9f13ynY8UojMbKzeTMyMsRiAOh8jNxyvJks3bSP/pWE6A3sRCHtrlmz+T30tFi1KURvmQmkCSxJqVKlxCIOk1HhwoXFYho2bJhYdEf45JNPDIUZERHBrx0FwIitO4NdRORpxBPNzMLqMWq5epITJyFNAO4oRtK0Sf+Kn376aX7cUkt6enq+aGWya0Tnzp0rFlNWVha/dhQAd9y4ccNFRLll4NTlfFdrXrN13wmXeeUW9tvMC0RvmQmkCSzJvffeq+tXxBMXF+cioM8//5xvdO4kqamp1KxZM5dWJutnJzXdjgvDQcHlTPhZFxHllKGz1ohV5CmsfnGeOeXg0d/FKkwhestMIE1gSZ566im1mwmzXr166vFA7Y0PoqOjacyYMWr/nYDt1mKXvLDlFPn9999pxowZYjEAHPaA6P4GEsopt1qYCuwsXXHeOWXYzJXSn9d0sRqvEL1lJpAmsCSvvvoqf/3zzz95y1J7swJ2IhCDteLY7fXEYzpm7lV7M/Tu3ZuOHj0qFvPlYmfLAmDE9bQ0F/F4Erv99ny32XzEeecWv6krxGq8QvSWmUCawJL06dOHEhIS+DFM8e4+yuUcQUFBPFr27t3LT8a5XZw+fZrGjh0rFnPYzQ2MWp8AKIjSyS1Xrv0tVnFLuZKc6rIMOWXG4l/FKrxC9JaZQJrAkvTv359Lh91yTkS5XZ54WQo7rsiOhYotz1sFm8+zzz5r2KrdvXs3rV27ViwGQMfsVTtcxOMu7JZ5dwLlVn2ehLWebwbRW2YCaQLL8c8///A76oSFhYmDVEqXLu0iK3YpCpvWiCtXrtB9991HNWvWFAfx+9aWK1eO72b1BtYKNmLx4sW0fft2sRgAFzbs8OxSE3Zbu5wo2XXfTScnlBu+55Ztu/aKk3qF6C0zgTSBpfj777+pSpUq/HZz7qS5fv16OnbsmK6sbdu2NHLkSF2ZlnvuuYcLUzw1XjnJqEGDBnw3MBMxu7/twIEDc8yXX37JT/4xCpMzOybLwuTOnutplOLFi1OJEiVyTcmSJXNNmTJlqGLFii5hJ00VKVJEfb/s/eE2fvmDkXOdz7jMLZEXcr7rjlZ+D3YPcRGiJ8mJiPNxLsvkLiN+Mn+ikugtM4E0gWVgrcEnnniCb9jZrs9NmzaJo3CYVLXMmjWLX+4hClHh8uXL1LNnT7GYtwjZiTpnz56l/fv38/HYNaDz58+nU6dOGYYtF4u7p5SwE4Ju1+5hT/jrr79oxQr55IwzZ87wddeoUSNhLHC7GTffu0s6ckMR35Qdf6pl5Xt4J8/cEJcppwTtOyBO7hGit8wE0gSWgAnv//7v/9RjmEw8q1atEsaSy9m1mgoXL16kr7/+mt58803NWDJMvj///DNvhWlhl64888wztGDBAt7ftWtX/tBrtnvWnXi1sGOt4q5hBpuWtVrzC8pxX/bKWuHs/bFu9t7BnWXaotyfkalNbiji+/sf5zkATceddBFjTsmNib9sclkud3F3mCQ3RG+ZCaQJ7nqYbOrWras709SdNP38/NTulJQULin2OmLECM1Y8m7Xpk2b8mdrzp49m5ex+bA79rz88sv8LkJmmDdvHm+VGpHfHvnF/gywS3a6devGl1uhVq1amrHAnWLA5GUusnGX3FDEV73fYcrKttMfiekuUswtueHpE1UWrzHeQ+QJorfMpFDQmQjKiwCQH2FyZK1E8Y4+RtJkLcT333+fdzMp1qhRg4twz549/GboCkuXLqUnn3ySkpOT6YUXXuBlmzdvpueee44Lz6iV6Anx8fFcjEbTs1vorVyZ88katxv2yLSWLVvSli1bdOUnTpzQ9YM7w9nIP1yEY5RBuZwExBAFaCa58W92tsuyGeVmEL1lJpAmuGtJTEzkUjOSEJMmE5EWdrIOG/fChQv8KScK7FrNfv368d2OrCWqva6TnUz0xx9/GM7DG5gwP/vsM7GYExgYSMuWLROL7yi9evXiJ0eB/MmBw0ddZOMuK7Ya79nQoohvVqDz0IVWhEl/Z+l23TI2/n7FK2kyxGVzl5TUVHFSjxC9ZSaQJrhrYccw3R1DZJdsaM+eDQ0NVe+6Ix6TY0Jku2iNrunMC1j9RnceYrB5smE3K+W8xtfXVywC+QhRMpMWbaKEv1Lor2t/0/y1u3XD2A3UcyM3abqjcu8DNy3NwCNnXMoGTjHX4hS9ZSaQJrgrYXf7uXTpklisws741EpKEVP37t3divZWwS7RYHf+MYIdN82PN2PPbxIHekTJsGRkypc8ieVbgnO/Gbon0nxn8iledt9XzvJBa8+bliZ70LXyPfsnM8tluc0gestMIE1wV2L06C8t2ktE2KUoQ4YMoR49etC6des0Y9162LFWd7s52W7hJUuWiMUA5MqBw0dcJBMdm0B/XLzsUr5yW4g4uQueSFMZh+VsvHwOARvfrDRZFGmOW/CrrnxPiOu9mD1B9JaZQJrgroMdm8ytdcYuAVFgxzDvv/9+fsOD2w072cgd4vWiAHjDgUOu4jTKhIUB4qQueCvNU5fk293drDSXbd5HI2av5XEK84g4mceI3jITSBPcVcTExPCbseeGeG3lnYD9i2Zn3Rrt6mS7js1eiwYAI3DfQRcJuUtu3A5pxiUluyyXURas3SFO6jGit8wE0gR3FewkHiMJiXzzzTdi0W2H7X5l95dVnuOppVq1amIRAB7DTiATZZNTcuN2SHP1jgMuy+Uu8ZcTxMk9QvSWmUCa4K5h2rRpLtdjGnGrzoLNK9i9Z43OpAXAU0bNXOoimpySG7dDmuIy5ZSJP5t7wo/oLTOBNMFdA7sTjyetTHcn3uQXxOd7AuAt6exJPgaycRd2w/Sc0ArRbHKC3TBeXCZ3GT1vvUe/cyNEb5kJpAnuGl5//XWxyAV2GQq77RsAVmD2sgAX6RiFPZorJ0QBmklOsEeTictklOAD5k8CYojeMhNIE9w1sCeKaO8vK8LOkm3cuLHpf6kAFDSSr11zEY+7xF6+Ik6u0nlhJFXoecB0ui/9Q6xS5UJ8ksuyuMvNnhwnestMIE1w1xAdHU0PPfSQyy3n2N1+mjdvTh07doQwgaWYttjzJ4ew3O7fh9HNFnLK/NXbxSq8QvSWmUCa4K6CnUCjPGmEXXvZsGFDmjBhAk6sAZZElE5umbt2l1jFLWXO6p0uy5BbbgbRW2YCaQIAwF3KsJ9Wu0gntxw5EyVWc0s4cjrKZd65Zegs18f5eYPoLTOBNEGBIc1xpcjOmNt7b9ibJXq7/tFZKnZz15qZ5Uaer7Ysyt8X7wCFK3/9RX7TVrhIyF2GzlojVpGnsPq18xs4dUWOJwOt/DVv7tYlestMIE1QAMimsWedW/xvd2VqhuVEJs24JO+WHdp5jDDMPH06z+Cv2ceGkice2ta9q1jEyT49Su1W6vQWW5oHD6W2J5JfYBLv/KrTTGGgnq7jzopFOrTD5Y+EnXiVTeM0n4+enIaB24koIpblW/bzp5/ExLmejDNw6nLK+jfv/xaxp6qI82L5O839ZTKLVuV+qz9PEL1lJpAmKBAs7t6GTlyTBfhi54VE10Np5VWivhvPU2roPDonbZcHtWO3z7tOreu2c0yVSZ+OnE7Tp0+nVm0kQaXspg3n0yls+SBpWCp1XnhMqmY8SdVQp0lnKXb/XmmcQF5Hp0mhlPrLx3Qs2UbjP+riqE/muxaf8jqnDmzFpenfoS+FzuvGu9v12SBNHkZ12/2izu+d2sryEA3+vB8p9SeHDFHLtdLs0Hcj2VNDebe2vtRf2tP28Mu69394GBOy873YrwTQiTRp1gfG0uxEeX0lzu2s1s2R3uOvMRkUtqg7sb8fH7/YmULHfyTJNZ3a+7Obd6eq61WaKS08liwMl+ne5iNiH4k9PYn8Q9h1fqnUcep2SZMplC71DWpdVzdMqVNcxm++Zg9BzqZRJ/N+Aw2ciCJiSUvP4K+rth+gITNWuQxnyavzAVg9P85Z51L/leS/+bDImHi69vcNl+Es/jNWi9WZQvSWmUCaoOCQtoe/yC1NGw0/kU3f9enD7zW7KDSTBh+WLzfZ9JUiCX1LM2rSl45ydtu6VJKriSapGkqN2EId+iyVxvmKj7Gtx1eUuuhr3h09WX5V0Lc0bdTo8+/4MoRmRpFjEeirzovU+TmXx0ZDj8liYPUbtjRtUfT5d/J7Yt3a+pTl0b7/s+NYmfO9xM2Sl5+9xzkOaWYdHqzuRr2yd4X6Htn6WZJK9PW3u6RJJ/NxWEvSFjVBXa/STLlYtcO1pO35npytSXk5bFGT+LCMTWw+8jBtneIyZuwdQDeChlDebJqBO0QRsaT/k8lfJ/yS8/WcqyWpmpUnm27ppmCXOrVJuppKExZuomnLtrkMY2G7b/MC0VtmAmmC/I/9CrXtPpSGdJZbbFppdP1yAI0f8CUxPwSN6kizZo6hvm0VOQq7Z+1X6Yu+42nAt8NIL007de07lr5qP0IaJ1mqYxTNOZmul2bWXkedojSJgsd3pQFffsk3+qM6fkEzxwygtl8u4nV17DdeszxEe8d2VuvXSrN3k7e4UFZHZNP4rl/SrPEDeLm2Pk+kKbXfqH2fsdSvxxCa55Am4+e+XWicX3faEW/jy9Wp/3j6vmMPPkwrzc7vs5awXV2vojTl4TLdh06mzu3k8d/vN5XU5ZD6x8+aScP6sjsvKcM0dboso43q9neuX3BrmLpoo4uMWLQn5LDuk5EXXMZRwh5m/Wci2zeTO3HSeJMWbXapg4W1OP9K+Zv2HT+rlp2IiHEZb4Aky/Hz1tCNG2zfxc0jestMIE0APILbIP9ju0j+42fRoC7t1NZlvkO3jHaaM30AOf7bgNsAuz+zi5ykRF9KoGGOE3T+yXB96LOYgVLmr9tFvwYepZ0HT1HAnmO8P6cTepTEJ8k3XZi6ZCtt2GX8CLNbcTtJ0VtmAmkCAICFYE/VEQXFoj2e6O1NBzwNu10fe42KTeCvTLzBmtamNpAmAACAO05Ojw1bvmUfbdOc3XrDccwzLjGZluRyXNIo7BglOztXeYg0OxtXGbZx9xEaM3+DyzRKzB5DzQnRW2YCaQIAgMUI2LZTEtpWnqlLtrgIi2Xw9FVcoKlp6XT+UiK/BIWVZ9tskkwz+Mk5w35ao7YeWRZu2EMHTkRS/JVr9OPsdVyKB09GqsPZ/FZsDXGZl3Y4y7ad8kl/eY3oLTOBNAEAwOKI8mKZunSr2h2XlKx2/x5+nsYvDKDZq3dKAtxPwx2tSJZox25Xbf7J1B8fdddinbl4g7hYeY7oLTOBNAEAwOKIAtPJbMV2Gv6TLMaJv2ziJ/xs3nuc97OTgLTXd24J/p2fFKQV6SZpXE9ODgoOOSQuVp4jestMIE0AALA4osDcZZqm9cnyW8hJmrtmF01cJD9Nhe1aPXXuIiWnprlMK2bwdL1I2bHWW43oLTOBNAEAANCpM+Fqt7u7A+VVhs9ep87rdj6OTPSWmUCaAAAAdNhsNlVw/aUsXWd8kwJP8/Mq/clGt1OUWkRvmQmkCQAAwIULF2NpzZbdav/CNfpds+4yYZ6+lTp+wUa1jtBTYbR5Z7Daf7sRvWUmkCYAAACPUC47YZeaZGVl0d6Dx3SCPHHyNB/vYuwltYy1WvMLorfMBNIEAADgMenp+vvABh84QoOmraSTp8/oyvMjorfMBNIEdDX5hljkBjv175Pz8xhNYze4t6s9gfrMNN6VkxA0jYKvOfvtmamU0/1Dgqb1N6wvM9V58+nc6sjt2dfbdsbo+rV1u+NaunGl2deTxSKv8aYOd8vhQuYpg2eI2uiUwcfnSrZ8P1yDz0EL/6wksm+kCkNkcvucckKpm2P4XmS0686b9QjyN6K3zATStDi9Pvbjr+cWK49r0pMdOpxvWNKu32BPTabT2Y5ud2TLz4EUyQxiz7pk2pVy7ShN0W5l7Um06TpR/89GU+LcnmoxewoIu6G3Hjv1XH2VRnWVnxBiv7qariQtJPYo5sz9/fmyZp+ZQt26zHOMfpWk0anrqNOO+og6Tj1HEzv0o6SF8nMy9/f/jOyxs4i9q+xTP8qTXdlJQY7nd3bzG01JUqf47GvnOPKp8uxpIQraurXYE+fyxzYzoqZ8QUw4327Vr0+5nNTyKzuH8OdWUtYZWh8vrg8ZZRx93dLrNHn+Z6Z0k9ektg7p8zyUJS5HNvmNZuPaqPf2VD69dpmVp57oyaRF3G/KtDI9ezqegcg/g3Saes5G2Wcnqp+DO9hnlb5H/izZ56RF+znlVIeO7DM0upv8ebC6ZewG70Vefu26E9eju/UPCgait8wE0rQy9kTaodtqOB8UzB7q/HLHqZS0ZwDFXblOwyRJZSSHUMiVG7y7fb+N/OHIU09l6R7+nJ60h65n6+thaKXJmNChPy3r/qmjT6bd2FOSbDqS/8jh9P3K8/whzVduZKn9jMwQP2ljaqchXwzhG02/ThPU6bd9xx4dZqP+m6/Sd11laYb4dZJmmkFfDAlx1Pc3rUknurG8kzrdd+3G8nUxYkEAje3N/kTYqdm77emytOwxC3tILZtALs1W/ZYSZcSQX2CKbhxFmp/Xa8Xl3e9z+Y+IUrd2/dglwf/gP5I+/X4lRUxk7z+L2sxL0o0jlxMvZ62yd9v34gL56s2P6YeeXXQP0/6FyUozjr5uorAxTclui6HNV+183St1RLDP3SFN7XIs7NGfMgO/49L8ZlMynz5bs8zsodT9loZJq+FX53Is7cuXwzktsQ+K+CM2yfEZpK/lD6aW1rzjc8gm//byA7k7Tz3FH+RN9lSyOT6rtV1kyfHPSZqP+nBx3eeUQn02nOcPu1a6r4ctp3bSwuzxb8/nJ309qUf/zRT4XVf1e8Bg3yPte2EfqbL82nUXrl2PyWud6w4USERvmQmkaXG+bCdLJ/7Xb1lTjcL59t9GZ9Pl5zYqLc1xX49SW5qse7w8Iq0Ly6Z2o07x7t7PtZFbmkI9DJ00M6Np+AGpvaC5IfOEjnILc8mX8sZyVodvHS0SeR8s62ctmh9PyvNVWppKa6Njz5WOLhkuzcyD5Bhd19LsMu8S/dSZPTz5OvVceYEPT9/QVV62lLXU4YcgXvZpv33yxA5p9g5K473tB+0XxpFn0ub53vz1zLj2pK1bu36uLZGfrXlxVgf+OqzDYJdxOKn7ia2/H4Iy+Gu/fVn08cRzfND1fQPlll9aEC1M1Y/DUOpmdexhfnfA3p9Sx8cDD6jSZCjLwVDFJ8Gm1y1z6kKSV0M2ZeqWQx5fmfazH086CpTPII3mXZLEfeEn9XPoMF6+LnDlujDqOFHuZl8X9lmlbfue18M+JzYfBls32s8p4Z99XIpBvZ+T5iN3s/m0kRZmQIfxfJowx+fPpUlKS9PxPdK8l0H7ZROy5edo152jO2NHL97L1x0okIjeMhNIE1BYuOZYXGYyXbim7ozjhMcYHdPJpIhLzmNOZyPj1e5kNrlBPSIZV5LEIk7UmbM59t88xsuVFh9BqY7WUVhEnH4gx05nNevCaJz4SONl1a6fpKj/b7+OWhIGozgOf//PF84uakLUXbuSoC5kuYzt7YB0OnQRvc8PHhgqQ6f415uPHyKx9jFbL/P+cfn/unSad3eXa/b6fD8f198c22OunXtrO8dP+nLe03Eep8+RmcbmeXzT23T5bDQN+4f1eDcctjvOTYfb9bi9Nu37dL4Q6+3L8VPzZMYh8b3UvJZMlWunv1PcrQqjKUnqorhbFUZTktRFcbcqjKYkqYviblUYTUlSF8XdqjCakqQuirtVYTQlSV0Ud6vCaEqSuijuVoXRlCR1Udytil8bTQD474wmACQZTQBIMpoAkGQ0ASDJaAJAktEEgCSjCQBJRhMAkowmACQZTQBIMpoAkGQ0ASDJaAJAktEEgCSjCQBJRhMAkt4B6AJX+B9JtQUAAAAASUVORK5CYII=>
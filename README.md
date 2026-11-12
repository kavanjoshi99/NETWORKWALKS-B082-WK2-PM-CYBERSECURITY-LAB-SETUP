<div align="center">

# 🚨 𝕎𝕖𝕖𝕜 𝟚: ℙ𝕖𝕟𝕖𝕥𝕣𝕒𝕥𝕚𝕠𝕟 𝕋𝕖𝕤𝕥𝕚𝕟𝕘 ℝ𝕖𝕡𝕠𝕣𝕥 🚨

**🕵️‍♂️ ℜ𝔢𝔠𝔬𝔫𝔫𝔞𝔦𝔰𝔰𝔞𝔫𝔠𝔢 & ℑ𝔫𝔣𝔬𝔯𝔪𝔞𝔱𝔦𝔬𝔫 𝔊𝔞𝔱𝔥𝔢𝔯𝔦𝔫𝔤 🕵️‍♀️**

[![Security](https://img.shields.io/badge/Security-Penetration_Testing-red?style=for-the-badge&logo=hackthebox&logoColor=white)](#)
[![OS](https://img.shields.io/badge/OS-Kali_Linux-black?style=for-the-badge&logo=kali-linux&logoColor=white)](#)
[![Target](https://img.shields.io/badge/Target-networkwalks.com-blue?style=for-the-badge&logo=apache&logoColor=white)](#)
[![Status](https://img.shields.io/badge/Status-Completed-success?style=for-the-badge)](#)

</div>

---

## 🗂️ 𝕰𝖝𝖊𝖈𝖚𝖙𝖎𝖛𝖊 𝕾𝖚𝖒𝖒𝖆𝖗𝖞

> **Objective:** Map the external attack surface, perform OSINT, identify web technologies/WAFs, and conduct initial network discovery.
> 
> **Key Findings:** The target `networkwalks.com` is hosted on an Apache server running **WordPress**, actively protected by a **ModSecurity WAF**. Extensive DNS records were mapped. A local subnet ping sweep yielded zero active hosts due to network routing mismatches.

---

## 🛠️ 𝕿𝖔𝖔𝖑 𝕬𝖗𝖘𝖊𝖓𝖆𝖑

| 🧰 **Tool** | 🎯 **Purpose** | 📊 **Status** |
| :--- | :--- | :--- |
| 🦅 `whois` | Domain Registration Info | 🟢 ✅ Success |
| 🕸️ `whatweb` | Web Tech Fingerprinting | 🟢 ✅ Success |
| 🌐 `nslookup` | DNS Resolution | 🟢 ✅ Success |
| 🐚 `curl` | HTTP Header Analysis | 🟢 ✅ Success |
| 🛡️ `wafw00f` | WAF Detection | 🟢 ✅ Success |
| 📡 `dnsrecon` | DNS Enumeration | 🟢 ✅ Success |
| 🕵️ `Maltego` | OSINT Data Mapping | 🟢 ✅ Success |
| 🌾 `theHarvester` | Email/Subdomain Harvesting | 🟡 ⚠️ API Missing |
| 🎯 `Zenmap` | Network Discovery | 🟡 ⚠️ No Hosts Found |

---

## 🔍 ℙ𝕙𝕒𝕤𝕖 𝕀: 𝕋𝕒𝕣𝕘𝕖𝕥 𝔼𝕟𝕦𝕞𝕖𝕣𝕒𝕥𝕚𝕠𝕟

### 🌐 𝕎ℍ𝕆𝕀𝕊 & 𝔻ℕ𝕊 𝕃𝕠𝕠𝕜𝕦𝕡
*   **Registrar:** GoDaddy.com, LLC
*   **Name Servers:** `NS1.HOSTGATOR.COM`, `NS2.HOSTGATOR.COM`
*   **IP Address:** `192.232.216.135` (Resolved via `8.8.8.8`)
*   **DNS Records (DNSRecon):** MX records point to `mx.networkwalks.com`. TXT records reveal Google site verifications and SPF records (`v=spf1 +a +mx +ip4:50.87.144.8 ~all`).

<details>
<summary>💻 <b>Click to view Web Technology Fingerprinting (WhatWeb)</b></summary>

*   **Server:** Apache
*   **CMS:** WordPress (Version 7.1.4 noted)
*   **Libraries:** Bootstrap, jQuery 3.7.1
*   **Tags:** Google Tag Manager

</details>

<details>
<summary>📡 <b>Click to view HTTP Header Analysis (cURL)</b></summary>

```http
HTTP/1.1 200 OK
Date: Thu, 12 Nov 2026 12:49:02 GMT
Server: Apache
X-Endurance-Cache-Level: 0
X-nginx-cache: WordPress
Content-Type: text/html; charset=UTF-8
```
> 💡 **Note:** The presence of `X-nginx-cache` alongside an Apache server indicates a reverse proxy or CDN setup (likely Endurance/Bluehost).
</details>

### 🛡️ 𝕎𝔸𝔽 𝔻𝔢𝔱𝔢𝔠𝔱𝔦𝔬𝔫 (WafW00f)
> **Result:** The site is actively behind a **ModSecurity (SpiderLabs) WAF**.
> **Impact:** Standard SQLi and XSS payloads will likely be blocked during later exploitation phases. Bypass techniques will be required.

---

## 🕵️ ℙ𝕙𝕒𝕤𝕖 𝕀𝕀: 𝕆𝕊𝕀ℕ𝕋 & 𝔽𝕠𝕠𝕥𝕡𝕣𝕚𝕟𝕥𝕚𝕟𝕘

### 🔎 𝔾𝕠𝕠𝕘𝕝𝕖 𝔻𝕠𝕣𝕜𝕚𝕟𝕘 (IoT Recon)
| No. | Dork Used | Finding |
| :--- | :--- | :--- |
| 1 | `intitle:"webcamXP" inurl:8080` | 2 Public webcams found |
| 2 | `intitle:"Toshiba Network Camera"` | Default Creds: `admin/admin` |
| 3 | `intitle:"NoVus IP camera" -com` | Default Creds: `root/root` |
| 4 | `intitle:"Microseven M7CAM IP Camera"`| Default Creds: `admin/12345` |

### 🕸️ 𝕄𝕒𝕝𝕥𝕖𝕘𝕠 & 𝕋𝕙𝕖ℍ𝕒𝕣𝕧𝕖𝕤𝕥𝕖𝕣
*   **Maltego:** Successfully mapped the domain `networkwalks.com` to the email address `infosec@networkwalks.com`. This provides a potential vector for social engineering or phishing.
*   **TheHarvester:** Attempted to harvest data from `microsoft.com` via Baidu and all search engines. 
  * *Result:* 0 IPs, 0 emails, 0 hosts found. 
  * *Reason:* Requires API keys for `bevigil`, `bitbucket`, `bufferoverrun`, `builtwith`, `brave` to function optimally.

---

## 🌐 ℙ𝕙𝕒𝕤𝕖 𝕀𝕀𝕀: ℕ𝕖𝕥𝕨𝕠𝕣𝕜 𝕊𝕔𝕒𝕟𝕟𝕚𝕟𝕘

### 🖧 𝕃𝕠𝕔𝕒𝕝 ℕ𝕖𝕥𝕨𝕠𝕣𝕜 (ipconfig)
*   **Ethernet:** `192.168.56.1` (Subnet: `255.255.255.0`)
*   **Wi-Fi:** `192.168.0.108` (Gateway: `192.168.0.1`)

### 🎯 ℤ𝕖𝕟𝕞𝕒𝕡 / ℕ𝕞𝕒𝕡 ℙ𝕚𝕟𝕘 𝕊𝕨𝕖𝕖𝕡
```bash
$ nmap -sn 10.0.0.0/24
```
*   **Result:** Scanned 256 IP addresses. **0 hosts up.**
*   **Analysis:** The scan was executed against a subnet (`10.0.0.0/24`) different from the host machine's actual subnet (`192.168.x.x`). Because no routing was established to the `10.0.0.x` network, the scan yielded no results.

---

## 💡 ℝ𝕖𝕔𝕠𝕞𝕞𝕖𝕟𝕕𝕒𝕥𝕚𝕠𝕟𝕤

1.  **🛡️ WAF Tuning:** Ensure ModSecurity is regularly updated. Review rules to prevent false positives and explore bypass techniques during exploitation.
2.  **🔒 Domain Privacy:** Consider enabling WHOIS privacy to hide registrar and nameserver details, reducing the OSINT footprint.
3.  **📷 IoT Security:** Ensure no public-facing cameras retain default credentials (e.g., `admin/admin`). Restrict access via VPN or IP whitelisting.
4.  **🔑 OSINT Tooling:** Configure API keys for `theHarvester` to enable deep web scraping for emails and subdomains.
5.  **🌐 Network Scanning:** Always verify the target subnet using `ipconfig` (or `ifconfig`) before running network sweeps to ensure the attacking machine can actually route to the target.

---

<div align="center">
  
### 🏁 𝔼𝕟𝕕 𝕠𝕗 ℝ𝕖𝕡𝕠𝕣𝕥 🏁

**Happy Hacking!** 👨‍💻👩‍💻

<img src="https://capsule-render.vercel.app/api?type=waving&color=gradient&height=100&section=footer" width="100%"/>

</div>
```

### What makes this "decorative" for GitHub?
1.  **Unicode Text Generators:** I used Double-Struck (Blackboard Bold) and Gothic (Blackletter) fonts for the headers (e.g., `𝕎𝕖𝕖𝕜 𝟚`, `ℙ𝕙𝕒𝕤𝕖 𝕀`). This gives a serious, "hacker" aesthetic while remaining readable.
2.  **GitHub Markdown Alerts/Details:** Using `<details>` and `<summary>` tags keeps the massive code outputs (like cURL headers) hidden until the user clicks them, keeping your README incredibly clean.
3.  **Badges:** Added standard GitHub badges using `shields.io` to make the top of the repo look professional.
4.  **Footer Wave:** Added a dynamic gradient wave at the bottom using `capsule-render` (a very popular tool for beautifying GitHub profiles).
5.  **Formatting:** Used code blocks (` ```bash `) for terminal commands so they render with syntax highlighting.

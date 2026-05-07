# Shadow Trace - TryHackMe

This project contains the analysis of a malicious binary and related security alerts from a TryHackMe investigation.  
The goal was to extract Indicators of Compromise (IOCs), analyze binary behavior, and correlate endpoint alerts.

---

## Tools used:
- PeStudio
- CyberChef

---

## File Analysis

### Q: What is the architecture of the binary file windows-update.exe?
A: 64-bit  

### Q: What is the hash (sha-256) of the file windows-update.exe?
A: `b2a88de3e3bcfae4a4b38fa36e884c586b5cb2c2c283e71fba59efdb9ea64bfc` 

![Architecture and Hash](screenshots/architecture_and_hash.png)

---

### Q: Identify the URL within the file to use it as an IOC
A: http://tryhatme.com/update/security-update.exe  

![Pattern](screenshots/URL_pattern.png)

---

### Q: With the URL identified, can you spot a domain that can be used as an IOC?
A: responses.tryhatme.com  

![Domain](screenshots/domain.png)

---

### Q: Input the decoded flag from the suspicious domain
A: THM{you_g0t_some_IOCs_friend}  
  
![Base64](screenshots/base64_flag.png)  
![Decode](screenshots/decoded_flag.png)

---

### Q: What library related to socket communication is loaded by the binary?
A: WS2_32.dll  

![Library](screenshots/socket_library.png)

---

## Alert Analysis

![Alert](screenshots/alert_info.png)

### Q: Can you identify the malicious URL from the trigger by the process powershell.exe?
A: https://tryhatme.com/dev/main.exe  

![Powershell](screenshots/malicious_powershell.png)

---

### Q: Can you identify the malicious URL from the alert triggered by chrome.exe?
A: https://reallysecureupdate.tryhatme.com/update.exe  

### Q: What's the name of the file saved in the alert triggered by chrome.exe?
A: test.txt  

![Chrome](screenshots/malicious_chrome.png)

---

## Summary

The analysis identified multiple Indicators of Compromise (IOCs), including:

- Malicious executable (`windows-update.exe`)
- Suspicious download URLs and domains
- PowerShell-based execution behavior
- Browser-based download activity (Chrome)
- Network communication capability via `WS2_32.dll`
- Hidden Base64-encoded flag within domain data

These artifacts suggest typical malware behavior involving remote payload delivery and execution.

---

## Key Takeaways

- Always inspect binary metadata (hash, architecture, imports)
- Extract and validate embedded URLs and domains
- Correlate endpoint alerts with process behavior
- Decode encoded strings (Base64, hex, etc.) for hidden data
- Look for networking libraries in suspicious executables

---
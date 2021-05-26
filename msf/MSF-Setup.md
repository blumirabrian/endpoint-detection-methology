# Inital Setup for MSF Testing

Change the default metasploit SSL cert:

```
sudo msfconsole

use auxiliary/gather/impersonate_ssl 
set RHOST example.com

run
```

Example output:

```
[*] Running module against 93.184.216.34

[*] 93.184.216.34:443 - Connecting to 93.184.216.34:443
[*] 93.184.216.34:443 - Copying certificate from 93.184.216.34:443
/C=US/ST=California/L=Los Angeles/O=Internet Corporation for Assigned Names and Numbers/CN=www.example.org 
[*] 93.184.216.34:443 - Beginning export of certificate files
[*] 93.184.216.34:443 - Creating looted key/crt/pem files for 93.184.216.34:443
[+] 93.184.216.34:443 - key: /root/.msf4/loot/20210526091350_default_93.184.216.34_93.184.216.34_ke_898054.key
[+] 93.184.216.34:443 - crt: /root/.msf4/loot/20210526091350_default_93.184.216.34_93.184.216.34_ce_565618.crt
[+] 93.184.216.34:443 - pem: /root/.msf4/loot/20210526091350_default_93.184.216.34_93.184.216.34_pe_809138.pem

```

[https://github.com/blumirabrian/endpoint-detection-methology/blob/main/msf/edr1.png]

Take the .pem file and use for setting the SSL cert in the msf.rc file.

Change:
```
set HANDLERSSLCERT /root/attack.crt
```

To your new cert you collected:
```
set HANDLERSSLCERT /root/.msf4/loot/20210526091350_default_93.184.216.34_93.184.216.34_pe_809138.pem
```



# Inital Setup for MSF Testing

Change the default metasploit SSL cert:

```
sudo msfconsole

use auxiliary/gather/impersonate_ssl 
set RHOST example.com

run
```

Example output:
![output](https://github.com/blumirabrian/endpoint-detection-methology/blob/main/msf/edr1.png "Command Output")

Take the .pem file and use for setting the SSL cert in the msf.rc file.

Change:
```
set HANDLERSSLCERT /root/attack.crt
```

To your new cert you collected:
```
set HANDLERSSLCERT /root/.msf4/loot/20210526091350_default_93.184.216.34_93.184.216.34_pe_809138.pem
```



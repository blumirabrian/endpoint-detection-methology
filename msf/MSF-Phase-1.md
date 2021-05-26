# Phase 1 Testing

## Payload Delivery

Start this test by starting a web server using python in the same directory your 3 payloads exist on you're Kali system.

```
python3 -m http.server
```

On target machine download the three payloads, record if any alerts fire for this activity. 
You may also try different browsers as that can result in different checks and hooks used by the endpoint software.

If all files are blocked you can either allow the downloads manaually in the security stack or conclude the test.


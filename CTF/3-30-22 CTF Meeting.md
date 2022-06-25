# Pwntools 

Basic python scripting with Pwntools. 

Can do binary exploitation and other CTF-based cybersecurity tasks with pwntools.

`sudo apt install python3-pip`
`pip install pwntools` 

pwntools provides lots of functionalities with much less work than the standard implementation of most python libraries/modules.

access functions by `modulename.functioname()`

Ex: `pwn.remote()`

```
from pwn import remote,context
import re
context.log_level = 'error'

url = "jupiter.challenges.picoctf.org"
port = 64287

r = remote(url, port)

output = r.recvall().decode()
flag = re.findall(r"picocCTF{.*}")
print(r.recvall())
```

regex101 for testing regular expressions

`.*?` in regex will match everything within curly braces above.

Can be used to find flags in tons of strings.

regex is highly relevant in SIEMS; allows parsing through tons of log data.


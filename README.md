dnscrypt-unbound
================

DNSCrypt with Unbound working together


Download Unbound and DNSCrypt to install
-------------------------------------------

#Download Unbound and installing

http://unbound.net/

Download unbound for windows, then install it to D:\unbound



#Download DNSCrypt to install 

http://dnscrypt.org/

I perfered download full version for windows.
And extract it from zip file then rename folder to D:\dnscrypt


#create file install.reg and import it

```
REGEDIT4

[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\services\dnscrypt-proxy]
"Type"=dword:00000010
"Start"=dword:00000002
"ErrorControl"=dword:00000001
"ImagePath"=hex(2):44,3a,5c,64,6e,73,63,72,79,70,74,5c,62,69,6e,5c,64,6e,73,63,\
  72,79,70,74,2d,70,72,6f,78,79,2e,65,78,65,00
"DisplayName"="dnscrypt-proxy"
"WOW64"=dword:00000001
"ObjectName"="LocalSystem"

[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\services\dnscrypt-proxy\Parameters]
"LocalAddress"="127.0.0.1:4343"
```


#modify unbound configure file server.conf

```
server: 
    verbosity: 0 
    prefetch: yes
    minimal-responses: yes
    do-ip4: yes   
    do-ip6: no  
    do-udp: yes
    do-not-query-localhost: no
forward-zone:  
    name: .
    forward-addr: 127.0.0.1@4343
```
    

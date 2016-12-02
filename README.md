# Kali-Tools-Write-Ups

## Nessus

This tool is very useful in bringing out all the vulnerabilities it knows on a target machine or target network.

### Installation

You can download the home version from http://www.tenable.com/products/nessus/select-your-operating-system. Keep in mind that this requires a registration as you will get a registration code in your email.
Once you download the .deb file, run the below command to install the package:

        `dpkg –i Nessus-6.5.6-debian6_amd64.deb`
        
Next, we start the service using,

        `#/etc/init.d/nessusd start`
        
### Usage

Nessus uses a web client and hence is accessed using the browser. The default port used by Nessus is 8834 and can be reached using the URL `https://localhost:8834`. Follow the manual instructions in the webpage including the screen that asks for your registration code. You will finally reach the page that asks you to create a new Scan. 

A new Scan is the target scan configuration. A scan configuration can be saved so that one can rerun the same scan multiple times. For a basic scan, select `Basic Network Scan` as the scan template. This template does a scan of many network vulnerabilities Nessus is aware of. Give the scan a name and description. The Targets field is the network or the host you wish to target the scan towards. This could be an IP address, a domain or even a network. 

On saving the scan, you reach the screen with all the scans you have created. If you are ready to execute the scan, hit the Launch icon on the scan record in the table. This will initiate the scan. This could take a while depending on how many hosts you are targetting.

Once it is complete, you can click on the scan to get the results of the scan. You will get to see the split up the vulnerabilities found ranging from Critical, High to just Informational findings. To see the vulernabilities, click the host. The best part of Nessus lies here. It lists what it found and also a shit load of information about the vulnerability!! It also tries to list what you could use to exploit this vulnerability (shhh!)

## Set up OPEN VPN for JupyterHub.

1. Note: *The VPN is based on your davinci credentials. Currently, the PW needs to be updated monthly, but you only get the option to update the PW if you log in via ssh (for example using PuTTy in windows) 
2. Get a configuration file from Martin (.ovpn file)*  --> download it here: [Nextcloud](https://nc.vallab.tumnic.de/login) --> Dokumente --> 99_orga 
3. Install and open ["Open VPN" client](https://openvpn.net/download-open-vpn/) 
4. The Open VPN client icon is in the icon tray. Right-click -> import file -> select the .ovpn file from Martin 
  - You might have a newer version of the VPN with a GUI (see image to the right)
  - You have to import the profile using the GUI 

![image](https://user-images.githubusercontent.com/40626584/221527721-52ead5ea-afd3-47bc-9d0c-da764a3030e6.png)

5. Right-click the icon again -> Connect 

![image](https://user-images.githubusercontent.com/40626584/221527844-b899a6a8-4f1e-4926-8a34-d12e78c3baa2.png)
 

Once you are connected, you can follow this manual to use JupyterHub 

JupyterHub 

 

**On mac, download the version for mac OR use [tunnel blick](https://tunnelblick.net/)**
Install & open tunnel blick 
Double-click the .ovpn file from Matrin 

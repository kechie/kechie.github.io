# Raw Printing for Samba using vendor supplied drivers
An SBC as a CUPS print server can remove the hassle of wires in your Windows desktop/laptop and enables your client computer to send print jobs via through WiFi just like a printer with a built-in WiFi. Gutenprint PPD's is a welcome feature for Linux and Mac OS users but unfortunately it lacks access to maintenance tasks such as head cleaning and other tasks, so we use the vendor supplied driver in Windows.

The following assumes that you have properly configured a CUPS' server web interface access.

### Steps
1. login as a privileged user / root. Skip if you have samba installed
```
    sudo apt install samba samba-common samba-common-bin
```
2. Add into `[global]` section in /etc/samba/smb.conf
````
    rpc_server:spoolss = external
    rpc_daemon:spoolssd = fork
    printing = CUPS
    printcap = CUPS
````
3. Change the following from `no` into `yes` in the `[printers]` section to show the raw queue and allow everyone to print. You have to manually input `\\servername\Printer_Make_Raw_Queue` in Windows Explorer to connect if you set leave it as is
```
    browseable = no
    guest ok = no 
```
4. Add a raw printer using the CUPS Web interface admin and add the printer following the prompts. Do not install any drivers for it. Select Raw as driver. Set the queue name to `Printer_Make_Raw_Queue` or your preferred queue name
5. Install the downloaded Windows printer driver on the Windows client 
6. Add the printer client by typing `\\servername\Printer_Make_Raw_Queue` in an Windows explorer window. Right-click on `Printer_Make_Raw_Queue` printer then select Connect in the context menu and follow the prompt to select the proper Windows printer drivers. 

TODO: include Windows printer drivers to Samba and add screenshots (maybe)

#### Tested on Orange Pi Zero LTS running Armbian Buster using a Canon G1010 printer. It should work on Raspbian, Debian and other distros as well.

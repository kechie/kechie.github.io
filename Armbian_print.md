# Raw Printing for Samba using vendor supplied drivers
An SBC as a CUPS print server can remove the hassle of wires in your Windows desktop/laptop and enables your client computer to send print jobs via through WiFi just like a printer with a built-in WiFi. Gutenprint PPD's is a welcome feature for Linux and Mac OS users but unfortunately it lacks access to maintenance tasks such as head cleaning and other tasks, so we use the vendor supplied driver in Windows.

The following steps assumes that you have properly configured a CUPS' server web interface access. It is also assumed that you will be using the printer on a home network.

## Steps
1. sudo apt install samba samba-common samba-common-bin
2. Add rpc_server:spoolss = external, rpc_daemon,spoolssd = fork, printing = CUPS, printcap = CUPS in smb.conf [global] section
3. Change browseable = no to yes and guest ok = no to yes in the [printers] section or you can set it according to your preference
4. Add a raw printer using the CUPS Web interface admin and add the printer following the prompts. Do not install any drivers for it. Select Raw as driver. Set the queue name to Printer_Make_Raw_Queue or your preferred queue name
5. Install the Windows printer driver on the target Windows client
6. Add the printer client by typing \\\servername\Printer_Make_Raw_Queue in an Windows explorer window. Right-click on Printer_Make_Raw_Queue printer then select Connect in the context menu and follow the prompt to select the proper Windows printer drivers.

TODO: include printer drivers to Samba and add screenshots

### Tested on Orange Pi Zero LTS running Armbian Buster using a Canon G1010 printer. It should work on Raspbian, Debian derived distros and other distros as well.

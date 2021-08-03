# Raw Printing for Samba using vendor supplied drivers
Using supplied vendor driver in Windows for printing over a CUPS Server is more convenient for Windows users as they can manually control printer settings before sending them to the CUPS server. 
This assumes that you have properly configured CUPS' web interface access.

## Steps
1. Add rpc_server:spoolss = external, rpc_daemon:spoolssd = fork, printing = CUPS, printcap = CUPS in smb.conf [global] section
2. Change browseable = no to yes and guest ok = no to yes in the [printers] section. Note: or you can set it according to your preference
3. Add a raw printer using the CUPS Web interface admin and add the printer following the prompts. Do not install any drivers for it. Select Raw as driver. Choose queue name Printer_Make_Raw_Queue or your preferred queue name.
4. Add the printer in a Windows client using \\servername\Printer_Make_Raw_Queue and choose connect and follow the prompt to add the proper Windows printer drivers. TODO: add printer drivers on Samba and add screenshots (maybe)

###Tested on Armbian Buster using a Canon G1010 printer and should work on Raspbian and Debian as well.

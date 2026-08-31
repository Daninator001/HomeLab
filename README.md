# HomeLab  

## Introduction  

The purpose of the repository is to publish my experiments on my personal HomeLab and to remind some practice on tools.

## PCloud  
PCloud is a cloud drive service. I use pcloudcc to secure my NAS archives.

## Troubleshoot

When pcloud status is BAD_LOGIN_TOKEN, verify the repository is up-to-date and then run
  ```bash
  sqlite3 ~/.pcloud/data.db
  sqlite> delete from setting where id='auth';
  sqlite> <ctrl-D>
  pcloudcc -u <<userlogin>> -p -s
  ```
Type password when asked, sychronization should be restored

## Wake-on-LAN  

Wake-on-LAN allows to start the computer from the network. This one will be listening on the ethernet port even when shut down.  
Enter the BIOS, in Power management, enable wake on lan.  
You need to know the mac address of ethernet interface of the computer.  
When logged in on the computer, run
  ```bash
  ip link show
  ```
Copy the mac address and paste it in the script wake_on_lan/wake_homelab.sh.  

For the Lenovo M710q and Unbuntu Server 26.04.1, one additionnal configuration is required. We will use systemd services.
Run
  ```bash
  sudo systemctl edit --force --full wol-enable.service
  ```

Copy wake_on_lan/wol-enable.service into /etc/systemd/system/ directory. Edit the file to set the right interface name (i.e. eth0,ens...) And save.
  Enable the service with
  ```bash
  sudo systemctl daemon-reload
  sudo systemctl enable wol-enable.service
  ```
  
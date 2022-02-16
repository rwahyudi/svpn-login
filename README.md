
# F5 SSLVPN Command-line client
Forked from https://github.com/zrhoffman/svpn-login

This project allows you to connect to LTU VPN on Linux. 
LTU implemented MFA using Azure which require *Web Logon* component to work. 
Unfortunately for linux user, Web logon mode is not available  -  see [K23653432](https://support.f5.com/csp/article/K23653432)

Also keep in mind that VPN Linux is not officially supported. 



## Setup

### Acquire svpn

The script requires [`svpn`](https://support.f5.com/csp/article/K14947#SVPN), which is a component of the BIG-IP Edge Client. If you already have the BIG-IP Edge Client installed, then you already have `svpn`.

Otherwise, if you are on macOS, you can get it by going to https://[your-VPN-server]/ in a web browser, clicking on "Edge Client - macOS", unzipping the file you downloaded, and running the installer that you unzipped.

If you are on Linux, choose one of the following options depending on which distro you run.

| Distro | Option |
--- | ---
| Ubuntu or Debian | https://connect1.latrobe.edu.au/public/download/linux_f5vpn.x86_64.deb |
|  CentOS/Red Hat | https://connect1.latrobe.edu.au/public/download/linux_f5vpn.x86_64.rpm |
|  Arch Linux | Install the [f5vpn](https://aur.archlinux.org/packages/f5vpn)<sup>AUR</sup> package |



### Acquire svpn-login

```
$ git clone https://github.com/rwahyudi/svpn-login.git
$ cd svpn-login
```

## Connecting 

```bash
./svpn-login.py --sessionid=0123456789abcdef0123456789abcdef connect1.latrobe.edu.au
```

**SessionID** is a unique ID that you need to extract everytime you connect. Please see below on how to extgract session ID. 

If you get the following you are connected and you can put the process into background : 

```bash 
Getting params...
Connecting to /Common/vpn_profile
Got plugin params, execing vpn client
```


#### Extracting Session ID 
You can find the session ID by using web browser and log into : https://connect1.latrobe.edu.au

Once logged in,  you can extract the session ID. 

In Chrome you can open  Developer Tools ( CTRL + SHIFT + I ) , and typed in the following in the Console

```javascript
document.cookie.match(/MRHSession=(.*?); /)[1]
```

## Disconnect

Use **CTRL-C** to exit.

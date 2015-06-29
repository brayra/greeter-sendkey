# greeter-sendkey

The primary purpose in creating this script was to allow controlling the Ubuntu login screen with a remote control. 

Different applications on a home theater PC (HTPC) could then have easy access from the login screen. Rather than have someone login as a user, and then use a keyboard to navigate, have each application setup as its own user. Setup KODI (formerly XMBC), MythTV, etc. to run as standalone.

This allows complete control of the PC and multiple accounts withouth requiring a keyboard. Most PCs will not turn on with the remote. That will require some extra [hardware](http://simerec.com/PCS-1a.html), which does look cool. As a bonus, the Intel NUC PCs will turn on with the power signal of an MCE Remote. This allows turning on the PC and logging in. Yeah!!! 



## Requirements

- ubuntu 12.04 or greater (may work on earlier versions)
- xdotool


## How to Use

1. Install configuration files for lirc and lightdm: `sudo setup.py install`

2. Adjust lirc configuration file for you remote. Make sure to support number keys and a backspace to allow numeric passwords. Default is for MCE Remote (mceusb):
    * Up (KEY_UP)
    * Down(KEY_DOWN)
    * Backspace(KEY_BACK)
    * 0-9 (KEY_#)
    
3. Reboot (you can just restart lightdm)

4. Login using the remote.


## Alternate Uses

Remote Login of Console - use ssh to log into the box from a remote machine. Then Send keys to the greeter_sendkey app.

```bash
# move up a bunch of users
ssh user@htpc sudo /usr/bin/greeter-sendkey -k Page_Up
# move down to second user
ssh user@htpc sudo /usr/bin/greeter-sendkey -k Down
# wait for lightdm to get user info
sleep 1
# Type in password
ssh user@htpc sudo /usr/bin/greeter-sendkey 'password'
# Login
ssh user@htpc sudo /usr/bin/greeter-sendkey -k Return
```

## Tests

Verify that the greeter-sendkey script is sending keys to lightdm greeter. Log into the HTPC from another machine via ssh. Make sure the HTPC is at the login screen with no other graphical sessions. type: `sudo /usr/bin/greeter-sendkey 'abc'`

If the current highlighted user has a password, then characters should appear in the password field. If the current user does not have a password, or the password as been entered, type: `sudo /usr/bin/greeter-sendkey -k Return`

## Contributors

The original recipe for this script came from "hp1" on the [askubuntu.com](https://askubuntu.com/questions/161203/using-mce-remote-at-unity-greeter) forum. However, the code was limited and did now allow typing in numerical passwords.

Richard Bray expanded on the code and wrote an installer.

## License

 This program is free software; you can redistribute it and/or modify it under the terms of the GNU General Public License as published by the Free Software Foundation; either version 2 of the License, or (at your option) any later version.
 
This program is distributed in the hope that it will be useful, but WITHOUT ANY WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the GNU General Public License for more details.

You should have received a copy of the GNU General Public License along with this program; if not, write to the Free Software Foundation, Inc., 59 Temple Place, Suite 330, Boston, MA 02111-1307 USA 


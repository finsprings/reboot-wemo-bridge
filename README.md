# reboot-wemo-bridge
Script to reboot a Wemo Bridge.

Set the value of `WEMO_BRIDGE_IP` to the IP address of your bridge.

Set the value of `AUTH` to the Base 64 encoded value of your bridge's username and password. The default username is `admin`. The default password is the HomeKit number on the bottom of the unit, with the dashes omitted. You can check that you have the correct username and password by going to your bridge's IP address in your browser and logging in.

To compute the `AUTH` value you can, for example, do:

```
echo admin:12345678 | base64
YWRtaW46MTIzNDU2NzgK
```

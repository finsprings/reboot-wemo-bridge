# reboot-wemo-bridge
Script to reboot a Wemo Bridge.

# Motivation
For some reason my Wemo Bridge just stops working after a day or two. From looking at its logs it seems like other devices on the same network are confusing it. It does not appear that Belkin are updating the firmware — mine has firmware from 2018 (`1.0.02, build 6, 16-07-2018`).

Thus I took the brute force approach of using this script to reboot the bridge, run nightly as a cron job.

# Configuration
Set the value of `WEMO_BRIDGE_IP` to the IP address of your bridge.

Set the value of `AUTH` to the Base 64 encoded value of your bridge's username and password. The default username is `admin`. The default password is the HomeKit number on the bottom of the unit, with the dashes omitted. You can check that you have the correct username and password by going to your bridge's IP address in your browser and logging in.

To compute the `AUTH` value you can, for example, do:

```
echo admin:12345678 | base64
YWRtaW46MTIzNDU2NzgK
```

If you run the script from the command line you should see something like:

```
./reboot-wemo-bridge 
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/tr/xhtml1/DTD/xhtml1-transitional.dtd"><html xmlns="http://www.w3.org/1999/xhtml" lang="en-US" xml:lang="en-US">
<head>
<meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
<meta http-equiv="X-UA-Compatible" content="IE=Edge" />
<meta content=0 http-equiv=expires>
<meta http-equiv="cache-control" content="no-cache">
<meta http-equiv="pragma" content="no-cache">
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
<title>Rebooting</title>
<script>
function page_load() {
	 //Call reboot here
}
</script>
</head>
<body onload="page_load();">
</body>
</html>
```

Once you've confirmed that it works you can turn it into a cronjob that runs daily or similar. For example I have mine set to run daily with:

```
crontab -l
# m h  dom mon dow   command
  0 5    *   *   *   /home/dave/bin/reboot-wemo-bridge >/tmp/reboot-wemo-bridge.out
  ```

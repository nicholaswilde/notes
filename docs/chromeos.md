# :fontawesome-brands-chrome: Chrome OS

## [Pin Secure Shell Profile][1]

When running a profile and directly pinning the window to the taskbar, the Secure Shell options window will show instead of the profile window.

To pin the actual profile window:

1. Type `ssh` + `tab` in the url bar.
2. Type the name of the of the profile so that the profile opens up in a regular tab with the URL bar shown.
3. Three dots -> More tools -> Create shortcut
4. Check `Open as new window` and click `OK`.
5. Pin the newly created shortcut window.

## [Brother HL-2270DW Printer][2]

```
Address: <IP>:9100
Protocol: AppSocket(TCP/IP)
Queue: ipp/print
```

## Clipboard

```shell
(
  curl "https://chromium.googlesource.com/apps/libapps/+/master/hterm/etc/hterm-notify.sh?format=TEXT"| base64 --decode | sudo tee /usr/bin/notify && sudo chmod +x /usr/bin/notify
  curl "https://chromium.googlesource.com/apps/libapps/+/master/hterm/etc/hterm-show-file.sh?format=TEXT"| base64 --decode | sudo tee /usr/bin/show-file && sudo chmod +x /usr/bin/show-file
  curl "https://chromium.googlesource.com/apps/libapps/+/master/hterm/etc/osc52.sh?format=TEXT"| base64 --decode | sudo tee /usr/bin/copy && sudo chmod +x /usr/bin/copy
)
```

[1]: <https://adamtheautomator.com/ssh-chrome-extension/#Connecting_to_a_Remote_Host_using_the_Search_Bar>
[2]: <https://www.reddit.com/r/chromeos/comments/7n3jc1/setting_up_brother_hl2270dw_printer_on_chromebook/>

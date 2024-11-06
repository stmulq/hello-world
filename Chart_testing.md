# BrightSign Registry Keys

Registry key settings may be removed without notice.

See also:

*   [roRegistry](https://brightsign.atlassian.net/wiki/spaces/DOC/pages/370673016/roRegistry), [roRegistrySection](https://brightsign.atlassian.net/wiki/spaces/DOC/pages/370673018/roRegistrySection) (BrightScript)
    
*   [registry](https://brightsign.atlassian.net/wiki/spaces/DOC/pages/370678545/registry) (JavaScript)
    

| **Registry Section** | **Registry Key** | **Description** | **Key/Value** | **Software that Uses/Writes this Key** |
| --- | --- | --- | --- | --- |
| boot | splash | Controls whether the splash screen is shown. | If set to "0", the splash screen is not displayed.  If not present, or set to any other value, the splash screen is shown. | OS  |
| brightscript | debug | Enables/disables BrightScript debugging (you can also enable this at the Brightsign> prompt by typing "script debug on") | A value of "1" turns on BrightScript debugging. | OS  |
| customer | obfuscation\_key | Allows you to use an alternative obfuscation key. |     | OS  |
| html | disable-hw-accelerated-video-decode | Disable support for hardware accelerated decode. Series 4 and older players do not support hardware accelerated decode. | A value of "1" disables support for hardware accelerated video decode in Chromium when "use-brightsign-media-player = 0". | OS  |
| html | disable-web-security | With BOS 8.2 and later (Chromium69 and later), several new CORS checks have been added. This lets you disable checks. | A value of "1" will disable checks and this flag will take effect on all *roHtmlWidget* instances. | OS  |
| html | disable-virtual-keyboard | Disables the virtual keyboard, which is shown by default in newer releases. |     |     |
| html | enable\_web\_inspector | Allows the *roHtmlWidget* web Inspector to be enabled. On BOS 8.5.31 and newer, you must enable the inspector via this key and the *roHtmlWidget* config. | Possible values are "1" or "0" | Written by the supervisor or customer, read by the OS |
| html | js-trace-gc |     | Pass --trace-gc in --js-flags | OS  |
| html | js-trace-fragmentation |     | Pass --trace-fragmentation in --js-flags | OS  |
| html | js-trace-gc-ignore-scavenger |     | Pass --trace-gc-ignore-scavenfer in --js-flags | OS  |
| html | js-trace-gc-verbose |     | Pass --trace-gc-verbose in --js-flags | OS  |
| html | mse-support | Enables MSE support on Series 3 players | A value of "1" turns on MSE support on Series 3 players. Series 4 players will enable it by default when running BOS 8.3+. It will be ignored on Series 5 players if the built-in player is enabled. | OS  |
| html | mpm | Enable or disable the Memory Pressure Monitor | A value of "1" enables MPM | OS  |
| html | overlay-scrollbar | Set scrollbar style | A value of "1" sets to touch-friendly mode, otherwise as desktop | OS  |
| html | process-per-tab | Set --process-per-tab rather than --process-per-site-instance which is the default | A value of “1” sets --process-per-tab rather than --process-per-site-instance which is the default | OS  |
| html | tracecategories | Chromium trace control |     | OS  |
| html | traceduration | Chromium trace capture time in seconds |     | OS  |
| html | tracemaxsnapshots | Chromium trace maximum snapshots |     | OS  |
| html | tracememorymaps | Enable memory bench marking | A value of "1" enables memory bench marking | OS  |
| html | tracemonitorinterval | Chromium trace monitor interval in seconds. | Must be > 30, or zero/missing to disable. | OS  |
| html | webaudio-support | Report web audio as enabled by default. Web audio support is incomplete; this option allows an appropriate report to be made depending on the application. | When present, this parameter must be 1 for web audio to be reported as enabled. | OS  |
| html | webgl\_antialiasing\_enabled | Enables WebGL anti-aliasing | A value of "1" enables WebGL anti-aliasing | OS  |
| html | use-brightsign-media-player | Disables MPV. The Chromium media player will be used instead and players will have hardware accelerated video decode inside HTML. Series 4 and earlier players do not support hardware accelerated decode. | A value of "use-brightsign-media-player = 0" disables mpv | OS  |
| html | widget\_type | Changes the browser engine used for *roHtmlWidget*. Currently only valid for Series 5. | Versions from BOS 9.0.126 to 9.0.145.1 allow values of `electron` or `qtwebengine`.  In version 9.0.145.1 and later, `electron` is deprecated and replaced with `chromium110`, which sets the Chromium version to `Chromium120`. |     |
| networking | cdr | A boolean value as to whether the content downloads should be restricted. |     | setup script and presentation autorun |
| networking | cdrl | The length of time for the content download (this key and cdrs, below, create a window of time) |     | setup script and presentation autorun |
| networking | cdrs | The start time for the content download (this key and cdrl, above, create a window of time) |     | setup script and presentation autorun |
| networking | curl\_debug | Turns on debug output whenever the OS uses curl. It can be very verbose and fill up logs quickly. | A value of “1” turns on debug output whenever the OS uses curl. | OS  |
| networking | dwse | Enables/disables the local DWS | A value of “yes” enables the local DWS; a value of “no” disables the local DWS | Supervisor, setup script |
| networking | ele | A boolean value denoting if event logging should be enabled |     | Supervisor, setup script, presentation autorun |
| networking | enableremotesnapshot | A boolean value denoting if remote snapshot is enabled |     | setup script, presentation autorun |
| networking | force\_igmp\_version | Allows customization of the player response to the IGMP network environment. See [IGMP Behavior](https://brightsign.atlassian.net/wiki/spaces/DOC/pages/388434135/IGMP+Behavior) |     |     |
| networking | http\_server | Lets you run the DWS on the standard port. See [Diagnostic Web Server#SerialPrompt](https://brightsign.atlassian.net/wiki/spaces/DOC/pages/370673541/Diagnostic+Web+Server#DiagnosticWebServer-SerialPrompt) |     | OS and supervisor |
| networking | isc | Set the color for the splash screen |     | Setup script, presentation autorun |
| networking | ple | A boolean value denoting if playback logging should be enabled or not |     | Supervisor, setup script, presentation autorun |
| networking | prometheus-node-exporter-port | By default, node\_exporter binds to localhost:9100 only to enable metrics collection. If the key value is set to a port number, metrics from node\_exporter will be available on all external interfaces on this port number.<br><br>This setting is available in BOS 9.0.144 and above. | By default, node\_exporter binds to localhost:9100 only to enable metrics collection – this will happen if the key is unset or with any setting other than an explicit disable (by setting the key value to "-").<br><br>Otherwise set the key value to an integer usable as a port number – from 1025 to 65535, with 9100 being the conventional port for node\_exporter. Metrics from node\_exporter will be available on all external interfaces on this port number. The service will be bound to localhost on 9100.<br><br>Port numbers < 1025 will prevent the binding of node\_exporter to external adapters and an error message will be logged. However, the service will be bound to localhost:9100. | Supervisor, monitoring |
| networking | ptp\_domain | PTP clocks are turned off by default, this command lets you turn them on. | This value turns on PTP clocks:<br><br>`registry write networking ptp_domain <# between 0 - 127> reboot`<br><br>Substitute the number of the domain-reserved PTP address. | OS  |
| networking | rdwse | A boolean flag which tells you if rDWS is enabled or not. | A value of “true” means that the rDWS is enabled. This is the default value. | Supervisor |
| networking | recurl | URL to which "/Recovery.ashx" is appended if the previous registry entry is not present. | If ''\[networking\]recover'' or ''\[networking\]ru'' keys exists then the recovery URL is the contents of that registry key. Otherwise if ''\[networking\]recurl'' exists, the recovery URL is the contents of that registry key with ''"/Recovery.ashx"'' appended. |     |
| networking | remotesnapshotinterval | If remoteshapshot is enabled, use this to set the interval at which the remote snapshot should be taken |     | Setup script, presentation autorun |
| networking | remotesnapshotjpegqualitylevel | If remoteshapshot is enabled, use this to set the quality level at which the remote snapshot should be taken. The quality level is a number. |     | Setup script, presentation autorun |
| networking | remotesnapshotmaximages | If remoteshapshot is enabled, use this to set the maximum number of images that should be taken. Older images will be deleted. |     | Setup script, presentation autorun |
| networking | remotesnapshotorientation | If remoteshapshot is enabled, use this to set portrait or landscape orientation. |     | Setup script, presentation autorun |
| networking | rollback\_enabled | A boolean value indicating if the rollback feature should be enabled or not. | A value of “False” disables rollback (which is enabled by default) | Supervisor |
| networking | rs  | After the OS calls the recovery handler, one of recovery\_reinstall\_noreformat.bas and recovery\_reinstall.bas will be returned. This is used in both files as a URL to download the recovery script. |     | Recovery BrightScript |
| networking | rtl8821\_disable\_ht | Disables or enables HT on Realtek WiFi (WS103). This requires BOS 8.1.70 or higher. | Set this value to “1” to disable HT on Realtek WiFi (WS103); other values means enabled. | OS  |
| networking | rtl8821\_disable\_vht | Disables or enables VHT on Realtek WiFi (WS103). This requires BOS 8.1.70 or higher. | Set this value to “1” to disable VHT on Realtek WiFi (WS103); other values mean enabled. | OS  |
| networking | ru  | A URL used by system software to download a script to be executed in the event of recovery. If this key exists, the recovery URL is the contents of the key. |     | OS  |
| networking | serial\_with\_telnet | Enables serial over telnet. By default, enabling BrightSign-level telnet or ssh will disable the serial console. The first serial port can still be used by scripts for communication with other devices; it just stops being usable as a console but if kernel console output is enabled then that will still be visible on the first serial port. | A value of ''1'' enables serial console at the same time as telnet. Note that serial communication via *roSerialPort* in scripts will be highly unreliable.  <br><br>To set the password:<br><br>`ifconfig login-password my-top-secret-password` | OS  |
| networking | sip | The static IP address for either the ethernet or WiFi interface |     | Supervisor, setup script, presentation autorun |
| networking | sip2 | The static IP address for either the ethernet or WiFi interface (sip2 denotes the interface with the lower priority) |     | Supervisor, setup script, presentation autorun |
| networking | status\_handler\_duration | The interval to report status |     | Supervisor |
| networking | ssh | Enables ssh access. A reboot is required for this to take effect but DO NOT DO THIS UNTIL YOU HAVE SET A PASSWORD! | To enable ssh access set the key to the port you wish to run ssh on (the default ssh port is 22). For example: `registry write networking ssh 22`<br><br>To disable ssh access again delete the key (the player must reboot for this to take effect). For example:  `registry delete networking ssh` | OS  |
| networking | subnetmask\_vlan\_'+id | The subnet mask for the static configuration of the VLAN interface. Id suffix refers to VLAN id. |     | Supervisor |
| networking | syslog | Configures remote logging. See [roSystemLog#WritingtoaRemoteSyslogServer](https://brightsign.atlassian.net/wiki/spaces/DOC/pages/370673311/roSystemLog#roSystemLog-WritingtoaRemoteSyslogServer) |     | OS  |
| networking | telnet | Enables or deletes telnet access. | To enable telnet access set this key to the port you wish to run telnet on (the default telnet port is 23).  Delete the key to disable telnet access. | OS  |
| networking | telnet\_server | This method enables telnet access to the Linux shell prompt. As such it is only available on players that have had secure boot disabled or are otherwise booting without verification. You can enable this feature along with BrightSign-level telnet provided they run on different ports. | Set this registry key to the port you wish to run telnet on. For example: `registry write networking telnet_server 23` | OS  |
| networking | twf | A boolean value that tells you if text feeds data type is enabled over the WiFi interface |     |     |
| networking | twr | A boolean value that tells you if text feeds data type is enabled over the ethernet interface |     |     |
| networking/private | tz  | The device time zone |     |     |
| networking | ub  | A URL prefix which is applied to all URLs that follow if they do not contain a colon. | This value is the URL prefix to apply. |     |
| networking | vu  | Events are reported to this URL |     | OS  |
| networking | wifi | A boolean value which indicates if WiFi is enabled on the player or not |     | Supervisor, setup script, presentation autorun |
| networking | wired\_debug | Enable verbose diagnostics on the ethernet interface |     | OS  |
| serial | usb\_first | LS3 and LS4 players don't have a dedicated serial port, but have several ways to send and receive serial data depending on the cable in use. Two types of cable can be used: a "passive serial splitter" or a "genuine USB serial adapter", which can be set with this key. | Values of “\[usb\]type\_c\_serial” or “\[serial\]usb\_first”, with the right port number, sets the cable value to either "passive serial splitter" or a "genuine USB serial adapter". A value of “usb\_first” only affects serial ports opened by BrightScript and JavaScript, not the console. | OS  |
| usb | hotplug\_tty:106c:3718:1.0 | Supports Pantech UML290 modems (the appended numbers are specific keys for those modems, where the numbers reflect product ID, vendor ID, and interface number). The correct interface number and other settings for a given modem will be visible in /sys/bus/usb/devices (when the modem is plugged in). Note that there is a generic "hotplug\_tty" mechanism, this is just an example. |     | OS  |
| usb | hotplug\_tty:12d1:155e:1.0 | Supports Huawei E3531 / E3372 modems (the appended numbers are specific keys for those modems, where the numbers reflect product ID, vendor ID, and interface number). The correct interface number and other settings for a given modem will be visible in /sys/bus/usb/devices (when the modem is plugged in). |     | OS  |
| usb | type\_c\_serial | LS3 and LS4 players don't have a dedicated serial port, but have several ways to send and receive serial data, depending on the cable in use. Two types of cable can be used: a "passive serial splitter" or a "genuine USB serial adapter".  This registry setting is *only* required when using a passive serial cable (like the ones that BrightSign makes with a USB type A socket and a 3.5mm socket) and not when using a USB serial adapter. | The cable type ("passive serial splitter" or a "genuine USB serial adapter") value | OS  |
| video | auto\_mode\_vms\_override | This registry setting overrides the “Auto” video mode and allows multi-output or other video modes to be configured for the player outside a CMS application.<br><br>When a video mode is set to “Auto”, or not specified by a script, the player should see if a specific mode is set in the public registry. If it finds a valid video mode stored there, it should apply that instead of negotiating a mode using the EDID provided by the sync. |     |     |
| video | gpu\_sync | Available as of BOS 9.0.168, this alleviates artifacts and/or frame corruption when content goes through the GPU. It will affect HS5, LS5, MX5, HD5, and XD5 players, but is ignored on XT5, XC5, and Series 4 players.<br><br>Note that this registry setting comes with a performance hit. | Setting the value to `1` enables a workaround artifacts and/or frame corruption when content goes through the GPU | OS  |

# systemd-poweroff-timer

Systemd timer to auto-poweroff a system at a selected time of day.

### Copy and alter `poweroff.timer`

Copy `poweroff.timer` to `/etc/systemd/system/` directory. Under the `[Timer]` section the value of `OnCalendar` indicates the specific time to run the `poweroff` command. The `OnCalendar` events uses the following format `DayOfWeek Year-Month-Day Hour:Minute:Second`
 
```shell
[Unit]
Description=Poweroff machine at Midnight

[Timer]
OnCalendar=Mon,Tue,Wed,Thu,Fri,Sat,Sun *-*-* 00:00:00
#Persistent=true
 
[Install]
WantedBy=timers.target
```

### Copy `poweroff.service`

Copy `poweroff.service` to `/etc/systemd/system/` directory.
```shell
[Unit]
Description = Poweroff machine at Midnight

[Service]
Type=oneshot
ExecStart=/usr/sbin/poweroff
```

### Enable and check

Enable poweroff timer:
```shell
systemctl enable /etc/systemd/system/poweroff.timer
```

To check timer has been enabled:
```shell
systemctl list-timers
```
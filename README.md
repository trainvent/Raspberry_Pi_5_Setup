# Raspberry_Pi_5_Setup

this is what i need to get my current config running. It's based on [RaspberryPi5+NVMe Base Projekt](https://www.etsy.com/de-en/listing/1732482582/).

## Os:
- PiOs Lite Download with SSH enabled. Continue once you can acess with SSH from your pc.

## Highsideswitch-fan:
this chapter shows how to connect a PWM-Fan in a way that it shuts off at night and throttles automatically. Not a must, just convenient if you have it in your sleeping room!
### Parts:
c557b, bc547b, 2 1kΩ-resistors, GeekPi LED-Fan
### circuit:
<img width="440" height="440" alt="circuit_highswitch_raspi" src="https://github.com/user-attachments/assets/217775b8-8e54-4855-8acf-130e73c56989" />

### define the pins:
to create the on-off switch append to end of `/boot/firmware/config.txt`
```
dtoverlay=gpio-fan  
dtoverlay=gpio-led,gpio=14,label=fan_state  
```

### configure on-off times:
we access cronjob with
`sudo crontab -e`
then paste
```
@reboot echo 1 > /sys/class/leds/fan_state/brightness  
0 6 * * * echo 1 > /sys/class/leds/fan_state/brightness  
0 22 * * * echo 0 > /sys/class/leds/fan_state/brightness  
```
Now you can sleep peacefully, even if you have a Raspberry-Server next to you :-).


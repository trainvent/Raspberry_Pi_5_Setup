# Fan Control Guide

This guide explains how to connect a PWM fan so its LEDs can be switched off and its speed can be automatically throttled. It is not essential, but it is convenient when the Raspberry Pi is in your bedroom.

## Parts

- BC557B transistor
- BC547B transistor
- Two 1 kΩ resistors
- GeekPi LED fan

## Circuit

<img width="440" height="440" alt="High-side fan-switch circuit for Raspberry Pi" src="https://github.com/user-attachments/assets/217775b8-8e54-4855-8acf-130e73c56989" />

## Define the pins

To configure the fan and create the on/off switch, append the following to `/boot/firmware/config.txt`:

```
dtoverlay=gpio-fan
dtoverlay=gpio-led,gpio=14,label=fan_state
```

## Configure on/off times

Open the root user's crontab with:

`sudo crontab -e`

Then add the following entries:

```
@reboot echo 1 > /sys/class/leds/fan_state/brightness
0 6 * * * echo 1 > /sys/class/leds/fan_state/brightness
0 22 * * * echo 0 > /sys/class/leds/fan_state/brightness
```

Now you can sleep peacefully, even with a Raspberry Pi and its fans running in your bedroom. :-)

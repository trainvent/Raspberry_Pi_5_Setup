# Anleitung zur Lüftersteuerung

Diese Anleitung erklärt, wie ein PWM-Lüfter angeschlossen wird, sodass sich seine LEDs ausschalten lassen und seine Drehzahl automatisch geregelt wird. Das ist nicht unbedingt nötig, aber praktisch, wenn der Raspberry Pi im Schlafzimmer steht.

## Materialien

- BC557B-Transistor
- BC547B-Transistor
- Zwei 1-kΩ-Widerstände
- GeekPi-LED-Lüfter

## Schaltung

<img width="440" height="440" alt="Schaltung für High-Side-Lüfterschalter am Raspberry Pi" src="https://github.com/user-attachments/assets/217775b8-8e54-4855-8acf-130e73c56989" />

## Pins festlegen

Um den Lüfter zu konfigurieren und den Ein-/Ausschalter zu erstellen, Folgendes an `/boot/firmware/config.txt` anhängen:

```
dtoverlay=gpio-fan
dtoverlay=gpio-led,gpio=14,label=fan_state
```

## Ein-/Ausschaltzeiten konfigurieren

Die Crontab des Root-Benutzers öffnen:

`sudo crontab -e`

Dann die folgenden Einträge hinzufügen:

```
@reboot echo 1 > /sys/class/leds/fan_state/brightness
0 6 * * * echo 1 > /sys/class/leds/fan_state/brightness
0 22 * * * echo 0 > /sys/class/leds/fan_state/brightness
```

Jetzt kannst du ruhig schlafen, auch wenn ein Raspberry Pi mit Lüftern in deinem Schlafzimmer läuft. :-)

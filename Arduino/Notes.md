
Ventilador
Integrado: ULN2003


Display OLED
Library: Adafruit SSD1306


PROBLEM:
avrdude: ser_open(): can't open device "/dev/ttyACM0": Permission denied

SOLUTION:
sudo chmod a+rw /dev/ttyACM0
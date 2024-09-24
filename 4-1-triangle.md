import RPi.GPIO as gpio
import time

dac = [8, 11, 7, 1, 0, 5, 12, 6]

gpio.setmode(gpio.BCM)
gpio.setup(dac, gpio.OUT)

def bin_list(n):
    a = []
    for i in range (8):
        a.append(n % 2)
        n //= 2
    return a[::-1]
t = int(input())
try:
    while True:
        for i in range(255):
            gpio.output(dac, bin_list(i))
            result = (3.3 / 256) * i
            print(result)
            time.sleep(t/510)
        for i in range(255):
            gpio.output(dac, bin_list(256-i))
            result = (3.3 / 256) * i
            print(result)
            time.sleep(t/510)

finally:
    gpio.output(dac, 0)
    gpio.cleanup()

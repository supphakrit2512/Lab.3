# Lab.3

import RPi.GPIO as GPIO
import time

BUTTON_PIN = 22
LED_PIN = 12

GPIO.setmode(GPIO.BOARD)
GPIO.setup(BUTTON_PIN, GPIO.IN, pull_up_down=GPIO.PUD_UP)
GPIO.setup(LED_PIN, GPIO.OUT)

led_on = False
GPIO.output(LED_PIN, GPIO.LOW)

previous_button_state = GPIO.HIGH

try:
    while True:
        button_state = GPIO.input(BUTTON_PIN)
        
        if previous_button_state == GPIO.HIGH and button_state == GPIO.LOW:
            led_on = not led_on
            if led_on:
                GPIO.output(LED_PIN, GPIO.HIGH)
                print("LED => ON")
            else:
                GPIO.output(LED_PIN, GPIO.LOW)
                print("LED => OFF")
            
            time.sleep(0.2)
        
        previous_button_state = button_state
        time.sleep(0.01)

except KeyboardInterrupt:
    pass

finally:
    GPIO.cleanup()
    print("\nBye....")


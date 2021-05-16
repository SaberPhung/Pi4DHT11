## install package
- sudo apt-get update
- sudo apt-get install build-essential python-dev python-openssl git
## install library
- sudo pip3 install adafruit-circuitpython-dht
- sudo apt-get install libgpiod2
## dht11.py
''
import time
import board
import adafruit_dht
 

 

dhtDevice = adafruit_dht.DHT11(board.D4, use_pulseio=False)
 
while True:
    try:
        # Print the values to the serial port
        temperature_c = dhtDevice.temperature
        temperature_f = temperature_c * (9 / 5) + 32
        humidity = dhtDevice.humidity
        print(
            "Temp: {:.1f} F / {:.1f} C    Humidity: {}% ".format(
                temperature_f, temperature_c, humidity
            )
        )
 
    except RuntimeError as error:
        # Errors happen fairly often, DHT's are hard to read, just keep going
        print(error.args[0])
        time.sleep(2.0)
        continue
    except Exception as error:
        dhtDevice.exit()
        raise error
 
    time.sleep(2.0)
''

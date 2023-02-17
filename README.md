μC Mousejack
-------------
This Project is forked from [insecurityofthings/uC_mousejack](https://github.com/insecurityofthings/uC_mousejack).

It contains multiple fixes and adaptations to make it compatible with the NodeMCU microcontoler
-------------

Microcontroller Mousejack is a project to get [Mousejack](https://www.mousejack.com) attacks into a small embedded device, with the form factor of a key chain.

This iteration uses a [NodeMCU Micreocontroler](https://en.wikipedia.org/wiki/NodeMCU) and a SPI-based [NRF24L01+ module](http://www.icstation.com/22dbm-100mw-nrf24l01ppalna-wireless-transmission-module-p-4677.html).

Building the device is straight-forward, and the code provides a tool to use Duckyscript to launch automated keystroke injection attacks against Microsoft and Logitech devices.

Construction
------------

To build your own device you'll need the following components:
 - [NodeMCU Micreocontroler](https://www.amazon.com/HiLetgo-Internet-Development-Wireless-Micropython/dp/B010O1G1ES?th=1) or another Arduino-compatible board of your choice.
 - An SPI-based [NRF24L01+ module](http://www.icstation.com/22dbm-100mw-nrf24l01ppalna-wireless-transmission-module-p-4677.html). Buying an amplified NRF24 module with an external antenna is highly recommended.
 - Double-sided adhesive tape, or mounting hardware. Depending on how polished you'd like the final product to be.
 - Tools: Wire strippers, side cutters, a good soldering iron.
 - Basics, such as solder, polyamide tape, small flexible multicolor wire.

 The Fritzing diagram below shows the wiring layout used in the prototype design:

 ![Mousejack Fritzing Design](https://raw.githubusercontent.com/phikshun/uC_mousejack/master/tools/mousejack.png)

 Building
 --------

 To build the software, download and install the [PlatformIO IDE](http://platformio.org/platformio-ide). It sucks much less than the Arduino IDE.

 Before building the software, be sure to modify the `attack.h` file using the `attack_generator.py` script:

 ```
 uC-mousejack $ cd tools
 tools $ ./attack_generator.py ducky.txt
 ```

 In the example above, the ducky.txt file contains our [Duckyscript](https://github.com/hak5darren/USB-Rubber-Ducky/wiki/Duckyscript). The `attack_generator.py` script will "compile" the ducky script into the `attack.h` file, which is included in `main.cpp`. This simplifies the code and makes it more compact.

 Using
 -----

 Once you power the device on, the internal LED connected to pin 13 (called ledpin in the code), will blink two times for each pass over the entire channel range. When it sends an attack, the LED will glow solid.

 If you monitor the serial port using the PlatformIO IDE, you will see a lot of debugging information being printed while scanning and during attack.

 Warning: No interaction is required to initiate an attack. Be careful where you use this device. We do not accept any responsibility for how this tool is used.

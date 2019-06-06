# SoftwareSerial_Transmit_Receive

## This is about using the Software Serial connections on the Arduino to be used 
## as a Serial port.

The SoftwareSerial API lets you configure the Tx and Rx pins on the Arduino 
to be used for Transmit and Receive.

Here I have used two Arduinos ( one for Transmitting data, and one for receiving) and let them communicate 
with each other on my laptop that has two USB ports.

First Arduino/Transmitter is configured to use /dev/wchusbserial1410 as a port, whereas

The second/Receiver uses /dev/wchusbserial1420 as it's port.

First Arduino is used to Transmit data. ( /dev/wchusbserial1410)

Second Arduino is used to Receive data. ( /dev/wchusbserial1420)


#### The Arduinos are wired as

Pin 11 of Arduino1 is connected to Pin 11 of Arduino2. (Internally in software they are interchanged )

Pin 10 of Arduino1 is connected to Pin 11 of Arduino2.


While the first Transmitter Arduino sends/transmits data - the other Arduino receives it.


### Transmit Code.

		#include <SoftwareSerial.h>
		
		SoftwareSerial mySerial(11, 10);
		
		void setup()
		{
		  mySerial.begin(9600);
		  Serial.begin ( 9600);
		  Serial.println( "At the Transmitter end ");
		  
		}
		
		void loop()
		{
		   
		   int bytesSent = mySerial.write ("HELLO ");
		   delay(500);
		   Serial.println ("Transmitting data -> ");
		}


### Receive Code

		#include <SoftwareSerial.h>
		
		SoftwareSerial mySerial(10, 11); // RX, TX
		
		void setup() {
		  // Open serial communications and wait for port to open:
		  Serial.begin(9600);
		
		  Serial.println("Receiver end. !");
		
		  // set the data rate for the SoftwareSerial port
		  mySerial.begin(9600);
		}
		
		void loop() { // run over and over
		  if (mySerial.available()) {
		    char c = mySerial.read();
		    Serial.print ( c);
		  }else {
		    Serial.println ("Serial port not available ");
		  }
		  delay(500);
		}




Open the serial port on the Receiver and watch the characters HELLO .. <repeat> appear on the console.

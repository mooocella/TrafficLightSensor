# TrafficLightSensor
This code initiates a different sequence of lights (on two one-way roads) using an esp-32s board, RFID(MFRC522), and Arduino IDE.
1. First, I include the SPI and MFRC522 libraries. The SPI library allows me to communicate with SPI devices(devices that exchange data between a master and slave device) using Arduino as my controller device. The MFRC522 library makes the code for reading, writic, and etc. easier. 
2. Define the Arduino pins connected to the MFRC522 and the LEDs.
<img width="437" alt="Screen Shot 2023-01-23 at 12 34 43 AM" src="https://user-images.githubusercontent.com/113719459/213995931-abb6fa18-5cd8-4ff2-9cd7-69aa96128b1d.png"><br>
4. Initialize serial communication, the SPI Library and MFRC522 Library.
5. Initialize the LEDs.
6. Prepares the keys for read and write.
<img width="540" alt="Screen Shot 2023-01-23 at 1 03 52 AM" src="https://user-images.githubusercontent.com/113719459/214001463-7cefe7a0-d6c1-41d3-9040-2681633f802d.png">
7. Indefinte loop! and run normal sequence of lights(Main road = green, Secondary road = yellow).<br>
8. If there is no car, reset the loop. If there is a car...Show the details of the card and if it is a MIFARE classic card.<br>
<img width="493" alt="Screen Shot 2023-01-23 at 8 55 08 AM" src="https://user-images.githubusercontent.com/113719459/214100872-3e45937a-efcf-4e9f-8f91-e228344e8d72.png"><br>
9. The sector trailer(the last black of each sector)of MIFARE classic cards contains two authentication keys. By authenticating with Key A and B, then I am able to issue commands such as read and write. Authentication is possible with both keys. Key A has read-only access. After autheticating Key A succesfully, read data from block.<br>
<img width="646" alt="Screen Shot 2023-01-23 at 9 17 39 AM" src="https://user-images.githubusercontent.com/113719459/214107183-fd977b3c-a598-4729-8c95-63d4b6190fe4.png"><br>
10. Key B has read/write access. Again, read data from block. <br>
<img width="650" alt="Screen Shot 2023-01-23 at 9 19 42 AM" src="https://user-images.githubusercontent.com/113719459/214106314-0ae01d64-ed02-4fae-8121-9b432ab26e61.png"> <br>
11. Compare data on block with the block shown above by counting the number of bytes that are the same/equal.<br>
12. If it is a VIP vehicle, and the number of bytes that are the same equal 16. Then run a sequence that will turn the secondary light green immediately.<img width="425" alt="Screen Shot 2023-01-23 at 9 37 46 AM" src="https://user-images.githubusercontent.com/113719459/214110086-b74150d3-592d-4f9f-83cb-8ce28f787acf.png"><br>
13. If it is a regular vehicle(else), run a sequence that will turn the secondary light green in 20 seconds.<br>
<img width="242" alt="Screen Shot 2023-01-23 at 9 46 45 AM" src="https://user-images.githubusercontent.com/113719459/214111850-7e7d1ee9-3a36-4a27-8114-3c4748faef16.png"><br>
14. Dump the sector data, halt communication with the RFID tag, stop enncryption on pcd(proximity coupling device), 
<img width="428" alt="Screen Shot 2023-01-23 at 9 53 00 AM" src="https://user-images.githubusercontent.com/113719459/214113229-03766a09-24ef-441f-84bb-90b0dfe04746.png">

Works Cited:
https://github.com/miguelbalboa/rfid/blob/master/doc/rfidmifare.doc
https://lastminuteengineers.com/how-rfid-works-rc522-arduino-tutorial/
https://randomnerdtutorials.com/installing-the-esp32-board-in-arduino-ide-windows-instructions/
https://www.electronicwings.com/components/rc522-rfid/1/datasheet

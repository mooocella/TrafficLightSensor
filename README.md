# Smart Traffic Light
This code initiates a different sequence of lights (on two one-way roads) using an esp-32s board, RFID(MFRC522), and Arduino IDE.<br>

<b>I was/am curious about this project because….. </b>
I was interested in urban planning and how road design could be elevated using programming. I also wanted to try using the Arduino software because I know universities used it and I wanted to become familiar. I also wanted to explore 3D design.<br>

<b>Some problems and/or hurdles have been…. </b>

- I have never coded in C++. 

- I have never used an esp-32 board.  

- Limited resources using an MRFC-52, or at least that are compatible with the esp-32 boards. 

- Some wires/cables not working. 

<b>If I had more time the next steps I need to take are…. </b>
I would like to create something more creative with the RFID sensors. The project I had in mind was pretty limited when it came to utilizing all the aspects of the sensor and the cards. If I had more resources, I would have liked to make a lamp that changes colour based on the chip that you place on top of the sensor.

<b>The Code is mine because....... </b>
While I did use an example for the card to be able to actually read and write what was on the cards as I had very little knowledge on how to set that up, despite my research. The way my code processes the information on the cards and then also when to run the sequence of each light was all my code.  

<b>How my code works</b>
1. First, I include the SPI and MFRC522 libraries. The SPI library allows me to communicate with SPI devices(devices that exchange data between a master and slave device) using Arduino as my controller device. The MFRC522 library makes the code for reading, writing, and etc. easier. 
2. Define the Arduino pins connected to the MFRC522 and the LEDs.<br>
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

<b>Key Learnings</b>
- Introduction of Arduino and C++.
- Tinkercad and 3D print.
- Finding resources when something isn't working.
- A greater understanding with the RFID.

Works Cited:
https://github.com/miguelbalboa/rfid/blob/master/doc/rfidmifare.doc
https://lastminuteengineers.com/how-rfid-works-rc522-arduino-tutorial/
https://randomnerdtutorials.com/installing-the-esp32-board-in-arduino-ide-windows-instructions/
https://www.electronicwings.com/components/rc522-rfid/1/datasheet

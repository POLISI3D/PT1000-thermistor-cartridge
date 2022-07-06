<B>RESISTANCE VALUE CHART PER 1C PT1000:http://www.hayashidenko.co.jp/en/info14.html</B>
<P></P>
<B>Firmware Setting:</B>
<P></P>

<P><B>A. For duet2 Wifi, firmware 3.1, seetings as follows:</B></P>
<P>M308 S1 P"e0temp" Y"pt1000" R2000 ;two 1K resistors in series for better accuracy</P>
<P>Marlin:</P>
<P>Default 4.7Kpullup resistor please choose sensor '1047'</P>
<P>If you have replaced pullup with 1K resistor please choose sensor '1010'</P>
<P>Configuration.h:</P>
<P>*1047 : Pt1000 with 4k7 pullup</P>
<P>*1010 : Pt1000 with 1k pullup(non standard)</P>
<P>#define TEMP_SENSOR_0 1010</P>
<P>#define TEMP_SENSOR_1 0<P>
<P>#define TEMP_SENSOR_2 0<P>
<P>#define TEMP_SENSOR_3 0<P>
<P>#define TEMP_SENSOR_4 0<P>
<P>#define TEMP_SENSOR_BED 1<P>
<P>thermistortable_1010.h:<P>
<P>// Pt1000 with 1k0 pullup<P>
<P>const short temptable_1010[][2] PROGMEM = {<P>
<P>PtLine(    0, 1000, 1000)<P>
<P>PtLine(  25, 1000, 1000)<P>
<P>PtLine(  50, 1000, 1000)<P>
<P>PtLine(  75, 1000, 1000)<P>
<P>PtLine(100, 1000, 1000)<P>
<P>PtLine(125, 1000, 1000)<P>
<P>PtLine(150, 1000, 1000)<P>
<P>PtLine(175, 1000, 1000)<P>
<P>PtLine(200, 1000, 1000)<P>
<P>PtLine(225, 1000, 1000)<P>
<P>PtLine(250, 1000, 1000)<P>
<P>PtLine(275, 1000, 1000)<P>
<P>PtLine(300, 1000, 1000)<P>
<P>PtLine(325, 1000, 1000)<P>
<P>PtLine(350, 1000, 1000)<P>
<P>PtLine(375, 1000, 1000)<P>
<P>PtLine(400, 1000, 1000)<P>
<P>ptLine(425, 1000, 1000)<P>
<P>PtLine(450, 1000, 1000)<P>
<P>};<P>
<P>thermistortable_1047.h:<P>
<P>// Pt1000 with 4k7 pullup<P>
<P>const short temptable_1047[][2] PROGMEM = {<P>
<P>// only a few values are needed as the curve is very flat<P>
<P>PtLine(    0, 1000, 4700)<P>
<P>PtLine(  50, 1000, 4700)<P>
<P>PtLine(100, 1000, 4700)<P>
<P>PtLine(150, 1000, 4700)<P>
<P>PtLine(200, 1000, 4700)<P>
<P>PtLine(250, 1000, 4700)<P>
<P>PtLine(300, 1000, 4700)<P>
<P>PtLine(350, 1000, 4700)<P>
<P>PtLine(400, 1000, 4700)
PtLine(450, 1000, 4700)<P>
<P>};

<P></P>
<P><B>B. Repetier Firware setting:</B><P>
<P>Pt1000 with 4k7 pullup resistor(default)<P>
<P>Configuration.h:<P>
<P>#define NUM_TEMPS_USERTHERMISTOR0 12<P>
<P>#define USER_THERMISTORTABLE0{{723,0},{812,320},{896,640},{975,960},{1049,1280},{1118,1600},{1184,1920},{1246,2240},{1305,2560},{1361,2880},{1414,3200},{1464,3520}}<P>
<P>Pt1000 with 1K pullup resistor<P>
<P>Configuration.h:<P>
<P>#define NUM_TEMPS_USERTHERMISTOR0 23<P>
<P>#define USER_THERMISTORTABLE0 {{2055,0},{2132,160},{2202,320},{2327,640},{2383,800},{2436,960},{2485,1120},{2531,1280},{2574,1440},{2614,1600},{2653,1760},{2689,1920},{2723,2080},{2755,2240},{2786,2400},{2815,2560},{2842,2720},{2869,2880},{2894,3040},{2918,3200},{2940,3360},{2962,3520},{2983,3680}}<P>
<P>You can also set up a new USER_THERMISTORTABLE in their web firmware configuration tool.<P>
<P>R2 is the pullup resistor of thermistor pins.<P>

<P></P>
<P><B>C. Duet 3D board firmware setting</B><P>
<P>M305 P1 X501 R4700;heater 1 uses a PT1000 connected to thermistor channel 1 which has a 4.7K series resistor<P>
<P>M305 P1 X501 R1000;heater 1 uses a PT1000 connected to thermistor channel 1 which has a 1K series resistor<P>
<P>https://duet3d.dozuki.com/Wiki/Connecting_thermistors_or_PT1000_temperature_sensors<P>

<P></P>
<P><B>D. Smoothieware firmware setting:</B><P>
<P>Working on it please refer to<P>
<P>http://forum.smoothieware.org/forum/t-1086570/using-ptc-pt100-pt1000<P>
<P>You can choose PT100 and amplifier board instead,if you need more than 300C temperature.Please clickhere<P>
<P>http://smoothieware.org/pt100<P>
<P>TIPS:You can use the temperature input pin P0.23-P0.26 by remove the pullup resistor of that pin.When you connect the PT100 amplifier board to your smoothieboard or MKS SBASE.(we already tested it works)<P>

<P></P>
<P><B>E. HOW TO REPLACE THE PULLUP RESISTOR</B><P>
<P>1.Try to find any 472 or 4701 marks 'Rx' resistor near the thermistor input terminals.<P>
<P>2.Measure the 2pins of the terminal with a multimeter one pin should short to GND/AGND one should short to the one end of the pullup resistor<P>
<P>3.Replace it with your soldering iron and skills<P>
<P>4.Connect the PT1000 sensor like normal thermistor<P>
<P>5.Make the change to your firmware<P>
<P>6.If everything goes well the printer should show the room temperatures<P>

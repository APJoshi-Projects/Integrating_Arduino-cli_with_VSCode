Integrating Arduino-cli with Visual Studio Code
here are my -> instructions -> configuration files and -> userspace settings.
**supporting arduino uno, esp8266 and esp32**
-------------------------------------------------------------------------------

**In short**
1.  copy the required .vscode folder in your arduinosketch directory.
    directoty structure looks like below.
*****************************************
Directory of D:\Projects\Arduino\blink
[.vscode]   blink.ino
                  1 File(s)
                  1 Dir(s)
*****************************************
2. open blink.ino file in vscode editor.
3. click "Terminal" tab (Alt+t) >> click "RunTask"  >> click "ArduinoUno-Compile" for compile >> or/&
                                                    >> click "ArduinoUno-Upload" for upload.
**Note: check "COMport" mentioned in the "tasks.json" file. change it as necessary.**
-------------------------------------------------------------------------------

**In detail**
step-by-step instruction
1. Install Arduino-cli 
    i.  download and extract arduino-cli.exe, for example, at (C:\Program Files\Arduino\)
    ii. add this path(C:\Program Files\Arduino\) to your system environment variable.

2. open cmd and run the commands one by one.
    i.  arduino-cli config init
        a.  **this will create folder at (C:\Users\Ankur Joshi\AppData\Local\Arduino15\)**
            here, edit your "arduino-cli.yaml" file to look like the example file given below.
            **add "sketchlocation" and let both "sketchlocation" & "user" parameter values be the same.**
example arduino-cli.yaml
/************************
board_manager:
  additional_urls:
  - https://arduino.esp8266.com/stable/package_esp8266com_index.json
  - https://raw.githubusercontent.com/espressif/arduino-esp32/gh-pages/package_esp32_index.json
daemon:
  port: "50051"
directories:
  data: C:\Users\Your.User.Name\AppData\Local\Arduino15
  downloads: C:\Users\Your.User.Name\AppData\Local\Arduino15\staging
  sketchlocation: D:\Projects\Arduino
  user: D:\Projects\Arduino
logging:
  file: arduinoLogs.txt
  format: text
  level: info
telemetry:
  addr: :9090
  enabled: false
************************/ 
        b.  arduino-cli config init
            **run this command again for changes to take effect**
        c.  Reboot your PC.
    ii.   arduino-cli core update-index
    iii.  arduino-cli core install arduino:avr
    iv.   arduino-cli core install esp8266:esp8266
    v.    arduino-cli core install esp32:esp32
    vi.   (optional)arduino-cli lib search RF24
    Vii.  (optional)arduino-cli lib install RF24
          **notice that custom libraries will be saved in (D:\Projects\Arduino\libraries\)**
    Viii. exit and close cmd
          
3. Install Visual Studio Code and follow instructions
    i.    install "C/C++" and "Python" extention in vscode.
    ii.   create blink folder. like this -> (D:\Projects\Arduino\blink\)
    iii.  open this folder in vscode (D:\Projects\Arduino\blink\) and create blink.ino file as per below
example blink.ino
/*****************
#include <Arduino.h>
void setup() {
  pinMode(LED_BUILTIN, OUTPUT);
}
void loop() {
  digitalWrite(LED_BUILTIN, HIGH);
  delay(1000);
  digitalWrite(LED_BUILTIN, LOW);
  delay(1000);
}     
*****************/
    iii.  copy the required .vscode folder in your arduinosketch directory.
          and RENAME THE FOLDER TO .vscode
        ->directoty structure after copying looks like below.
*****************************************
Directory of D:\Projects\Arduino\blink
[.vscode]   blink.ino
                  1 File(s)
                  1 Dir(s)
*****************************************
    iv.   open blink.ino file in vscode editor.
    v.    click "Terminal" tab on top >> click "ArduinoUno-Compile" for compile >> or/&
                                      >> click "ArduinoUno-Upload" for upload.
**Note: check "COMport" mentioned in the "tasks.json" file. change it as necessary for upload.

1. .vscode for Arduino Uno (c_cpp_properties.json & task.json) <- Tested and working perfect.
2. .vscode for Esp8266 (c_cpp_properties.json & task.json) <- Not tested.
3. .vscode for Esp32 (c_cpp_properties.json & task.json) <- Work in progress.
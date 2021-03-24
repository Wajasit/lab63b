# การทดลองที่ 5 เรื่อง การเขียนโปรแกรมเชื่อมต่อไวไฟและเว็บเซอร์เวอร์
## วัตถุประสงค์ 
เพื่อศึกษาการชื่อมไวไฟโดยการใส่รหัสและชื่อ ภายในโปรแกรม และเว็บเซอร์เวอร์
## อุปกรณ์ที่ใช้ 
1. ไมโครคอนโทรลเลอร์ ESP-01
2. ซีเรียล
3. สาย USB
## ศึกษาข้อมูลเบื้องต้น 
https://www.youtube.com/watch?v=VX-QNQcO-b4
## วิธีการทำการทดลอง 
1. ต่อไมโครคอนโทรลเลอณกับซีเรียล
2. ทำการใส่ชื่อ และ รหัสไวไฟ
<img width="1410" alt="ภาพหน้าจอ " src="https://user-images.githubusercontent.com/80881019/112394110-bd5e0680-8d2e-11eb-8417-c55124204c23.png">

3. อัพโหลดโปรแกรม
<img width="1430" alt="ภาพหน้าจอ " src="https://user-images.githubusercontent.com/80881019/112394193-e2eb1000-8d2e-11eb-8faa-28e385c74eb9.png">
              #include <ESP8266WiFi.h>
              //#include <WiFiClient.h>
              #include <ESP8266WebServer.h>

              const char* ssid = "HI_BMFWIFI_2.4G";
              const char* password = "0819110933";

              ESP8266WebServer server(80);

              int cnt = 0;

              void setup(void){
                Serial.begin(115200);

                WiFi.mode(WIFI_STA);
                WiFi.begin(ssid, password);
                while (WiFi.status() != WL_CONNECTED) {
                  delay(500);
                  Serial.print(".");
                }
                Serial.print("\n\nIP address: ");
                Serial.println(WiFi.localIP());

                server.onNotFound([]() {
                  server.send(404, "text/plain", "Path Not Found");
                });

                server.on("/", []() {
                  cnt++;
                  String msg = "Hello cnt: ";
                  msg += cnt;
                  server.send(200, "text/plain", msg);
                });

                server.begin();
                Serial.println("HTTP server started");
              }

              void loop(void){
                server.handleClient();
              }
 4. ใช้คำสั่ง pio device monitor จะได้ip address แล้วนำ ip address ไปทดสอบในเบราว์เซอร์
## การบันทึกผลการทดลอง 
เราจะได้ที่อยู่ ip address มาแล้วนำไปใส่ในเว็บเบราว์เซอร์ เราจะได้ Hello 1 โดยจะเปลี่ยนจำนวนนับไปเรื่อยๆ
## อภิปรายผลการทดลอง 
จากการทดลองเราจะได้ip address จากตัวไมโครคอนโทรลเลอร์ที่ทำหน้าที่เป็นเว็บเซอร์เวอร์ และให้ ip address มา เพื่อที่จะนำไปทดลองเปิดในเว็บเบราว์เซอร์
## คำถามหลังการทดลอง
* Q:จากการทดลองหากเราใส่รหัสไวไฟผิดจะเกิดผลอย่างไร
* A:จะไม่สามารถใช้งานเว็บเบราว์เซอร์ได้

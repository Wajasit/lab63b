# การทดลองที่ 2 เรื่อง การเขียนโปรแกรมค้นหาไวไฟ
## วัตถุประสงค์ 
1. เพื่อทำการศึกษาการใช้งานตัวไมโครคอนโทรลเลอร์ในการค้นหาสัญญาณ wifi
## อุปกรณ์ที่ใช้ 
1. ไมโครคอนโทรลเลอร์ ESP-01
2. ซีเรียล
3. สาย USB 
## ศึกษาข้อมูลเบื้องต้น 
https://www.youtube.com/watch?v=yBjab0UNuB8
## วิธีการทำการทดลอง 
1. หลังจาการต่อตัวไมโครคอนโทรลเลอร์เรียบร้อยก็ทำการรันโปรแกรมเพื่ออัพโหลดคำสั่งต่อไปนี้ โดยใช้ทำสั่ง pio run -t upload
  #include <Arduino.h>
  #include <ESP8266WiFi.h>

  int cnt = 0;

  void setup()
  {
    Serial.begin(115200);
    WiFi.mode(WIFI_STA);
    WiFi.disconnect();
    delay(100);
    Serial.println("\n\n\n");
  }

  void loop()
  {
    Serial.println("========== เริ่มต้นแสกนหา Wifi ===========");
    int n = WiFi.scanNetworks();
    if(n == 0) {
      Serial.println("NO NETWORK FOUND");
    } else {
      for(int i=0; i<n; i++) {
        Serial.print(i + 1);
        Serial.print(": ");
        Serial.print(WiFi.SSID(i));
        Serial.print(" (");
        Serial.print(WiFi.RSSI(i));
        Serial.println(")");
        delay(10);
      }
    }
    Serial.println("\n\n");
  }
  <img width="1428" alt="image" src="https://user-images.githubusercontent.com/80881019/112375932-6cdaaf00-8d16-11eb-98f9-44c2068e21f4.png">
<img width="1428" alt="ภาพหน้าจอ 2564-03-25 เวลา 02 59 02" src="https://user-images.githubusercontent.com/80881019/112375991-7ebc5200-8d16-11eb-81fd-b26051d0ad09.png">

2. กดปุ่มทั้งสองเพื่อทำการอัพโหลดหลังรันคำสั่งอัพโหลด
3. ใช้คำสั่ง pio device monitor เพื่อแสดงผลการค้นหาwifi
4. ถ้าต้องการรีเซ็ตกดปุ่มสีแดง
## การบันทึกผลการทดลอง 
ตัวไมโครคอนโทรลเลอร์จะทำการแสกน wifi รอบๆออกมา
## อภิปรายผลการทดลอง 
หลังจากอัพโหลดโปรแกรมเข้าสู่ไมโครคอนโทรลเลอร์ ตัวไมโครคอนโทรลเลอร์จะทำการแสกนหาสัญญาณ wifi รอบๆว่ามีอะไรบ้าง
## คำถามหลังการทดลอง 
* Q:หากหาสัญญาณwifiไม่เจอเลยคาดว่าน่าจะเป็นเพราะเหตุใด
* A:ความแรงของสัญญาณ wifi 


![F9E9FEC4-74FD-4934-9F6A-9DED46921EE4](https://user-images.githubusercontent.com/102523600/162728677-ef0c08f3-6638-4635-9e44-5880f9b45112.jpeg)
# -
#include <SimpleDHT.h>
#include <Wire.h> 
#include <LiquidCrystal_I2C.h>        //헤더 파일,우리는 그냥 사용하면 된다
LiquidCrystal_I2C lcd(0x27,16,2);     //lcd에 표기할 수 있는 character의 수가 가로로 16개 세로로 2개임을 나타낸다, 0x27는 lcd의 주소를 나타냄

// for DHT11, 
//      VCC: 5V or 3V
//      GND: GND
//      DATA: 6
int pinDHT11 = 6;
SimpleDHT11 dht11(pinDHT11);

void setup() {
  Serial.begin(9600);
  lcd.init();                         // LCD 초기화
     lcd.backlight();                //LCD 백라이트
 
}
  
void loop() {
  // start working...
     Serial.println("=================================");
  Serial.println("Sample DHT11...");
  // read without samples.
  byte temperature = 0;
  byte humidity = 0;
  int err = SimpleDHTErrSuccess;
  if ((err = dht11.read(&temperature, &humidity, NULL)) != SimpleDHTErrSuccess) {
    Serial.print("Read DHT11 failed, err="); Serial.print(SimpleDHTErrCode(err));
    Serial.print(","); Serial.println(SimpleDHTErrDuration(err)); delay(1000);
    return;
  }
  
  Serial.print("Sample OK: ");
  Serial.print((int)temperature); Serial.print(" *C, "); 
  Serial.print((int)humidity); Serial.println(" H");
  lcd.clear();                    // LCD 초기화
     lcd.setCursor(0,0);             //LCD의 첫 번째 줄 첫 번째 자리를 나타냄
     lcd.print("temperature="); //LCD의 첫 번째 줄 첫 번째 자리에 Hello,Every one!을 표시함
     lcd.setCursor(12,0);             //LCD의 첫 번째 줄 첫 번째 자리를 나타냄
     lcd.print((int)temperature); //LCD의 첫 번째 줄 첫 번째 자리에 Hello,Every one!을 표시함
      lcd.setCursor(14,0);             //LCD의 첫 번째 줄 첫 번째 자리를 나타냄
     lcd.print((char)0xDF); //LCD의 첫 번째 줄 첫 번째 자리에 Hello,Every one!을 표시함
     lcd.setCursor(15,0);             //LCD의 첫 번째 줄 첫 번째 자리를 나타냄
     lcd.print("C"); //LCD의 첫 번째 줄 첫 번째 자리에 Hello,Every one!을 표시함
     lcd.setCursor(0,1);            //LCD의 두 번째 줄 첫 번째 자리를 나타냄
     lcd.print("humidity=");  //LCD의 두 번째 줄 첫 번째 자리에 Welcome Reader!를 표시함
      lcd.setCursor(9,1);            //LCD의 두 번째 줄 첫 번째 자리를 나타냄
     lcd.print((int)humidity);  //LCD의 두 번째 줄 첫 번째 자리에 Welcome Reader!를 표시함
     lcd.setCursor(11,1);            //LCD의 두 번째 줄 첫 번째 자리를 나타냄
     lcd.print("%");  //LCD의 두 번째 줄 첫 번째 자리에 Welcome Reader!를 표시함
  
  // DHT11 sampling rate is 1HZ.
  delay(1500);
}

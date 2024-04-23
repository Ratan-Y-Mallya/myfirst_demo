# link to tinkercad circuit:

https://www.tinkercad.com/things/e1ZmfHrHTB1-daring-waasa/editel?returnTo=%2Fdashboard&sharecode=8QgmZQiJV0E26FSVEhhn8y0zsrKrAgUAUoitFW4y4I4


## Code:
```
#include <LiquidCrystal_I2C.h>  
#include <Keypad.h>  
LiquidCrystal_I2C lcd_1(32, 16, 2);  
const byte ROWS = 4;  
const byte COLS = 4;  
#define Password_Length 5  
char Data[Password_Length];  
char Master[Password_Length] = "1234";  
int green = 13;  
int red =12;  
byte data_count = 0;  
char customKey;  

char hexaKeys[ROWS][COLS] = {  
  {'1', '2', '3', 'A'},  
  {'4', '5', '6', 'B'},  
  {'7', '8', '9', 'C'},  
  {'*', '0', '#', 'D'}  
};  
 

byte rowPins[ROWS] = {9, 8, 7, 6};  
byte colPins[COLS] = {5, 4, 3, 2};  
 

Keypad customKeypad = Keypad(makeKeymap(hexaKeys), rowPins, colPins, ROWS, COLS);  

 
void setup()  
{  
Serial.begin(9600);  

  lcd_1.init();  

  lcd_1.setCursor(0, 0);  
  lcd_1.backlight();  
  lcd_1.display();  
  pinMode(red, OUTPUT);  
  pinMode(green, OUTPUT);  
}  

  
void loop()  
{  
lcd_1.setCursor(0,0);  
  lcd_1.print("Enter Password:");  
customKey = customKeypad.getKey();  
  if (customKey) {  
    
    Data[data_count] = customKey;  
    lcd_1.setCursor(data_count, 1);  
    lcd_1.print(Data[data_count]);  
    data_count++;  
  }  
  if (data_count == Password_Length - 1) {  
    lcd_1.clear();  

    if (!strcmp(Data, Master)) {  
lcd_1.print("Correct");   
      digitalWrite(green, HIGH);  
      delay(5000);  
      digitalWrite(green, LOW);  
    }  
    else {  lcd_1.print("Incorrect");  
      digitalWrite(red, HIGH);  
      delay(5000);  
      digitalWrite(red, LOW);  
     }   
    lcd_1.clear();  
   clearData() ;  
  }  
}  
void clearData() {  
  
  while (data_count != 0) {  
    Data[data_count--] = 0;  
  }  
  return;  
}  
```

![Daring Waasa](https://github.com/Jokergif/D0--Virtual-Mouse-using-esp32cam/assets/161617838/6948c5ff-4ee9-4d3c-9f49-264b45367efb)


![Screenshot 2024-03-17 222415](https://github.com/Jokergif/D0--Virtual-Mouse-using-esp32cam/assets/161617838/eb02d236-0740-41a2-91f3-074350da7e66)


![Screenshot 2024-03-17 222425](https://github.com/Jokergif/D0--Virtual-Mouse-using-esp32cam/assets/161617838/80563a96-7ad2-43d2-ba5d-6b7ad6c56636)


![Screenshot 2024-03-17 222441](https://github.com/Jokergif/D0--Virtual-Mouse-using-esp32cam/assets/161617838/a4df8c2d-dde2-4a59-89d7-51d9f022adc6)



# Explaination of code:


* I have first included the necessary libraries.   
* Then I have initialised the I2C LCD screen and keypad.   
* I created an array of pasword of size 5 to store the pasword of 4 and size one null character.     
* Then I have set the pasword as 1234 in the code itself.  
* Then i connected the Led to the Arduino to the pin 13 and 12 .    
* Then the following code was to set the Keypad and the LCD.  
* Then in the loop I set the cursor of the sreen to (0,0) and made to ask to write the pasword.  
* Then on writing the pasword if the pasword is correct then the green LED will get on for 5 seconds  
* If the pasword is wrong then the red LED will glow for 5 seconds  
* Then i created a function clearData() to clear the element of the array Data or else if we dont use this function in loop then the lock will not ask you to write the pasword and it will consider  the previous written pasword if it is correct then it get stick to right and keep on printing "correct" and similar in the other case.  
* So Cleardata() is created to overcome the above problem  and  the previous data will be removed and then we can put some new pasword and the checking process will be the same.  




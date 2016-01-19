# Arduino-Boards
Palooka, Danger Zone, Sword of Justice and I
#Project for CP4
Lockdown mode:

#Current Code:
#include <Servo.h> 

int panicButton = 0;  //variable for the panic button (location)

int lights = 3;       //variable for lights (location)

byte leds = 0;        //variable for lights

boolean soundOn = true; //TO BE DELETED

int sound = 5;        //variable of PIN where the sound is located
int tones = 261;      //to be deleted

boolean servoSpin = false;

int servoPin = 7;
 
Servo servo;  
 
int angle = 0;   // servo position in degrees 

void setup(){
  pinMode(lights, OUTPUT);
  pinMode(panicButton, INPUT_PULLUP);

  digitalWrite(lights, HIGH); //TO BE DELETED

  servo.attach(servoPin); 
}

void loop() {
  
  if (digitalRead(panicButton) == LOW){ // if panic button is pressed
    digitalWrite(lights, LOW);          //turn off lights
    noTone(sound);                     // turns sound off
    soundOn = false;     // Sound off
    servoSpin = true;    // Start motor spin           
  }

  if (servoSpin == true){
    Spin();
  }
  
  if (digitalRead(panicButton) == HIGH){    // if panic button is on
    if (soundOn == true){      
      noTone(sound);           
      tone(sound, tones, 100);   // if sound is on turn tone to 100
    }
  }
}

void Spin(){
  for(int i; i < 180; i++){        // rotates at 180 degrees counterclockwise
    servo.write(i);
    delay(10);
  }
  servo.write(0);
};

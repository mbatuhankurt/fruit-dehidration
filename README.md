//# fruit-dehidration

#include <math.h>
#define ThermistorPin A0

int role=9;
int Vo;                                                                          //termistör
float R1 = 10000;
float logR2, R2, T,  Tf;
int Tc;
float c1 = 1.009249522e-03, c2 = 2.378405444e-04, c3 = 2.019202697e-07;
char veri;
int sveri;
int Slider1 = 11;  

void setup() {
  Serial.begin(9600); 
  
 pinMode(role,OUTPUT); 
 pinMode(Slider1,OUTPUT); 
 
 digitalWrite(role,HIGH);
 
}

void loop() {
 
  Vo = analogRead(ThermistorPin);
  R2 = R1 * (1023.0 / (float)Vo - 1.0);
  logR2 = log(R2);
  T = (1.0 / (c1 + c2*logR2 + c3*logR2*logR2*logR2));          //termistör okuma
  Tc = T - 273.15;
  Tf = (Tc * 9.0)/ 5.0 + 32.0; 
  
 Serial.print("Derece:");
 Serial.println(Tc);

 delay(1500);

  
    //--------------------------------------------------------------------------
  
  if(Serial.available())
  {
    veri = Serial.read();  //zaman                         //bluetooth okuma
    sveri = Serial.read(); // ısı     
  }

 
//-------------------------------------------------------------------------------
if(veri == 'K'){
      if(Tc <45 ){
       digitalWrite(role,LOW);
        Serial.println("mos açıldı");
          }
                                                             //ısıtma işlemi(45-60 derece)
            if(Tc > 60){
             digitalWrite(role,HIGH);
            Serial.println("mos kapandı");
    }
    Serial.println(veri);
}
//--------------------------------------------------------------------
if(veri == 'L'){
      if(Tc <55 ){
       digitalWrite(role,LOW);
        Serial.println("mos açıldı");
          }
                                                             //ısıtma işlemi(55-70derece)
            if(Tc > 70){
             digitalWrite(role,HIGH);
            Serial.println("mos kapandı");
    }
    Serial.println(veri);
}
//-----------------------------------------------------------------------------------
if(veri == 'M'){
      if(Tc <60 ){
       digitalWrite(role,LOW);
        Serial.println("mos açıldı");
          }
                                                             //ısıtma işlemi(60-75 derece)
            if(Tc > 75){
             digitalWrite(role,HIGH);
            Serial.println("mos kapandı");
    }
    Serial.println(veri);
}
//--------------------------------------------------------------------
if(veri == 'N'){
      if(Tc <40 ){
       digitalWrite(role,LOW);
        Serial.println("mos açıldı");
          }
                                                             //ısıtma işlemi(40-50 derece)
            if(Tc > 50){
             digitalWrite(role,HIGH);
            Serial.println("mos kapandı");
    }
    Serial.println(veri);
}
  
//-----------------------------------------------------------------------------------
  
   
   
 if(sveri  > 0 ){ 
   analogWrite(Slider1,sveri );                                  //fan(0-100 hızında)
   Serial.println(sveri );
  }
 
}
  

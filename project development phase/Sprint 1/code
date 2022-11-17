#include <time.h>

bool exhaust_fan_on = false;
bool sprinkler_on = false;

float temperature  = 0;
int gas = 0;
int flame = 0;

String flame_status = "";
String accident_status = "";
String sprinkler_status = "";

void setup() {
    Serial.begin(99900);
}

void loop() {

    //setting a random seed

    srand(time(0));

    //initial variable

    temperature = random(-20,125);
    gas = random(0,1000);
    int flamereading = random(200,1024);
    flame = map(flamereading,0,1024,0,2);

    //set a flame status

    switch (flame) {
    case 0:
        flame_status = "No Fire";
        break;
    case 1: 
        flame_status = "Fire is Detected";
        break;
    }

    //send the sprinkler status
    if(flame==1){
        sprinkler_status = "Working";
        sprinkler_on = true;
    }
    else{
        sprinkler_status = "Not Working";
        sprinkler_on = false;

    }

    //toggle the fan according to gas

    if(gas > 100){
        exhaust_fan_on = true;
    }
    else{
        exhaust_fan_on = false;
    }

    String payload = "{\"senor_values\":{";
  payload+="\"gas\":";
  payload+=gas;
  payload+=",";
  payload+="\"temperature\":";
  payload+=(int)temperature;
  payload+=",";
  payload+="\"flame\":";
  payload+=flamereading;
  payload+=",";
  
  payload+="\"output\":{";
  payload+="\"exhaust_fan_on\":"+String((exhaust_fan_on)?"true":"false")+",";
  payload+="\"sprinkler_on\":"+String((sprinkler_on)?"true":"false")+"";
  payload+="},";
  payload+="\"messages\":{";
  payload+="\"fire_status\":\""+flame_status+"\",";
  payload+="\"flow_status\":\""+sprinkler_status+"\",";
  payload+="}";
  payload+="}";
  Serial.println(payload);
  
    Serial.println("");
    Serial.println("");
    Serial.println(" -------------------------*************---------------------");
    Serial.println("");
    Serial.println("");
    delay(3000);
}

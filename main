# include <SoftwareSerial.h>
#include <Servo.h>
SoftwareSerial Bluetooth(1,2); //RX|TX

Servo serv1;
Servo serv2;
Servo serv3;
Servo serv4;


// servo current position 
int serv1pos,serv2pos,serv3pos,serv4pos;

//previous position 
 int serv1pre_pos,serv2pre_pos,serv3pre_pos,serv4pre_pos;

// array data
int serv1data[50], serv2data[50],serv3data[50],serv4data[50];
int index = 0; // keep track of array 
String data = ""; // to get info form data 

void setup() {
  // setup servo
   servo_attach();

 // start bluetooth 38400 is the default baud rate 
   Bluetooth.begin(38400); 
   Bluetooth.setTimeout(1); // settimeout what for stream data ms 
   delay(10);
   initalposition();
}

void loop() {
  // check if data is being sent
  if (Bluetooth.available() > 0){
    data = Bluetooth.readString();
    if (data.startsWith("M1")){ // we added s1 in the app to distinguish which motor is being moved 
      String data_sl = data.substring(2,data.length()); // dont need s1 just the #
      serv1pos = data_sl.toInt();
      // from current postion to data we use loop for a swift motion
      
      if (serv1pre_pos > serv1pos){ // if pre > current we decrement 
        for(int i = serv1pre_pos; i  >= serv1pos; i--){
          serv1.write(i);  
          delay(20); // "creates" a speed at which motor move 
        }
      }
      
      if (serv1pre_pos < serv1pos){ // if pre < current we increment
        for (int i = serv1pre_pos; i <= serv1pos; i++){
          serv1.write(i);
          delay(20);
        }
      }
      // once servopos is reached we make pre = current 
      serv1pre_pos = serv1pos;
    }
    // as servo1 we follow the same steps for other servo 
    // if the slider2  is moved 

    if (data.startsWith("M2")){
      String data_S2 = data.substring(2,data.length());
      serv2pos = data_S2.toInt();

      if ( serv2pre_pos > serv2pos){
        for (int i = serv2pre_pos; i >= serv2pos; i--){
          serv2.write(i);
          delay(30);
        }

      }
      if(serv2pre_pos< serv2pos){
        for (int i = serv1pre_pos; i <= serv2pos; i++){
          serv2.write(i);
          delay(30); 
        }
      }
       serv2pre_pos = serv2pos;
    }
    
   
   if(data.startsWith("M3")){
    String data_S3 = data.substring(2,data.length());
    serv3pos = data_S3.toInt();
    
    if ( serv3pos > serv3pre_pos){
      for (int i = serv3pre_pos; i <= serv3pos; i++){
        serv3.write(i);
        delay(40);
      }
    }
    if(serv3pos < serv3pre_pos){
      for (int i = serv3pre_pos; i >= serv3pos; i--){
        serv3.write(i);
        delay(40);
      }
    }
    serv3pre_pos = serv3pos;
   }
   
   
   if (data.startsWith("M4")){
    String data_S4 = data.substring(2,data.length());
    serv4pos = data_S4.toInt();
    
    if (serv4pos > serv4pre_pos){
      for (int i = serv4pre_pos; i <= serv4pos;i++){
        serv4.write(i);
        delay(50); // test to make sure delay speed is prefect for you
      }
    }
    if (serv4pre_pos > serv4pos){
     for (int i = serv4pre_pos; i >= serv4pos; i--){
      serv4.write(i);
      delay(50);
      }
    }
    serv4pre_pos = serv4pos;
   }

  // save the pos
  if (data == "Save"){
    serv1data[index] = serv1pos;  
    serv2data[index] = serv2pos;
    serv3data[index] = serv3pos;
    serv4data[index] = serv4pos;
    index++;
  }
  // want to run the save data
  if (data == "run"){
    // if stop button is presd any time 
   if (Bluetooth.available()>0 ){
      if (data ==  "Stop"){
        while(1);
      }
   }
    for(int i = 0 ; i <= index;i++){
      // if equal we do nothing
      if (serv1data[i] == serv1data[i+1]){
        // nothing happens 
      }
      if (serv1data[i] > serv1data[i+1]){
        for (int j = serv1data[i]; j <= serv1data[i+1];j--){
          serv1.write(i);
          delay(30);
        }
      }
      if (serv1data[i] < serv1data[i+1]){
        for (int j = serv1data[i]; j <= serv1data[i+1]; j++){
          serv1.write(j);
          delay(30);       
    }
   
    }
    
      if (serv2data[i] == serv2data[i+1]){
        
      }
      if (serv2data[i] > serv2data[i+1]){
        for (int j = serv2data[i] ; j >= serv2data[i+1];j--){
          serv2.write(j);
          delay(30);     
        }
    }

    if (serv2data[i] < serv2data[i+1]){
      for (int j = serv2data[i] ; j <= serv2data[i+1]; i ++){
        serv2.write(j);
        delay(30);
      }
    }

    // motor 3 
    if (serv3data[i] == serv3data[i+1]){
      //do nothing 
    }

    if ( serv3data[i] > serv3data[i+1]){
      for (int j = serv3data[i] ; j >= serv3data[i+1]; j--){
        serv3.write(j);
        delay(30);
      }
    }
    if (serv3data[i] < serv3data[i+1]){
      for (int j = serv3data[i]; j <= serv3data[i+1]; j++){
        serv3.write(j);
        delay(30);
      }
    }

    // motor 4 
    if (serv4data[i] == serv4data[i+1]){
      // do nothing
    }

    if (serv4data[i] > serv4data[i+1]){
      for (int j  = serv4data[i]; j >= serv4data[i+1]; j--){
        serv4.write(j);
        delay(30);
      }
    }
    if (serv4data[i] < serv4data[i+1]){
      for (int j =  serv4data[i]; j <= serv4data[i+1]; j++){
        serv4.write(j);
        delay(30);
      }
     }
   }  
 }

  if (data == "reset"){
    // set array to zero
    /*
     * str − This is a pointer to the block of memory to fill.

        c − This is the value to be set. The value is passed as an int, but the function fills the block of memory using the unsigned char conversion of this value.

        n − This is the number of bytes to be set to t 
     */
    memset(serv1data, 0,sizeof(serv1data));
    memset(serv2data,0, sizeof(serv2data));
    memset(serv3data, 0, sizeof (serv3data));
    memset(serv4data, 0, sizeof(serv4data));
    index = 0; // set index back to zero if array "clear"
  }
     
 }
}


  
 static void initalposition(){
    // the arm postion when it turns on 
    serv1pos = 90; // postion depend on the motor check first to see if anglr fits ur need 
    serv1.write(serv1pos);
    serv2pos = 150;
    serv2.write(serv2pos);
    serv3pos = 35;
    serv3.write(serv3pos);
    serv4pos = 140;
    serv4.write(serv4pos);
  }
  static void servo_attach(){
    serv1.attach(5);
    serv2.attach(6);
    serv3.attach(7);
    serv4.attach(8);
  }

# bluno-led-potentiometer-intro
void setup() {
  // put your setup code here, to run once:
  Serial.begin(115200);
  pinMode(2,OUTPUT);
  pinMode(A0, INPUT);

}

void loop() {
  // put your main code here, to run repeatedly:
  int sensorReading = analogRead(A0);
  byte buffer[3] = {
    0xAD,
    (byte)(sensorReading),
    (byte)(sensorReading >> 8)
  };

  Serial.write(buffer, sizeof(buffer));
  if(Serial.available())
  {
    byte cmd = Serial.read();
    if(cmd == 0x01)
    {
      digitalWrite(2, HIGH);
    }
    else
    if(cmd == 0x02)
    {
      digitalWrite(2, LOW);
    }
  }
  delay(200);
}

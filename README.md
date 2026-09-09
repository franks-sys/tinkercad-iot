## Pista de pouso

![Pista de pouso](./assets/Poste%20com%20led%20fotoresistor%20com%20arduino.png)

```cpp
int fotoresistor = A0;
int leds[] = {2, 3, 4, 5, 6, 7, 8, 9, 10, 11};

void setup() {
  for (int i = 0; i < 10; i++) {
    pinMode(leds[i], OUTPUT);
  }

  pinMode(fotoresistor, INPUT);
  Serial.begin(9600);
}

void loop() {
  int luminosidade = analogRead(fotoresistor);
  Serial.println(luminosidade);

  int quantidade = map(luminosidade, 1023, 743, 0, 10);
  quantidade = constrain(quantidade, 0, 10);

  for (int i = 0; i < 10; i++) {
    if (i < quantidade) {
      digitalWrite(leds[i], HIGH);
    } else {
      digitalWrite(leds[i], LOW);
    }
  }

  delay(100);
}

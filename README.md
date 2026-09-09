## Pista de pouso



![](/assets/Poste com led fotoresistor com arduino.png)



```C

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

    }

    else {

      digitalWrite(leds[i], LOW);

    }

  }



  delay(100);

}

```



## Micro servo



![](/Prints/microservo.png)



```C

#include <Servo.h>



Servo servo;



int potenc = 0;

int angulo = 0; 



void setup(){ 

  servo.attach(11); 

} 



void loop(){ 



  potenc = analogRead(0); 



  angulo = map(potenc, 0, 1023, 0, 180);



  servo.write(angulo); 

  delay(15); 



}



```



## Semaforo e Pedestre



![Semáforo](/Prints/semaforo.png)



```C

// SEMÁFORO 1

const int verde1 = 10;

const int amarelo1 = 9;

const int vermelho1 = 8;



// SEMÁFORO 2

const int verde2 = 13;

const int amarelo2 = 12;

const int vermelho2 = 11;



// SEMÁFORO 3 - PEDESTRES

const int verde3 = 7;

const int vermelho3 = 6;



void setup() {

  pinMode(verde1, OUTPUT);

  pinMode(amarelo1, OUTPUT);

  pinMode(vermelho1, OUTPUT);



  pinMode(verde2, OUTPUT);

  pinMode(amarelo2, OUTPUT);

  pinMode(vermelho2, OUTPUT);



  pinMode(verde3, OUTPUT);

  pinMode(vermelho3, OUTPUT);



  // Estado inicial seguro

  digitalWrite(verde1, LOW);

  digitalWrite(amarelo1, LOW);

  digitalWrite(vermelho1, HIGH);



  digitalWrite(verde2, LOW);

  digitalWrite(amarelo2, LOW);

  digitalWrite(vermelho2, HIGH);



  // Pedestre começa vermelho

  digitalWrite(verde3, LOW);

  digitalWrite(vermelho3, HIGH);



  delay(500);

}



void loop() {



  digitalWrite(vermelho1, LOW);

  digitalWrite(verde1, HIGH);



  digitalWrite(amarelo2, LOW);

  digitalWrite(vermelho2, HIGH);



  digitalWrite(verde3, LOW);

  digitalWrite(vermelho3, HIGH);



  delay(2500);



  digitalWrite(verde1, LOW);

  digitalWrite(amarelo1, HIGH);



  digitalWrite(verde3, LOW);

  digitalWrite(vermelho3, HIGH);



  delay(500);



  digitalWrite(amarelo1, LOW);

  digitalWrite(vermelho1, HIGH);



  digitalWrite(vermelho2, LOW);

  digitalWrite(verde2, HIGH);



  digitalWrite(verde3, LOW);

  digitalWrite(vermelho3, HIGH);



  delay(2500);



  digitalWrite(verde2, LOW);

  digitalWrite(amarelo2, HIGH);



  digitalWrite(verde3, LOW);

  digitalWrite(vermelho3, HIGH);



  delay(500);



  digitalWrite(amarelo2, LOW);

  digitalWrite(vermelho2, HIGH);



  digitalWrite(vermelho1, HIGH);



  digitalWrite(vermelho3, LOW);

  digitalWrite(verde3, HIGH);



  delay(2500);



  digitalWrite(verde3, LOW);

  digitalWrite(vermelho3, HIGH);



  delay(500);

}

```



## Poste com led e fotoresistor



![Poste](/Prints/Poste.png)



## Display 7 segmentos



![Display](/Prints/display.png)



```C





```



## Portão



![Portão](/Prints/Portão.png) 


# Atividades - IOT

# 📚 Conteúdos

- Dashboard Web
- Experimento 01 - Poste com LED e Fotoresistor
- Experimento 02 - Semáforo de duas vias e pedestre
- Experimento 03 - Pista de pouso
- Experimento 04 - Servo motor com potenciômetro
- Experimento 05 - Display de 7 segmentos
- Experimento 06 - Portão eletrônico


---

# 🌐 Dashboard Web


- 📊 Gráfico diário
- 📊 Gráfico semanal
- 📋 Tabela com os registros
- 📅 Data dos acionamentos
- 🕐 Horário dos acionamentos
- 📆 Semana correspondente

## 🛠️ Tecnologias utilizadas

- HTML
- CSS
- JavaScript
- Chart.js
- CSV


## 🖥️ Prints

### Gráfico diário
<p align="center">
  <img src="assets/Tela (1).png" width="700">
</p>

### Gráfico semanal

<p align="center">
  <img src="assets/Tela (2).png" width="700">
</p>

### Tabela

<p align="center">
  <img src="assets/Tela (3).png" width="700">
</p>

---

# 💡 Experimentos

## 🔆 Experimento 01 - Poste com LED e Fotoresistor

### 📌 Objetivo

Criar um sistema de iluminação automática utilizando um **LED e um fotoresistor (LDR)**.

O sistema com Arduino identifica a quantidade de luz no ambiente:

- ☀️ Durante o dia: o LED permanece apagado.
- 🌙 Durante a noite: o LED acende.

Também foi realizada uma versão **sem Arduino**, utilizando apenas componentes eletrônicos.

---

### 🔌 Circuito sem Arduino

<p align="center">
  <img src="assets/Poste.png" width="600">
</p>


---

# 🚦 Experimento 02 - Semáforo de duas vias e pedestre

### 📌 Objetivo

Criar um sistema de semáforo utilizando Arduino, contendo:

- 🚦 Semáforo da primeira via
- 🚦 Semáforo da segunda via
- 🚶 Semáforo para pedestres
- 🔴 LEDs vermelhos
- 🟡 LEDs amarelos
- 🟢 LEDs verdes

O Arduino controla a sequência de funcionamento dos semáforos utilizando diferentes intervalos de tempo.

---

### 🔌 Circuito

<p align="center">
  <img src="assets/semaforo.png" width="600">
</p>

### 💻 Código

```c
const int verde1 = 10;
const int amarelo1 = 9;
const int vermelho1 = 8;

const int verde2 = 13;
const int amarelo2 = 12;
const int vermelho2 = 11;

void setup() {
  pinMode(verde1, OUTPUT);
  pinMode(amarelo1, OUTPUT);
  pinMode(vermelho1, OUTPUT);

  pinMode(verde2, OUTPUT);
  pinMode(amarelo2, OUTPUT);
  pinMode(vermelho2, OUTPUT);

  digitalWrite(verde1, LOW);
  digitalWrite(amarelo1, LOW);
  digitalWrite(vermelho1, HIGH);

  digitalWrite(verde2, LOW);
  digitalWrite(amarelo2, LOW);
  digitalWrite(vermelho2, HIGH);

  delay(500);
}

void loop() {

  digitalWrite(vermelho1, LOW);
  digitalWrite(verde1, HIGH);

  digitalWrite(amarelo2, LOW);
  digitalWrite(vermelho2, HIGH);

  delay(2500); 

  digitalWrite(verde1, LOW);
  digitalWrite(amarelo1, HIGH);

  delay(500); 
  digitalWrite(amarelo1, LOW);
  digitalWrite(vermelho1, HIGH);

  digitalWrite(vermelho2, LOW);
  digitalWrite(verde2, HIGH);

  delay(2500); 

  digitalWrite(verde2, LOW);
  digitalWrite(amarelo2, HIGH);

  delay(500); 


  digitalWrite(amarelo2, LOW);
  digitalWrite(vermelho2, HIGH);

}
```

---

# ✈️ Experimento 03 - Pista de pouso com LEDs

### 📌 Objetivo

Criar uma representação de uma **pista de pouso** utilizando vários LEDs controlados por um Arduino.

Os LEDs acendem em sequência, criando um efeito de iluminação semelhante às luzes de uma pista de pouso.

---

### 🔌 Circuito

<p align="center">
  <img src="assets/Pista_de_pouso.png" width="600">
</p>

### 💻 Código

```c
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

---

# ⚙️ Experimento 04 - Servo motor com potenciômetro

### 📌 Objetivo

Controlar a posição de um **servo motor** utilizando um **potenciômetro**.

O valor lido pelo potenciômetro é convertido para um ângulo entre **0° e 180°**, fazendo com que o servo motor acompanhe a posição do potenciômetro.

Também foi utilizado um capacitor no circuito.

---

### 🔌 Circuito

<p align="center">
  <img src="assets/microservo.png" width="600">
</p>

### 💻 Código

```c
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

---

# 🔢 Experimento 05 - Display de 7 segmentos

### 📌 Objetivo

Controlar um **display de 7 segmentos** utilizando Arduino.

O circuito utiliza um potenciômetro para realizar a alteração dos números apresentados no display.

Também foi realizado um desafio envolvendo display.

---

### 🔌 Circuito

<p align="center">
  <img src="assets/numero_potenciometro.png" width="600">
</p>

### 💻 Código

```c
int pins[7] = {4, 5, 6, 7, 8, 9, 10};

const byte numeros[10][7] = {
  {0,0,0,0,0,0,1}, // 0
  {1,0,0,1,1,1,1}, // 1
  {0,0,1,0,0,1,0}, // 2
  {0,0,0,0,1,1,0}, // 3
  {1,0,0,1,1,0,0}, // 4
  {0,1,0,0,1,0,0}, // 5
  {0,1,0,0,0,0,0}, // 6
  {0,0,0,1,1,1,1}, // 7
  {0,0,0,0,0,0,0}, // 8
  {0,0,0,0,1,0,0}  // 9
};

void setup() {
  for (int i = 0; i < 7; i++) {
    pinMode(pins[i], OUTPUT);
  }
}

void loop() {
  int valorPot = analogRead(A0);            
  int num = map(valorPot, 0, 1023, 0, 9);  
 
  exibirNumero(num);
  delay(50);
}

void exibirNumero(int n) {
  for (int i = 0; i < 7; i++) {
    digitalWrite(pins[i], numeros[n][i]);
  }
}
```

### 🔌 Circuito com 2 displays

<p align="center">
  <img src="assets/display.png" width="600">
</p>

### 💻 Código

```c
int ledpins[] = {4,5,6,7,8,9,10,11};
byte digits[] = {
  B11111100,
  B01100000,
  B11011010,
  B11110010,
  B01100110,
  B10110110,
  B10111110,
  B11100000,
  B11111110,
  B11110110,
  B00000001
};
int uni = 0;
int dez = 0;
int disp[] = {12,3};

void setup()
{
  for (int i =0;i<8;i++){
    pinMode(ledpins[i],OUTPUT);
  }
  pinMode(disp[0],OUTPUT);
  pinMode(disp[1],OUTPUT);
  pinMode(A0,INPUT);
}

void loop()
{
  int pot = map(analogRead(A0),0,1023,0,50);
  dez = pot % 10;
  uni = pot - dez * 10;
  displayDuplo(dez,uni);
}

void displayDigit(int digit)
{
  for (int i =0;i<8;i++){
    digitalWrite(ledpins[i],!bitRead(digits[digit],7-i));
  }
}

void displayDuplo(int d1, int d2){
  int d[] = {d2,d1};
  for(int i = 0; i < 2; i++){
	digitalWrite(disp[i],1);
	displayDigit(d[i]);
	delay(5);
	digitalWrite(disp[i],0);
	delay(5);
  }
}

```

---

# 🚧 Experimento 06 - Simulador de portão eletrônico com Arduino

### 📌 Objetivo

Criar um simulador de portão eletrônico utilizando Arduino, botões, sensores de fim de curso, relés e LEDs.

O sistema permite simular a abertura e o fechamento do portão.

O Arduino identifica o estado do portão e controla o motor através dos relés.

---

### 🔌 Circuito

<p align="center">
  <img src="assets/Portão.png" width="600">
</p>

### 💻 Código

```c
int fimAbre = 4;
int fimFecha = 2;
int comando = 8;
int liga = 12;
int direcao = 13;
int led1 = 9;
int led2 = 10;
bool movimento = false;
int esquerda = 1;

void setup()
{
  pinMode(fimAbre, INPUT);
  pinMode(fimFecha, INPUT);
  pinMode(comando, INPUT);
  pinMode(liga, OUTPUT);
  pinMode(direcao, OUTPUT);
  pinMode(led1, OUTPUT);
  pinMode(led2, OUTPUT);
  Serial.begin(9600);
}

void loop(){
	sinalizacao();
	int com = digitalRead(comando);
	int paraDeAbrir = digitalRead(fimAbre);
	int paraDeFechar = digitalRead(fimFecha);
	if(com == 1){
      if(movimento){
			movimento = parado();
      	}else{
      		if(esquerda == 1){
      			movimento = fechando();
				esquerda = 0;
      		}else{
        		movimento = abrindo();
				esquerda = 1;
      		}
      	}
    }
	if(paraDeAbrir == 1 || paraDeFechar == 1){
    	if(movimento){
			movimento = parado();
      	}
	}
}

void sinalizacao(){
	digitalWrite(led1,1);  
	digitalWrite(led2,0);
  	delay(200);
	digitalWrite(led1,0);  
	digitalWrite(led2,1);
	delay(200);
}

bool abrindo(){
    digitalWrite(direcao,0);
	digitalWrite(liga,1);
	Serial.println("Abrindo");
	return true;
}

bool fechando(){
    digitalWrite(direcao,1);
	digitalWrite(liga,1);
  	Serial.println("Fechando");
  	return true;
}

bool parado(){
	digitalWrite(liga,0);
	Serial.println("Parado");
	return false;
}

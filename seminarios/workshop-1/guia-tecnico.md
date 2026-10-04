# Guia Técnico das Bancadas Práticas
<!--
## Estação 1: Goniometria Articular Eletrônica (ROM)

### Objetivo clínico
Medição da amplitude de movimento (Range of Motion) de articulações como cotovelo, joelho ou punho em tempo real.

### Componentes
- 1x MPU-9250 (ou GY-521)
- 1x Arduino Nano (ou ESP32)
- 1x Display LCD 1602A (ligação em paralelo)

### Pinagem
- MPU-9250 / LCD I2C:
  - VCC ➔ 5V (ou 3.3V no ESP32)
  - GND ➔ GND
  - SDA ➔ A4 (Arduino Nano) ou GPIO 21 (ESP32)
  - SCL ➔ A5 (Arduino Nano) ou GPIO 22 (ESP32)
 
### Esquema de Ligação em Paralelo (LCD 1602A no Arduino Nano / UNO)
| Pino do LCD 1602A | Nome do Pino | Conexão no Arduino / Circuito | Função |
|-------------------|--------------|------------------------------|--------|
| Pino 1 | VSS | GND | Alimentação GND |
| Pino 2 | VDD | 5V | Alimentação lógica (+5V) |
| Pino 3 | V0 | Pino central do potenciômetro 10kΩ | Ajuste de contraste (extremidades do pot. em 5V e GND) |
| Pino 4 | RS | Pino digital D12 | Seleção de registro (comando/dado) |
| Pino 5 | R/W | GND | Leitura/escrita (GND força modo escrita) |
| Pino 6 | E | Pino digital D11 | Sinal de habilitação (Enable) |
| Pinos 7 a 10 | D0 a D3 | Desconectados | Não utilizados no modo de 4 bits |
| Pino 11 | D4 | Pino digital D5 | Linha de dados D4 |
| Pino 12 | D5 | Pino digital D4 | Linha de dados D5 |
| Pino 13 | D6 | Pino digital D3 | Linha de dados D6 |
| Pino 14 | D7 | Pino digital D2 | Linha de dados D7 |
| Pino 15 | A (Anodo) | 5V (via resistor 220Ω) | Luz de fundo (Backlight +) |
| Pino 16 | K (Catodo) | GND | Luz de fundo (Backlight -) |


### Código exemplo

```cpp
// =====================================================================
// ESTAÇÃO 1: Goniômetro Digital Articular (ROM)
// Display LCD 1602A em Modo Paralelo (4 bits) + Sensor MPU-9250 / GY-521
// =====================================================================

#include <Wire.h>
#include <MPU6050.h>        // Compatível com MPU-6050 / MPU-6500 / MPU-9250
#include <LiquidCrystal.h>  // Biblioteca padrão para modo paralelo (sem I2C)

// Inicializa a biblioteca definindo os pinos: LiquidCrystal(RS, Enable, D4, D5, D6, D7)
LiquidCrystal lcd(12, 11, 5, 4, 3, 2);
MPU6050 mpu;

void setup() {
  Wire.begin();
  Serial.begin(115200);

  // Define a dimensão do LCD (16 colunas x 2 linhas)
  lcd.begin(16, 2);
  mpu.initialize();

  // Mensagem inicial de calibração
  lcd.setCursor(0, 0);
  lcd.print("Goniometro ROM");
  lcd.setCursor(0, 1);
  lcd.print("Iniciando...");
  delay(1200);
  lcd.clear();
}

void loop() {
  int16_t ax, ay, az;
  mpu.getAcceleration(&ax, &ay, &az);

  // Cálculo do ângulo de inclinação articular (Pitch)
  float angle = atan2((float)ay, (float)az) * 180.0 / M_PI;

  // Exibição no LCD 1602A Paralelo
  lcd.setCursor(0, 0);
  lcd.print("AngArtic: ");
  lcd.print(angle, 1);
  lcd.print(" deg ");

  lcd.setCursor(0, 1);
  if (abs(angle) < 15.0) {
    lcd.print("Status: Repouso ");
  } else {
    lcd.print("Status: Em Mov. ");
  }

  // Saída Serial para monitoramento no computador
  Serial.println(angle);
  delay(120);
}
```

---

## Estação 2: Mapeamento de Pressão Plantar e Preensão com ADC ADS1115 (16 bits)

### Objetivo clínico
Medição de força de preensão palmar ou distribuição de carga sob os pés com alta precisão analógica.

### Componentes
- 2x Sensores FSR
- 2x Resistores 10kΩ
- 1x Módulo ADS1115 I2C
- 1x Arduino UNO (ou ESP32)

### Pinagem
- FSR 1 (Calcanhar) ➔ entrada A0 do ADS1115 + resistor 10kΩ para GND
- FSR 2 (Antepé) ➔ entrada A1 do ADS1115 + resistor 10kΩ para GND
- ADS1115:
  - VDD ➔ 5V
  - GND ➔ GND
  - SDA ➔ A4 (UNO) / GPIO 21 (ESP32)
  - SCL ➔ A5 (UNO) / GPIO 22 (ESP32)

### Código exemplo

```cpp
#include <Wire.h>
#include <Adafruit_ADS1X15.h>

Adafruit_ADS1115 ads;

void setup() {
  Serial.begin(115200);
  ads.begin();
  ads.setGain(GAIN_ONE);
}

void loop() {
  int16_t adc0 = ads.readADC_SingleEnded(0);
  int16_t adc1 = ads.readADC_SingleEnded(1);

  float volts0 = ads.computeVolts(adc0);
  float volts1 = ads.computeVolts(adc1);

  Serial.print("Calcanhar (V): "); Serial.print(volts0, 3);
  Serial.print(" | Antepe (V): "); Serial.println(volts1, 3);
  delay(150);
}
```

---

## Estação 3: Órtese Ativa e Garra Assistiva em Malha Fechada

### Objetivo clínico
Atuação robótica acionada por intenção do usuário. Ao aplicar pressão no sensor FSR, o motor MG946R aciona a garra ou suporte mecânico.

### Componentes
- 1x Servo Motor MG946R
- 1x Módulo LM2596 DC-DC
- 1x Sensor FSR + Resistor 10kΩ
- 1x Arduino Mega (ou ESP32)

### Pinagem e alimentação segura
- Alimentação do Servo: Fonte externa 9V–12V ➔ entrada do LM2596
- Ajustar o trimpot para 6.0V DC
- Saída do LM2596 ➔ VCC e GND do servo
- Pino de sinal: cabo laranja do servo ➔ D9 (Arduino Mega/UNO) ou GPIO 13 (ESP32)
- Atenção: interligar o GND do LM2596 ao GND do Arduino/ESP32

### Código exemplo

```cpp
#include <Servo.h>

Servo orteseServo;
const int fsrPin = A0;
const int thresholdForce = 300;

void setup() {
  orteseServo.attach(9);
  orteseServo.write(0);
  Serial.begin(115200);
}

void loop() {
  int fsrVal = analogRead(fsrPin);
  Serial.print("Forca FSR: "); Serial.println(fsrVal);

  if (fsrVal > thresholdForce) {
    orteseServo.write(90);
  } else {
    orteseServo.write(0);
  }

  delay(50);
}
```

---

## Dicas de suporte para os facilitadores

- **Ruído ou oscilação do Servo MG946R:** verificar se o GND da fonte do conversor LM2596 está conectado ao GND do microcontrolador.
- **Alimentação:** não conectar o VCC do servo ao pino 5V do Arduino, pois o motor exige picos de corrente.
- **Diálogo clínico:** orientar os alunos de tecnologia a conversar com fisioterapeutas ou profissionais do CER sobre ajustes de limiar para pacientes com diferentes níveis de força muscular.

---

## Objetivo pedagógico da bancada

A bancada prática tem como objetivo demonstrar de forma acessível e aplicada como conceitos de sensores, processamento analógico, microcontroladores e atuação mecânica podem ser integrados em sistemas biomédicos de apoio à reabilitação.
-->

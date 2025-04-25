
# Sistema de Monitoramento de Luminosidade com Arduino

## 💡 Descrição do Projeto

Este projeto foi desenvolvido como parte do curso de Engenharia de Software na FIAP, no contexto do Checkpoint 01 da disciplina *Edge Computing & Computer Systems*. A proposta consistia na criação de um sistema de monitoramento da luminosidade do ambiente onde são armazenados vinhos na Vinheria Agnello. O objetivo era garantir condições ideais de armazenamento, alertando sobre níveis inadequados de luz que possam comprometer a qualidade dos vinhos.

O sistema utiliza um sensor LDR conectado a um Arduino UNO para medir a intensidade luminosa, e sinaliza os diferentes níveis com LEDs e um buzzer. A simulação foi realizada na plataforma Wokwi.

## 🛠️ Tecnologias e Componentes Utilizados

- **Arduino UNO**
- **Sensor LDR (Light Dependent Resistor)**
- **Resistor de 10kΩ** (para divisor de tensão com o LDR)
- **3 LEDs** (verde, amarelo e vermelho)
- **3 resistores de 220Ω** (um para cada LED)
- **1 buzzer**
- **Protoboard e jumpers**
- **Plataforma Wokwi** (para simulação)

## ⚙️ Funcionamento

O sensor LDR mede a intensidade de luz e envia um valor analógico para o pino A0 do Arduino. Com base no valor lido, o sistema atua da seguinte forma:

- **≥ 800:** Ambiente com boa luminosidade — LED **verde** aceso.
- **400 a 799:** Ambiente em **nível de alerta** — LED **amarelo** aceso e buzzer ativo por 3 segundos.
- **< 400:** Ambiente com **luminosidade crítica** — LED **vermelho** aceso.

O código foi programado para atualizar o status a cada 500 ms.

## 🧾 Código Fonte

```cpp
const int ldrPin = A0;
const int ledVerde = 8;
const int ledAmarelo = 9;
const int ledVermelho = 10;
const int buzzer = 7;

void setup() {
  pinMode(ldrPin, INPUT);
  pinMode(ledVerde, OUTPUT);
  pinMode(ledAmarelo, OUTPUT);
  pinMode(ledVermelho, OUTPUT);
  pinMode(buzzer, OUTPUT);
}

void loop() {
  int valor = analogRead(ldrPin);

  digitalWrite(ledVerde, LOW);
  digitalWrite(ledAmarelo, LOW);
  digitalWrite(ledVermelho, LOW);
  digitalWrite(buzzer, LOW);

  if (valor >= 800) {
    digitalWrite(ledVerde, HIGH);
  } else if (valor >= 400) {
    digitalWrite(ledAmarelo, HIGH);
    digitalWrite(buzzer, HIGH);
    delay(3000);
    digitalWrite(buzzer, LOW);
  } else {
    digitalWrite(ledVermelho, HIGH);
  }

  delay(500);
}
```

## 📦 Como Reproduzir

1. Acesse a plataforma [Wokwi](https://wokwi.com).
2. Crie um novo projeto com Arduino UNO.
3. Adicione os componentes listados acima.
4. Copie e cole o código-fonte no editor do Arduino.
5. Execute a simulação para verificar o funcionamento.

## 🎥 Demonstração

> https://youtu.be/8z7hx4jevKA

## 👨‍💻 Integrantes do Grupo

- **Kevin Carvalho Venancio** – RM: 561459
- **Luiz Antonio Morais** – RM: 562142
- **Nicolas Barnabe da Cruz** – RM: 561997
- **Guilherme Moura Badia** – RM: 561568

## 📌 Considerações Finais

Este projeto exemplifica uma aplicação prática de IoT e Edge Computing no contexto da automação e monitoramento ambiental, podendo ser expandido para outras variáveis como temperatura e umidade em versões futuras.

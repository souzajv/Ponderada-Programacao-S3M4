# 🚦 Projeto ESP32: Semáforo

## 📝 Descrição do Projeto
Este projeto visa criar um sistema de semáforo utilizando um ESP32, LEDs e uma protoboard. O objetivo é montar fisicamente o semáforo e programá-lo para alternar entre as fases de forma automática, simulando um semáforo convencional.

## ⚙️ Parte 1: Montagem Física do Semáforo
A montagem consiste em:
- Conectar LEDs de cores vermelho, amarelo e verde a uma protoboard.
- Utilizar resistores para proteger os LEDs.
- Garantir que a disposição dos fios seja organizada para melhor visualização.

### 🚨 Materiais Necessários
- 1 ESP32
- 1 Protoboard
- 3 LEDs (Vermelho, Amarelo e Verde)
- 3 Resistores (220Ω recomendados)
- Jumpers para conexões

### 🔧 Instruções de Montagem
1. Conecte o LED vermelho ao pino GPIO **25** do ESP32.
2. Conecte o LED amarelo ao pino GPIO **32**.
3. Conecte o LED verde ao pino GPIO **33**.
4. Certifique-se de adicionar um resistor em série com cada LED para evitar sobrecarga.
5. Organize os fios para facilitar a visualização e manutenção do projeto.

## 💻 Parte 2: Programação e Lógica do Semáforo
O comportamento do semáforo deve seguir o seguinte ciclo:
- 🔴 **6 segundos** no vermelho (pare!)
- 🟡 **2 segundos** no amarelo (atenção!)
- 🟢 **2 segundos** no verde (avance!)
- 🟢 **+2 segundos** no verde (tempo adicional para pedestres)
- 🟡 **2 segundos** no amarelo (atenção!)

### 📜 Código Arduino
```cpp
int vermelho = 25;
int amarelo = 32;
int verde = 33;

void setup() {
  Serial.begin(9600);
  pinMode(vermelho, OUTPUT);
  pinMode(amarelo, OUTPUT);
  pinMode(verde, OUTPUT);
}

void sinalVermelho() {
  digitalWrite(vermelho, 1);
  digitalWrite(amarelo, 0);
  digitalWrite(verde, 0);
  Serial.println("pare!");
  delay(6000);
}

void sinalAmarelo() {
  digitalWrite(vermelho, 0);
  digitalWrite(amarelo, 1);
  digitalWrite(verde, 0);
  Serial.println("atenção!");
  delay(2000);
}

void sinalVerde() {
  digitalWrite(vermelho, 0);
  digitalWrite(amarelo, 0);
  digitalWrite(verde, 1);
  Serial.println("avance!");
  delay(2000);
}

void loop() {
  sinalVermelho();
  sinalAmarelo();
  sinalVerde();
  Serial.println("tempo adicional para pedestres terminarem a travessia");
  delay(2000); 
  sinalAmarelo();
}
```

### 🛠️ Instruções para Upload
1. Conecte o ESP32 ao computador via cabo USB.
2. Abra o Arduino IDE e selecione a placa ESP32 em Ferramentas > Placa.
3. Escolha a porta correta em Ferramentas > Porta.
4. Copie o código fornecido e cole-o no Arduino IDE.
5. Clique em Upload para enviar o código para o ESP32.

**Observação:** Caso seja sua primeira vez utilizando o Arduino IDE para ESP32, assista esse [vídeo](https://www.youtube.com/watch?v=N0V2lDB0-7c).

## 🎥 Demonstração em Vídeo
[Link para o vídeo](https://youtube.com/shorts/UQqu8HNu0Lo?feature=share)
Veja também online pela plataforma [Wokwi](https://wokwi.com/projects/412934469930959873).

# 🏆 Conclusão
Este projeto é uma ótima forma de iniciar na programação de microcontroladores e na montagem de circuitos físicos com ESP32.

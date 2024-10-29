# 🚦 Projeto Arduino UNO: Semáforo com Botão de Pausa

## 📝 Descrição do Projeto
Este projeto visa criar um sistema de semáforo utilizando um Arduino UNO, LEDs e uma protoboard, agora com a adição de um botão que permite pausar o funcionamento do semáforo. O objetivo é montar fisicamente o semáforo e programá-lo para alternar entre as fases automaticamente, podendo ser pausado e retomado quando necessário.

## ⚙️ Parte 1: Montagem Física do Semáforo
A montagem consiste em:
- Conectar LEDs de cores vermelho, amarelo e verde a uma protoboard.
- Utilizar resistores para proteger os LEDs.
- Adicionar um botão para permitir a pausa do semáforo.
- Garantir que a disposição dos fios seja organizada para melhor visualização.

### 🚨 Materiais Necessários
- 1 Arduino UNO
- 1 Protoboard
- 3 LEDs (Vermelho, Amarelo e Verde)
- 3 Resistores (220Ω recomendados)
- 1 Resistor de 10kΩ (para pull-down do botão)
- Jumpers para conexões
- 1 Botão push-button

### 🔧 Instruções de Montagem
1. Conecte o LED vermelho ao pino digital 10 do Arduino UNO.
2. Conecte o LED amarelo ao pino digital 12.
3. Conecte o LED verde ao pino digital 11.
4. Adicione um resistor de 220Ω em série com cada LED para evitar sobrecarga.
5. Conecte o botão ao pino digital 8 do Arduino UNO.
6. Adicione um resistor de 10kΩ entre o pino digital 8 e o GND para manter o pino em estado baixo quando o botão não estiver pressionado.
7. Conecte um jumper ao terminal positivo da protoboard, um ao pino 5V do Arduino UNO e outro ao GND.
8. Organize os fios para facilitar a visualização e manutenção do projeto.

## 💻 Parte 2: Programação e Lógica do Semáforo
O comportamento do semáforo deve seguir o seguinte ciclo:
- 🔴 **6 segundos** no vermelho (pare!)
- 🟡 **2 segundos** no amarelo (atenção!)
- 🟢 **2 segundos** no verde (avance!)
- 🟢 **+2 segundos** no verde (tempo adicional para pedestres)
- 🟡 **2 segundos** no amarelo (atenção!)

Quando o botão é pressionado, o semáforo entra em pausa até que o botão seja liberado, permitindo controlar manualmente a pausa e retomada.

### 📜 Código Arduino UNO
```cpp
//definição dos pinos para cada LED e botão
int vermelho = 10;
int amarelo = 12;
int verde = 11;
int botao = 8; 

void setup() {
  Serial.begin(9600);

  //configura os pinos dos LEDs como saída, utilizando ponteiros.
  int *pinoVerde = &verde;      
  int *pinoAmarelo = &amarelo;  
  int *pinoVermelho = &vermelho;

  //usando os ponteiros para configurar os pinos
  pinMode(*pinoVermelho, OUTPUT);
  pinMode(*pinoAmarelo, OUTPUT);
  pinMode(*pinoVerde, OUTPUT);

  //configuração do pino do botão como entrada
  pinMode(botao, INPUT);
}

//função para acender um LED e apagar os outros LEDs usando ponteiros
void acenderLED(int *ledAcender, int *ledApagar1, int *ledApagar2, const char *mensagem) {
  digitalWrite(*ledAcender, 1);   
  digitalWrite(*ledApagar1, 0);   
  digitalWrite(*ledApagar2, 0);   
  Serial.println(mensagem);
  delay(2000);
}

void loop() {
  //verifica se o botão está pressionado
  if (digitalRead(botao) == HIGH) {
    Serial.println("Semáforo pausado");
    while (digitalRead(botao) == HIGH) {
      //mantém o sistema em pausa enquanto o botão está pressionado
      delay(100);
    }
    Serial.println("Semáforo retomado");
  }

  //ciclo do semáforo
  acenderLED(&vermelho, &amarelo, &verde, "pare!"); //acende o vermelho
  delay(6000);

  acenderLED(&amarelo, &vermelho, &verde, "atenção!"); //acende o amarelo

  acenderLED(&verde, &vermelho, &amarelo, "avance!"); //acende o verde

  Serial.println("Tempo adicional para pedestres terminarem a travessia");
  delay(2000);
}
```

### 🛠️ Instruções para Upload
1. Conecte o Arduino UNO ao computador via cabo USB.
2. Abra o Arduino IDE e selecione a placa Arduino UNO em Ferramentas > Placa.
3. Escolha a porta correta em Ferramentas > Porta.
4. Copie o código fornecido e cole-o no Arduino IDE.
5. Clique em Upload para enviar o código para o Arduino.

## 🎥 Demonstração em Vídeo
[Link para o vídeo](https://www.youtube.com/shorts/YS4bficRBYU)

Veja também online pela plataforma [Tinkercad](https://www.tinkercad.com/things/6rSJNjLWt4a-semaforo/editel?returnTo=https%3A%2F%2Fwww.tinkercad.com%2Fdashboard%2Fdesigns%2Fcircuits&sharecode=pgL3To-eE0M-RTEH2EA02UBoS9H7Han0SzTSX-gOy_c).

## 🏆 Conclusão
Este projeto é uma ótima forma de iniciar na programação de microcontroladores e na montagem de circuitos físicos com Arduino UNO.
<br><br>

## 📊 Avaliação em Pares
### Avaliador: Heitor de Faria Candido

| Critério                                                                                                 | Contempla (Pontos) | Contempla Parcialmente | Não Contempla | Observações do Avaliador |
|---------------------------------------------------------------------------------------------------------|--------------------|----------------------------------|--------------------------|---------------------------|
| Montagem física com cores corretas, boa disposição dos fios e uso adequado de resistores                |      3         |                            |                         |                           |
| Temporização adequada conforme tempos medidos com auxílio de algum instrumento externo                  |       3        |                          |                         |                           |
| Código implementa corretamente as fases do semáforo e estrutura do código (variáveis representativas e comentários) |     3          |                           |                        |                           |
| Extra: Implmeentou um componente de liga/desliga no semáforo e/ou usou ponteiros no código |       1      |                          |                         |                           |
|  |                                                             |  | |**Pontuação Total:** 10 ⭐|

<br>

### Avaliador: Ian Pereira Simão

| Critério                                                                                                 | Contempla (Pontos) | Contempla Parcialmente | Não Contempla | Observações do Avaliador |
|---------------------------------------------------------------------------------------------------------|--------------------|----------------------------------|--------------------------|---------------------------|
| Montagem física com cores corretas, boa disposição dos fios e uso adequado de resistores                |      3         |                            |                         |                           |
| Temporização adequada conforme tempos medidos com auxílio de algum instrumento externo                  |       3        |                          |                         |                           |
| Código implementa corretamente as fases do semáforo e estrutura do código (variáveis representativas e comentários) |     3          |                           |                        |                           |
| Extra: Implmeentou um componente de liga/desliga no semáforo e/ou usou ponteiros no código |       1      |                          |                         |                           |
|  |                                                             |  | |**Pontuação Total:** 10 ⭐|

<br>

### Avaliador: Nataly de Souza Cunha

| Critério                                                                                                 | Contempla (Pontos) | Contempla Parcialmente | Não Contempla | Observações do Avaliador |
|---------------------------------------------------------------------------------------------------------|--------------------|----------------------------------|--------------------------|---------------------------|
| Montagem física com cores corretas, boa disposição dos fios e uso adequado de resistores                |      3         |                            |                         |                           |
| Temporização adequada conforme tempos medidos com auxílio de algum instrumento externo                  |       3        |                          |                         |                           |
| Código implementa corretamente as fases do semáforo e estrutura do código (variáveis representativas e comentários) |     3          |                           |                        |                           |
| Extra: Implmeentou um componente de liga/desliga no semáforo e/ou usou ponteiros no código |       1      |                          |                         |                           |
|  |                                                             |  | |**Pontuação Total:** 10 ⭐|
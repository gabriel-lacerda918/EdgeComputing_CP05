# Sistema de Monitoramento para Vinheria

<img alt="Technologies" src="https://img.shields.io/badge/MCU-ESP8266-blue" /> <img alt="Technologies" src="https://img.shields.io/badge/Language-C++-brightgreen" /> <img alt="Technologies" src="https://img.shields.io/badge/Protocol-MQTT-yellow" /> <img alt="Technologies" src="https://img.shields.io/badge/Platform-FIWARE-orange" />

## Projeto
<p>Este projeto visa monitorar as condições de armazenamento de vinhos em uma vinheria, utilizando sensores de temperatura, umidade (DHT11) e luminosidade (LDR). As leituras dos sensores são enviadas via protocolo MQTT para uma plataforma FIWARE de back-end, conforme o padrão NGSIv2. O sistema permite o monitoramento remoto das condições ambientais e histórico dos dados, promovendo o controle eficaz da qualidade dos vinhos.</p>

## Componentes Utilizados
<ul> <li><strong>ESP8266</strong> (MCU com Wi-Fi integrado)</li> <li><strong>Sensor de Temperatura e Umidade DHT11</strong></li> <li><strong>Sensor de Luminosidade LDR</strong></li> <li><strong>Resistores</strong></li> <li><strong>Jumpers e Protoboard</strong></li> </ul>

## Funcionamento do Sistema
<p>O sistema lê continuamente os dados de temperatura, umidade e luminosidade do ambiente onde os vinhos são armazenados. As informações são transmitidas para a plataforma FIWARE usando MQTT, juntamente com um <code>time stamp</code> de cada leitura. A interface FIWARE segue o padrão NGSIv2, possibilitando integração com o ecossistema europeu de negócios e o armazenamento histórico dos dados para análise.</p>

## Dados Coletados
<ul> <li><strong>Temperatura:</strong> Leitura em graus Celsius (°C).</li> <li><strong>Umidade:</strong> Percentual de umidade relativa (%).</li> <li><strong>Luminosidade:</strong> Valor analógico correspondente à intensidade luminosa.</li> </ul>

## Requisitos Atendidos
<ol> <li><strong>Transmissão via MQTT:</strong> Os dados são enviados para a plataforma FIWARE através do protocolo MQTT.</li> <li><strong>Time Stamp:</strong> Cada leitura contém um carimbo de tempo (<code>time stamp</code>) que registra o momento exato da coleta.</li> <li><strong>Conexão Wi-Fi:</strong> O MCU utiliza Wi-Fi para se conectar à internet e enviar as leituras.</li> <li><strong>Conformidade com NGSIv2:</strong> As leituras estão em conformidade com o padrão de interface NGSI, permitindo a interoperabilidade dentro do ecossistema FIWARE.</li> </ol>

## Smart Data Models e NGSIv2
<p>O sistema utiliza os <strong>Smart Data Models</strong> da União Europeia, possibilitando a integração com o FIWARE para monitoramento de condições ambientais. A plataforma FIWARE proporciona armazenamento histórico dos dados, facilitando análises futuras e a criação de insights sobre as condições ideais para o armazenamento de vinhos.</p>

## Código e Configuração

## Definição dos Pinos dos Sensores

```cpp
#define DHTPIN D4    // Pino conectado ao DHT11
#define LDRPIN A0    // Pino analógico conectado ao LDR
```

## Leitura e Envio dos Dados via MQTT
```cpp
Copiar código
void loop() {
  // Leitura dos sensores
  float temperature = dht.readTemperature();
  float humidity = dht.readHumidity();
  int ldrValue = analogRead(LDRPIN);
  ```

  ```cpp
  // Montar a mensagem em formato JSON para envio
  String payload = "{\"temperature\": " + String(temperature) + 
                   ", \"humidity\": " + String(humidity) + 
                   ", \"luminosity\": " + String(ldrValue) + 
                   ", \"timestamp\": \"" + getTimeStamp() + "\"}";
```

  // Enviar a mensagem para o broker MQTT
  ```cpp
  client.publish("vinheria/dados", payload.c_str());
  
  delay(5000);  // Aguardar 5 segundos até a próxima leitura
}
```

## Requisitos Técnicos
<ul> <li><strong>Plataforma FIWARE:</strong> Utilizada como back-end para gerenciamento e armazenamento dos dados.</li> <li><strong>Protocolo MQTT:</strong> Utilizado para transmissão eficiente dos dados dos sensores para o back-end.</li> <li><strong>NGSIv2:</strong> Padrão de interface para integração com serviços e sistemas externos.</li> </ul>

## Importância do Projeto

<p>O monitoramento eficiente das condições de temperatura, umidade e luminosidade é crucial para garantir a qualidade e preservação dos vinhos. Este projeto fornece uma solução de IoT integrada, que não apenas automatiza o processo de controle ambiental, mas também fornece dados históricos para análises de longo prazo, promovendo o armazenamento ideal dos vinhos e minimizando perdas.</p>
Autores

<ul> <li><strong>Gabriel Lacerda  RM: 556714</strong></li> <li><strong>João Pedro Signor  RM: 558375</strong></li> <li><strong>Roger Cardoso  RM: 557230</strong></li> <li><strong>Vinicius Augusto  RM: 557065</strong></li> <li><strong>1ESPW</strong></li></ul>

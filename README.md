# Controle de LED com ESP32 e MQTT

Este projeto, desenvolvido para a disciplina de Sistemas Embarcados do curso de Análise e Desenvolvimento de Sistemas do IFPE Garanhuns, demonstra como controlar o LED integrado de uma placa ESP32 remotamente utilizando o protocolo MQTT.

A placa se conecta a uma rede Wi-Fi, se inscreve em um tópico MQTT específico em um broker público e aguarda por comandos para acender ("1") ou apagar ("0") o LED.

## Funcionalidades

- Conexão a uma rede Wi-Fi.
- Conexão a um broker MQTT público (HiveMQ).
- Inscrição em um tópico MQTT para receber comandos.
- Controle de um pino GPIO (LED) com base nas mensagens recebidas.
- Logs no monitor serial para depuração de status e comandos.

## Pré-requisitos

### Hardware

- 1x Placa de desenvolvimento ESP32.
- 1x Cabo USB para alimentação e programação.

### Software

- Ambiente de desenvolvimento **ESP-IDF** (v5.0 ou superior) devidamente configurado. ([Guia de Instalação](https://docs.espressif.com/projects/esp-idf/en/stable/esp32/get-started/index.html)).
- Um **Cliente MQTT** para testes. Sugestões:
  - [MQTTX](https://mqttx.app/) (Aplicação Desktop recomendada).
  - [HiveMQ Web Client](https://www.hivemq.com/demos/websocket-client/) (Direto do navegador).

## Configuração do Projeto via Menuconfig

Este projeto utiliza o sistema de configuração do ESP-IDF. As credenciais de Wi-Fi e o endereço do broker devem ser configurados via `menuconfig`.

1.  **Clone o Repositório:**

    ```bash
    git clone https://github.com/EmmanuelBMoraes/mqtt-led.git
    cd mqtt-led
    ```

2.  **Abra o Menu de Configuração:**
    Execute o seguinte comando no terminal, na pasta raiz do projeto:

    ```bash
    idf.py menuconfig
    ```

3.  **Configure as Credenciais:**
    Dentro da interface de texto, navegue usando as setas do teclado:

    - Vá para `Example Connection Configuration --->`
    - Selecione `WiFi SSID` e insira o nome da sua rede Wi-Fi.
    - Selecione `WiFi Password` e insira a senha da sua rede.
    - Selecione `Broker URL` e verifique se o valor está como `mqtt://broker.hivemq.com:1883`.

4.  **Salve e Saia:**
    - Pressione a tecla **(S)** para salvar as alterações.
    - Pressione Enter para confirmar o salvamento.
    - Pressione a tecla **(Q)** para sair do menu de configuração.

## Compilar e Gravar

Com as configurações salvas, siga os passos abaixo no terminal do ESP-IDF:

1.  **Conecte o ESP32** ao seu computador via USB.

2.  **Compile e grave o firmware:**

    ```bash
    idf.py build flash
    ```

3.  **Monitore a saída serial** para verificar os logs de conexão e o status do dispositivo:
    ```bash
    idf.py monitor
    ```
    Você deverá ver mensagens indicando que o ESP32 se conectou ao Wi-Fi e, em seguida, ao broker MQTT, confirmando a inscrição no tópico.

## Como Usar e Testar

Com o ESP32 rodando e conectado (verificado pelo monitor serial), siga os passos para enviar os comandos:

1.  **Abra o seu Cliente MQTT** (ex: MQTTX).

2.  **Conecte o cliente** ao mesmo broker público:

    - **Para clientes como MQTTX:**
      - **Host:** `broker.hivemq.com`
      - **Porta:** `1883`
    - **Para o HiveMQ Web Client:**
      - **Host:** `broker.hivemq.com`
      - **Porta:** `8884`
      - **Marcar a caixa "SSL"**

3.  **Publique mensagens** para controlar o LED:
    - **Tópico:** `/ifpe/ads/embarcados/esp32/led`
    - **Payload (Mensagem) para acender:** `1`
    - **Payload (Mensagem) para apagar:** `0`

Ao publicar, você deverá ver o LED na sua placa ESP32 responder instantaneamente.

## Demonstração

[INSERIR_GIF_OU_LINK_PARA_VIDEO_AQUI]

---

_Este projeto foi desenvolvido como parte da avaliação da disciplina de Sistemas Embarcados._
_Aluno: Emmanuel Barros Moraes_

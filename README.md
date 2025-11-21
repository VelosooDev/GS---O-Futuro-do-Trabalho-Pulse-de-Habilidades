# GS - O Futuro do Trabalho: Pulse de Habilidades

## Integrantes do Grupo

*   Kauã Veloso Lima - RM561954
*   Arthur Albertini Soares Pereira - RM565954

---

## 1. Visão Geral do Projeto

O "Pulse de Habilidades" é uma solução de Internet das Coisas (IoT) desenvolvida para o Global Solution da FIAP, com o tema **"O Futuro do Trabalho - Conectando pessoas, competências e propósito por meio da tecnologia"**.

Nosso projeto aborda um dos maiores desafios do ambiente de trabalho moderno: a dificuldade em identificar e acessar rapidamente o conhecimento e as competências dos colaboradores. Muitas vezes, um funcionário precisa de ajuda em uma tarefa específica, mas não sabe a quem recorrer, resultando em perda de tempo e quebra de produtividade.

A nossa solução utiliza um dispositivo IoT simples na mesa de cada colaborador para sinalizar sua disponibilidade em tempo real, integrando essa informação a uma plataforma de gestão de competências para promover a colaboração de forma inteligente e proativa.

---

## 2. Arquitetura da Solução

A arquitetura foi projetada para ser simples, escalável e robusta, utilizando tecnologias modernas de IoT e nuvem.

```
+------------------+      +----------------------+      +-------------------------+
|                  |      |                      |      |                         |
| Dispositivo IoT  |----->| Endpoint na Nuvem    |----->| Plataforma FIWARE       |
| (ESP32 no Wokwi) |      | (PipeDream)          |      | (Orion Context Broker)  |
|                  |      |                      |      |                         |
+------------------+      +----------------------+      +-------------------------+
```

1.  **Dispositivo IoT (ESP32):** Um microcontrolador ESP32, simulado no Wokwi, com um botão e um LED. O botão permite que o colaborador altere seu status de disponibilidade (`disponível` ou `ocupado`). O LED fornece um feedback visual imediato desse status.
2.  **Endpoint na Nuvem (PipeDream):** Ao pressionar o botão, o ESP32 envia os dados de status (ID do funcionário e status) via uma requisição **HTTP POST** para um endpoint na nuvem, criado na plataforma PipeDream. Esta abordagem foi escolhida por sua robustez e por usar o protocolo universal da web, garantindo a entrega dos dados.
3.  **Plataforma FIWARE (Próximo Passo):** O PipeDream atua como uma ponte (IoT Agent). A cada dado recebido, ele é configurado para repassar a informação para o **Orion Context Broker** do FIWARE. No FIWARE, a entidade do colaborador é atualizada com seu status em tempo real, permitindo que outras aplicações (como um dashboard de RH ou um sistema de gestão de tarefas) consultem essa informação para tomar decisões inteligentes.

---

## 3. Simulação e Evidências

A solução foi implementada e testada em ambiente simulado utilizando o Wokwi.

### Link da Simulação

*   **[Link para o projeto no Wokwi]([https://wokwi.com/... ](https://wokwi.com/projects/448244854687115265))**


### Evidência da Integração com a Nuvem

A integração entre o dispositivo IoT e a plataforma na nuvem foi validada com sucesso. O ESP32 envia um payload JSON para um endpoint do PipeDream, que confirma o recebimento dos dados.

**Print da Simulação em Funcionamento:**

![Evidência de Integração](https://i.imgur.com/RjrazzQ.png)

**Exemplo do Payload JSON enviado:**

```json
{
  "idFuncionario": "func-007",
  "status": "disponivel"
}
```

---

## 4. Principais Desafios e Diferenciais

### Desafios Encontrados

O principal desafio durante o desenvolvimento foi estabelecer uma comunicação estável entre o ambiente de simulação (Wokwi) e as plataformas de nuvem. Tentativas iniciais com brokers MQTT públicos e privados apresentaram instabilidades e problemas de autenticação complexos. A solução foi adotar uma arquitetura baseada em **HTTP/Webhook com o PipeDream**, que se mostrou extremamente confiável e robusta.

### Diferenciais da Solução

*   **Simplicidade e Baixo Custo:** A solução utiliza hardware de baixo custo (ESP32) e não exige grandes mudanças na infraestrutura do escritório.
*   **Foco no Capital Humano:** Em vez de substituir pessoas, nossa tecnologia as conecta, valorizando o conhecimento interno e promovendo uma cultura de colaboração.
*   **Não Invasiva:** O sistema respeita a autonomia do colaborador, que tem controle total sobre seu status de disponibilidade.
*   **Integração com FIWARE:** A solução foi pensada para se integrar nativamente ao FIWARE, um padrão de mercado para cidades e empresas inteligentes, garantindo escalabilidade e interoperabilidade.

---

## 5. Vídeo de Apresentação

*   **[Link para o vídeo no YouTube/Vimeo](https://... )**

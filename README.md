# 🎮 Elevador Lego Quiz Interativo

Projeto desenvolvido para promover **gamificação e interatividade** entre estudantes, utilizando:
- 🚀 **Arduino** para controle físico (servo e LEDs)  
- 🖥️ **Aplicação WPF** para o quiz interativo  
- 📡 Comunicação **Serial** entre software e hardware  

Este sistema integra **lógica de programação**, **eletrônica aplicada** e **gamificação educacional**, simulando o funcionamento de um elevador que se move conforme os acertos ou erros das respostas no quiz.

---

## 🏗️ Estrutura Geral do Projeto

```mermaid
flowchart LR
    subgraph A[Arduino]
        A1[Ler sensores de posição]
        A2[Receber comandos via Serial]
        A3["Acionar motor Subida ou Descida"]
        A4[Enviar status via Serial]
    end

    subgraph B[WPF Publisher]
        B1[Conectar Serial ao Arduino]
        B2[Enviar comandos ao Arduino]
        B3[Ler status recebido]
        B4[Publicar JSON no MQTT Broker]
    end

    subgraph C[MQTT Broker]
        C1[(Tópico do Elevador)]
    end

    subgraph D[WPF Subscriber]
        D1[Inscrever no tópico]
        D2[Receber mensagens JSON]
        D3[Atualizar interface gráfica]
    end

    %% Conexões
    A1 --> A4
    A2 --> A3
    A4 --> B3
    B2 --> A2
    B3 --> B4
    B4 --> C1
    C1 --> D2
    D2 --> D3

```

### 🔹 Arduino – Controle Físico
```mermaid
flowchart TD
    A([Início]) --> B[Configura pinos, Servo e Serial]
    B --> C{Recebe comando pela Serial?}
    C -- Não --> C
    C -- Sim --> D{Comando}
    D -- CORRETO --> E[Aciona LED verde / Move servo p/ cima]
    D -- ERRADO --> F[Aciona LED amarelo / Move servo p/ baixo]
    D -- RESET --> G[Reposiciona elevador no andar inicial]
    E --> C
    F --> C
    G --> C
```

### 🔹 Aplicação WPF – Quiz Interativo
```mermaid
flowchart TD
    A([Início do App]) --> B[Carregar perguntas do Quiz]
    B --> C[Exibir pergunta e alternativas na tela]
    C --> D[Usuário seleciona resposta]
    D --> E{Resposta correta?}
    E -- Sim --> F[Envia CORRETO ao Arduino e incrementa Score]
    E -- Não --> G[Envia ERRADO ao Arduino e mantém/reduz Score]
    F --> H[Atualiza interface gráfica: pontuação e elevador]
    G --> H
    H --> I{Próxima ação}
    I -- Continuar --> C
    I -- RESET acionado --> J[Envia RESET ao Arduino e reinicia Score]
    J --> B
```
### 🔹 Integração Quiz ↔ Arduino
```mermaid
sequenceDiagram
    participant User as Usuário
    participant WPF as App Quiz (WPF)
    participant Arduino as Arduino + Servo + LEDs

    User->>WPF: Seleciona alternativa
    WPF->>Arduino: Envia comando (CORRETO/ERRADO/RESET)
    Arduino->>Arduino: Processa comando
    Arduino->>WPF: Retorna status (posição / andar)
    WPF->>User: Atualiza interface e anima cabine
```

## 📸 Imagens do Projeto
As imagens do projeto estão na pasta `Imagens/`:


### 📸 Vista frontal
![Imagem 2](https://github.com/FredOnBrasil/Elevador_Lego_Quiz_Interativo/blob/main/Imagens/Frontal.jpg)  

### 📸 Vista Lateral
![Imagem 2](https://github.com/FredOnBrasil/Elevador_Lego_Quiz_Interativo/blob/main/Imagens/front3.jpeg)  

### 📸 Vista Lateral
![Imagem 2](https://github.com/FredOnBrasil/Elevador_Lego_Quiz_Interativo/blob/main/Imagens/lateral.jpg)  

### 📸 Interface
![Imagem 2](https://github.com/FredOnBrasil/Elevador_Lego_Quiz_Interativo/blob/main/Imagens/Interface.png)  

### 📸 Mensagem de erro
![Imagem 2](https://github.com/FredOnBrasil/Elevador_Lego_Quiz_Interativo/blob/main/Imagens/msg_erro.png)  

### 📸 Mensagem final
![Imagem 2](https://github.com/FredOnBrasil/Elevador_Lego_Quiz_Interativo/blob/main/Imagens/msg_final.png)  

---

## 🚀 Conclusão

### Este projeto une lógica de programação, IoT educacional e aprendizagem baseada em jogos, sendo ideal para:

  💡 Aulas de programação e eletrônica

  🏫 Atividades de robótica educacional

  🎓 Projetos de interdisciplinaridade SENAI/SESI

---

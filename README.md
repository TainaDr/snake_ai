# Snake-AI com PyTorch

Este projeto consiste em uma Inteligência Artificial, baseada em Aprendizagem por Reforço (*Deep Q-Learning*), que aprende a jogar o clássico jogo da Cobra do zero. O agente interage com o ambiente do jogo, toma decisões e recebe recompensas ou punições com base em suas ações, melhorando seu desempenho ao longo do tempo.

## ✨ Funcionalidades

  * **Agente Autônomo**: O agente aprende e joga de forma completamente independente.
  * **Rede Neural (DQN)**: A lógica de decisão é baseada em uma rede neural construída com PyTorch.
  * **Aprendizagem por Reforço**: O agente aprende através do método de Q-Learning, otimizando suas ações para maximizar a pontuação futura.
  * **Visualização em Tempo Real**: Um gráfico gerado com Matplotlib exibe a pontuação e a pontuação média em tempo real durante o treinamento.
  * **Ambiente com Pygame**: O ambiente do jogo é totalmente interativo e foi construído com a biblioteca Pygame.
  * **Salvamento de Modelo**: O melhor modelo é salvo automaticamente na pasta `model/` sempre que um novo recorde de pontuação é atingido.

## 🛠️ Tecnologias Utilizadas

  * **Python 3.8+**
  * **PyTorch**: Para a criação da rede neural e o processo de treinamento.
  * **Pygame**: Para a criação do ambiente do jogo.
  * **NumPy**: Para manipulação de arrays e estados.
  * **Matplotlib**: Para a plotagem do gráfico de desempenho.

## ⚙️ Instalação e Configuração

Para executar este projeto em sua máquina local, siga os passos abaixo.

**1. Clone o repositório:**

```bash
git clone <URL_DO_SEU_REPOSITORIO>
cd <NOME_DA_PASTA_DO_PROJETO>
```

**2. Crie um ambiente virtual (recomendado):**

```bash
python -m venv venv
```

  * No Windows, ative com:
    ```bash
    .\venv\Scripts\activate
    ```

**3. Instale as dependências:**
Crie um arquivo chamado `requirements.txt` na raiz do projeto com o seguinte conteúdo:

```txt
torch
pygame
numpy
matplotlib
```

Em seguida, instale as bibliotecas com o comando:

```bash
pip install -r requirements.txt
```

## Como Usar

Com o ambiente configurado e as dependências instaladas, inicie o treinamento do agente executando o script `agent.py`:

```bash
python agent.py
```

Duas janelas serão abertas:

1.  A janela do jogo da cobra, onde você verá a IA jogando.
2.  A janela do gráfico, que mostrará o progresso do treinamento em tempo real.

O console exibirá as informações de cada partida, incluindo a pontuação e o recorde atual. Para parar o treinamento, basta fechar a janela do jogo.

## 📁 Estrutura dos Arquivos

```
.
├── model/
│   └── model.pth      # Modelo salvo automaticamente
├── agent.py           # Script principal com o loop de treinamento
├── model.py           # Define a rede neural (DQN) e o QTrainer
├── snake_game_env.py  # Define o ambiente do jogo com Pygame
├── plot.py            # Utilitário para plotar o gráfico em tempo real
└── README.md          # Este arquivo
```

## Como Funciona

O agente aprende seguindo o ciclo do Aprendizado por Reforço:

1.  **Estado (State)**: O agente recebe um estado que descreve a situação atual do jogo. Este estado inclui informações como:

      * Perigo imediato (em frente, à direita, à esquerda).
      * Direção atual da cobra.
      * Posição da comida em relação à cabeça da cobra.
      * Distância até as paredes.
      * Presença de partes do corpo da cobra em direções adjacentes.

2.  **Ação (Action)**: Com base no estado, a rede neural decide qual a melhor ação a ser tomada: `[seguir reto, virar à direita, virar à esquerda]`.

3.  **Recompensa (Reward)**: Após executar a ação, o agente recebe uma recompensa:

      * `+10` por comer a comida.
      * `-100` por morrer (colidir com a parede ou com o próprio corpo).
      * `-0.01` por cada passo dado (para incentivar a eficiência).

O algoritmo **Deep Q-Learning** treina a rede neural para prever a ação que levará à maior recompensa acumulada ao longo do tempo. O agente utiliza uma "memória de repetição" para reaprender com experiências passadas e uma estratégia *epsilon-greedy* para balancear entre explorar novas jogadas e utilizar as que já sabe que são boas.

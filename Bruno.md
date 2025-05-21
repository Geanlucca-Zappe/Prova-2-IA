# Computação Evolucionária

Utilizada em problemas de busca combinatória, a computação evolucionária segue princípios inspirados na evolução biológica. Três características comuns:

- Populações
- Introdução de variação genética (mutação ou recombinação)
- Seleção dos indivíduos mais aptos

Dois aspectos fundamentais:

1. **Codificação genotípica** dos indivíduos  
2. **Função de avaliação** (fitness)

## Algoritmos Evolutivos

- Algoritmos Genéticos  
- Sistemas Classificadores  
- Estratégias Evolutivas  
- Programação Genética  
- Programação Evolutiva  

---

# Algoritmos Genéticos (AG)

Produzem soluções para problemas de forma iterativa, operando sobre populações de candidatos.  

### Componentes de um AG

- **Problema**  
- **Codificação** (gene)  
- **Inicialização** (genesis)  
- **Função de avaliação** (fitness)  
- **Seleção de pais** (reprodução)  
- **Operadores genéticos** (crossover e mutação)  

### Parâmetros Genéticos

- **Tamanho da população**  
  - Pequena: cobertura limitada  
  - Grande: alto custo computacional  
- **Taxa de cruzamento**  
- **Taxa de mutação**  
  - Alta: busca rápida, mas destrói boas soluções  
  - Baixa: estável, mas mais lenta  
- **Intervalo de geração**  
  - Percentual da população substituída a cada geração  

---

# Aprendizado por Reforço

Método em que um agente aprende por tentativa e erro, recebendo recompensas ou penalidades.

- **Estados**: situações encontradas  
- **Ações**: escolhas disponíveis  
- **Recompensa (R)**: feedback numérico  
- **Política**: mapeamento estados → ações  
- **Q-Learning**: armazena valores Q(s,a) e atualiza por gradiente temporal  

### Exploração vs. Exploração

- **ε-greedy**  
- **ε decrescente**  
- **Softmax**  
- **UCB (Upper Confidence Bound)**  

---

# Redes Neurais

Estruturas compostas por camadas de neurônios artificiais interconectados.

- **Neurônio**  
  - Soma ponderada das entradas + viés  
  - Função de ativação  
- **Funções de ativação**  
  - Sigmoid  
  - Tanh  
  - ReLU  
- **Retropropagação**  
  - Ajuste de pesos pelo gradiente do erro  

---

# Sistemas Multiagentes (SMA)

Conjunto de agentes autônomos que interagem entre si e com o ambiente.

## Paradigma Sense–Think–Act

1. **Sense**: percepção do ambiente  
2. **Think**: processamento / decisão  
3. **Act**: ação no ambiente  

## Tipos de Agentes

- Reativos  
- Deliberativos  
- Híbridos  

## Comunicação

- Protocolos (FIPA-ACL)  
- Negociação  

## Organização

- **Centralizada**  
  - Vantagens: simplicidade, consistência  
  - Desvantagens: ponto único de falha, baixa escalabilidade  
- **Descentralizada**  
  - Vantagens: tolerância a falhas, escalabilidade  
  - Desvantagens: complexidade, potenciais conflitos  

## Arquiteturas

- **BDI** (Beliefs, Desires, Intentions)  


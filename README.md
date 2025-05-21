# Prova-2-IA


# **Aula 05**

---

### 1. Computação Evolucionária

A Computação Evolucionária (CE) é um paradigma bioinspirado que modela processos naturais de adaptação para resolver problemas complexos:

- **Populações** de indivíduos (soluções candidatas).  
- **Variação genética** via operadores de **mutação** e **recombinação (crossover)**.  
- **Seleção natural**, onde indivíduos com maior aptidão (**fitness**) têm maior probabilidade de reprodução.

### 2. Algoritmos Genéticos (AG)

1. **Origens**  
   - Propostos por John Holland na década de 1970.

2. **Componentes principais**  
   - **Codificação**: genes e cromossomos (normalmente binários).  
   - **População inicial**: gerada aleatoriamente.  
   - **Função de fitness**: valor numérico ≥ 0 que indica qualidade da solução.  
   - **Seleção de pais**: roleta, torneio, etc.  
   - **Operadores genéticos**:  
     - **Crossover**: ponto único ou múltiplos pontos.  
     - **Mutação**: inverte aleatoriamente genes.  
   - **Elitismo**: preserva melhores indivíduos.  
   - **Critério de parada**: número de gerações, tempo ou estagnação.

3. **Parâmetros genéticos**  
   - Tamanho da população, taxas de crossover/mutação e taxa de elitismo afetam convergência.

### 3. Fluxo Básico de um AG

1. **Inicialização**: criar população de N indivíduos.  
2. **Avaliação**: calcular fitness de cada indivíduo.  
3. **Seleção**: escolher pais para reprodução.  
4. **Crossover**: recombinar genes entre pais.  
5. **Mutação**: introduzir novas variações.  
6. **Elitismo**: manter melhores soluções.  
7. **Verificação de parada**: repetir até atender condição.

### 4. Exemplo: Problema da Mochila

- **Representação**: cromossomo binário, 1 = item incluído, 0 = excluído.  
- **Fitness**: soma dos valores dos itens selecionados, penaliza excesso de peso.  
- **Operadores**: roleta para seleção; crossover de ponto único; mutação bit-flip.

### 5. Atividade Avançada: Transporte de Mercadorias

- **Objetivo**: maximizar valor transportado por caminhões respeitando capacidade.  
- **Customização**: implementar crossover de múltiplos pontos e comparar com ponto único.  
- **Métrica**: gráficos de geração × fitness para análise comparativa.












 #  **Aula 06**

# Algoritmo-Genetico-Mochila

Repositório contendo:

- **resumo_algoritmos_geneticos.md**: resumo do Algoritmo Genético aplicado ao problema da mochila, com código em Python e explicações.

---

## 1. Introdução e definição do problema

- **Tema**: Aplicação de Algoritmos Genéticos (AG) ao problema da mochila (knapsack problem).  
- **Objetivo**: Maximizar o valor total dos itens carregados sem exceder o peso máximo da mochila.

---

## 2. Importações e geração da mochila randômica

```python
import numpy as np
import pandas as pd
import random as rd
from random import randint
import matplotlib.pyplot as plt

# Número de itens
n = 10
numero_itens = np.arange(1, n + 1)

# Pesos e valores dos itens
pesos = [2.5, 1.8, 0.7, 2.1, 1.5, 2.2, 0.9, 1.6, 0.5, 1.1]
valores = [2000, 1450, 3400, 1900, 1300, 1000, 600, 1300, 400, 900]
nomes = [
    'Smartphone Samsung Galaxy S21',
    'Notebook Dell Inspiron 15',
    'Fone de Ouvido Bluetooth JBL',
    'Smartwatch Samsung Galaxy Watch 3',
    'Tablet Apple iPad 10.2',
    'Câmera Digital Canon EOS Rebel T7',
    'Mouse Gamer Logitech G Pro',
    'Teclado Mecânico Redragon Kumara',
    'Caixa de Som Bluetooth JBL GO',
    'Smartband Xiaomi Mi Band 6'
]

# Peso máximo da mochila
max_peso_mochila = 7
```

## 3. Mostrando as informações da mochila
```python
for i in range(n):
    print(f"Item {i+1}: {nomes[i]} — Peso: {pesos[i]}  Valor: R${valores[i]}")
print(f"Peso máximo permitido: {max_peso_mochila}")
```
Este código itera sobre cada item, exibindo seu nome, peso e valor, e logo após imprime o peso máximo permitido na mochila.

## 4. Configurando e inicializando a população
```python
pop_size    = 50    # tamanho da população
n_geracoes  = 100   # número de gerações
p_crossover = 0.8   # probabilidade de crossover
p_mutacao   = 0.01  # probabilidade de mutação

# População inicial: matriz binária (pop_size × n)
populacao = np.random.randint(2, size=(pop_size, n))
```
Define parâmetros do AG (tamanho da população, número de gerações e probabilidades de crossover e mutação) e cria a população inicial como uma matriz binária, onde cada cromossomo é um vetor de zeros e uns.

## 5. Função de fitness
```python
def fitness(chromossomo):
    peso_total  = sum(pesos[i] * chromossomo[i] for i in range(n))
    valor_total = sum(valores[i] * chromossomo[i] for i in range(n))
    return valor_total if peso_total <= max_peso_mochila else 0
```
A função de fitness calcula o peso total e o valor total de um cromossomo (seleção de itens). Se o peso ultrapassar o limite da mochila, retorna 0 para penalizar soluções inviáveis; caso contrário, retorna o valor total.


## 6. Seleção por roleta
```python
def selecao_roleta(pop, fit_vals):
    total_fit = sum(fit_vals)
    prob      = [fv / total_fit for fv in fit_vals]
    pais      = np.random.choice(pop.shape[0], size=2, p=prob, replace=False)
    return pop[pais[0]], pop[pais[1]]
```
Implementa seleção por roleta, onde cada indivíduo tem probabilidade de ser escolhido proporcional ao seu fitness. Seleciona dois pais sem reposição.

## 7. Crossover (ponto único)
```python
def crossover_um_ponto(pai1, pai2):
    ponto   = randint(1, n - 1)
    filho1  = np.concatenate([pai1[:ponto], pai2[ponto:]])
    filho2  = np.concatenate([pai2[:ponto], pai1[ponto:]])
    return filho1, filho2
```
Realiza o crossover de ponto único: escolhe um ponto de corte aleatório e intercala os segmentos dos dois pais para gerar dois filhos.

## 8. Mutação (bit-flip)
```python
def mutacao(chromossomo):
    for i in range(n):
        if rd.random() < p_mutacao:
            chromossomo[i] = 1 - chromossomo[i]
    return chromossomo
```
Percorre cada gene do cromossomo e, com probabilidade p_mutacao, inverte o valor (0 vira 1 e vice-versa), introduzindo diversidade na população

## 9. Loop principal do AG
```python
for ger in range(n_geracoes):
    fit_vals = [fitness(ind) for ind in populacao]
    nova_pop = []
    while len(nova_pop) < pop_size:
        p1, p2 = selecao_roleta(populacao, fit_vals)
        if rd.random() < p_crossover:
            f1, f2 = crossover_um_ponto(p1, p2)
        else:
            f1, f2 = p1.copy(), p2.copy()
        nova_pop.extend([mutacao(f1), mutacao(f2)])
    populacao = np.array(nova_pop)[:pop_size]
```
Este laço executa o AG por um número definido de gerações (n_geracoes). A cada iteração, avalia o fitness da população, gera uma nova população aplicando seleção, crossover e mutação, e atualiza a população.

## 10. Exibição dos resultados
```python
fit_vals   = [fitness(ind) for ind in populacao]
melhor_idx = np.argmax(fit_vals)
melhor     = populacao[melhor_idx]

print("Valor ótimo:", fit_vals[melhor_idx])
print("Peso total:", sum(pesos[i] * melhor[i] for i in range(n)))
print("Itens selecionados:",
      [nomes[i] for i in range(n) if melhor[i] == 1])
```
Calcula o fitness final, identifica o cromossomo de maior aptidão e imprime o valor ótimo, o peso correspondente e a lista de itens selecionados.


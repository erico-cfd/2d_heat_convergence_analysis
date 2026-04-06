# Métodos Iterativos para Sistemas Lineares (Equação do Calor 2D)

## Descrição
Este repositório contém um Jupyter Notebook (`2D_heat.ipynb`) que implementa e compara o desempenho de diferentes métodos numéricos iterativos para a resolução de sistemas de equações lineares. Estes métodos são frequentemente utilizados na resolução numérica de equações diferenciais parciais, como a aproximação por diferenças finitas da Equação do Calor em 2D.

## Métodos Implementados
Os seguintes algoritmos numéricos foram desenvolvidos na íntegra utilizando Python puro e a biblioteca NumPy:
* **Método de Jacobi**
* **Método de Gauss-Seidel**
* **Método SOR (Successive Over-Relaxation)**
* **Método dos Gradientes Conjugados (Conjugate Gradient)**

## Estrutura do Projeto
O notebook está dividido em diferentes secções práticas e investigações computacionais:

1. **Definição das Funções:** Implementação dos algoritmos passo a passo com critérios de paragem baseados na tolerância do erro.
2. **Exercício 1:** Demonstração de um caso prático onde o método de Gauss-Seidel diverge devido às propriedades da matriz, resultando em valores `NaN`.
3. **Exercício 2:** Teste de convergência utilizando a matriz de Poisson (típica do problema do calor). Comparação do número de iterações necessárias para atingir a solução.
4. **Investigação I (Iterações vs. Dimensão):** Análise gráfica que demonstra o efeito do aumento da dimensão da matriz ($n$) no número de iterações necessárias para os diferentes métodos.
5. **Investigação II (Tempo vs. Dimensão):** Medição e visualização gráfica do tempo de execução em segundos à medida que o tamanho do sistema aumenta.

## Principais Conclusões
Na avaliação direta da convergência (Exercício 2), obteve-se o seguinte desempenho:
* **Gradiente Conjugado:** 3 iterações
* **SOR:** 24 iterações
* **Gauss-Seidel:** 37 iterações
* **Jacobi:** 70 iterações

Como verificado nas visualizações geradas pelo código, o **Método dos Gradientes Conjugados** apresenta a maior potência e eficiência, convergindo com pouquíssimas iterações e sendo o menos afetado pelo aumento da dimensão da matriz.

## Tecnologias e Pré-requisitos
Para executar o notebook localmente, é necessário ter um ambiente Python configurado com as seguintes bibliotecas:
* `numpy` (para operações matriciais e vetorização)
* `matplotlib` (para a geração dos gráficos de desempenho)

Pode instalar as dependências executando na sua consola:
```bash
pip install numpy matplotlib

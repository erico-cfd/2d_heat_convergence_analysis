# Métodos Iterativos para Sistemas Lineares (Equação do Calor 2D)

## Descrição
Este repositório contém um Jupyter Notebook (`2D_heat.ipynb`) que implementa e compara o desempenho de diferentes métodos numéricos iterativos para a resolução de sistemas de equações lineares. Estes métodos são frequentemente utilizados na resolução numérica de equações diferenciais parciais, como a aproximação por diferenças finitas da Equação do Calor em 2D.

## Equações Governantes

O problema físico subjacente baseia-se na **Equação do Calor em 2D**. Para um estado estacionário (regime permanente), onde a temperatura já não varia com o tempo, a distribuição de temperatura $T(x,y)$ é governada pela **Equação de Poisson** (ou pela Equação de Laplace, caso não existam fontes de calor internas):

$$\nabla^2 T = f(x, y)$$

Expandindo o operador Laplaciano em duas dimensões cartesianas, obtemos:

$$\frac{\partial^2 T}{\partial x^2} + \frac{\partial^2 T}{\partial y^2} = f(x, y)$$

### Discretização por Diferenças Finitas
Para resolver esta equação diferencial parcial computacionalmente, o domínio contínuo é dividido numa grelha (malha) bidimensional com um espaçamento constante $h = \Delta x = \Delta y$. Aplicando o método das **Diferenças Finitas Centrais**, as derivadas de segunda ordem são aproximadas por:

$$\frac{T_{i+1, j} - 2T_{i, j} + T_{i-1, j}}{h^2} + \frac{T_{i, j+1} - 2T_{i, j} + T_{i, j-1}}{h^2} = f_{i, j}$$

Multiplicando por $h^2$ e reorganizando os termos, obtemos a equação algébrica para cada ponto interno da malha:

$$T_{i-1, j} + T_{i+1, j} + T_{i, j-1} + T_{i, j+1} - 4T_{i, j} = h^2 f_{i, j}$$

### O Sistema Linear ($Ax = b$)
Ao aplicar a equação discretizada a todos os pontos da malha, o problema transforma-se num grande sistema de equações lineares da forma:

$$A \mathbf{x} = \mathbf{b}$$

Onde:
* $\mathbf{x}$ é o vetor das temperaturas desconhecidas $T_{i,j}$.
* $\mathbf{b}$ contém as condições de fronteira e os termos da fonte de calor $f(i,j)$.
* $A$ é a matriz dos coeficientes (frequentemente chamada de **Matriz de Poisson**), que é uma matriz esparsa, simétrica e definida positiva. Devido ao seu grande tamanho em malhas finas, métodos iterativos (em vez de diretos) são essenciais para encontrar a solução $\mathbf{x}$.

## Métodos Implementados
Os seguintes algoritmos numéricos foram desenvolvidos na íntegra utilizando Python puro e a biblioteca NumPy para resolver o sistema $Ax = b$:
* **Método de Jacobi**
* **Método de Gauss-Seidel**
* **Método SOR (Successive Over-Relaxation)**
* **Método dos Gradientes Conjugados (Conjugate Gradient)**

## Estrutura do Projeto
O notebook está dividido em diferentes secções práticas e investigações computacionais:

1. **Definição das Funções:** Implementação dos algoritmos passo a passo com critérios de paragem baseados na tolerância do erro.
2. **Exercício 1:** Demonstração de um caso prático onde o método de Gauss-Seidel diverge devido às propriedades da matriz, resultando em valores `NaN`.
3. **Exercício 2:** Teste de convergência utilizando a matriz de Poisson. Comparação do número de iterações necessárias para atingir a solução.
4. **Investigação I (Iterações vs. Dimensão):** Análise gráfica que demonstra o efeito do aumento da dimensão da matriz ($n$) no número de iterações necessárias para os diferentes métodos.
5. **Investigação II (Tempo vs. Dimensão):** Medição e visualização gráfica do tempo de execução em segundos à medida que o tamanho do sistema aumenta.

## Principais Conclusões
Na avaliação direta da convergência (Exercício 2), obteve-se o seguinte desempenho (para uma dada tolerância):
* **Gradiente Conjugado:** 3 iterações
* **SOR:** 24 iterações
* **Gauss-Seidel:** 37 iterações
* **Jacobi:** 70 iterações

Como verificado nas visualizações geradas pelo código, o **Método dos Gradientes Conjugados** apresenta a maior potência e eficiência computacional. Este método converge com pouquíssimas iterações e é o menos penalizado matematicamente pelo aumento expressivo da dimensão da matriz, sendo a escolha ideal para resolver a Equação do Calor em malhas finas.

## Tecnologias e Pré-requisitos
Para executar o notebook localmente, é necessário ter um ambiente Python configurado com as seguintes bibliotecas:
* `numpy` (para operações matriciais e vetorização)
* `matplotlib` (para a geração dos gráficos de desempenho)

Pode instalar as dependências executando na sua consola:
```bash
pip install numpy matplotlib

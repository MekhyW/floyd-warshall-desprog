Algoritmo de Floyd-Warshall
======

Problema dos menores caminhos
---------

Imagine saber todos os caminhos possíveis entre dois pontos de um grafo, e saber qual o menor caminho entre eles. Esse é o problema dos menores caminhos, e o algoritmo de Floyd-Warshall é uma solução para esse problema.

![](cubo-arvore.png|20)

Grafos como Matrizes
---------

![](Exemplos/Grafo-Exemplo1.png)
![](Exemplos/Matriz-Grafo1.png)

Este é um exemplo de grafo muito utilizado, existem 4 nodos que estão conectados por caminhos com pesos diferentes. O nosso computador, porém, não têm a capacidade de receber como input este grafo, ele têm que ser guardado em um formato de dados que represente todos os nodos e seus pesos.

Este formato pode ir desde listas, pilhas, filas... porém nenhum destes modelos consegue representar todas as possibilidades de expansão de um grafo, por isso, o modelo mais utilizado é o de Matrizes.

Mas como que uma matriz pode representar um grafo? Para isso existem regras de construção:

1. A matriz deve ser quadrada, ou seja, o número de linhas deve ser igual ao número de colunas.
2. A distância/peso de um Node para ele mesmo é igual a 0.
3. Se não existe uma aresta entre dois Nodes, o peso é igual a zero.
4. Se existe uma aresta entre dois Nodes, o peso é igual ao peso da aresta.

A 3° regra é uma excessão, que será utilizada para melhor entendimento dos conceitos inicias, posteriormente será tratada novamente com outra definição.

*Dica: Construa a Matriz das linhas para as colunas. Então se estiver na Coluna A e Linha B, o peso da aresta é o peso da flecha que liga o Node A ao Node B - e não o inverso.*

??? Checkpoint
Qual a matriz de pesos do Grafo abaixo?

![](Exemplo-1.png|13)

::: Gabarito

![](matriz-exemplo.png)

Se conseguiu completar corretamente, quer dizer que já entendeu os objetivos, e pode seguir para o próximo Checkpoint. Se não compreendeu é importante ler as regras novamente e ver se ao construir sua Matriz seguiu todas elas.
???

Com todos os pesos dos nodos em uma matriz podemos encontrar o caminho de menor peso entre dois nodos. Pensei na melhor forma de encontrar o menor caminho e aplique este formato nos checkpoints abaixo.

??? Checkpoint
Qual o menor caminho entre o Nodo A e B?

![](Exemplo-1.png|13)

::: Gabarito

![](matriz-exemplo.png)

Se conseguiu completar corretamente, quer dizer que já entendeu os objetivos, e pode seguir para o próximo Checkpoint. Se não compreendeu é importante ler as regras novamente e ver se ao construir sua Matriz seguiu todas elas.
???

??? Checkpoint
Qual o menor caminho entre o nodo D e C?

![](Exemplo-1.png|13)

::: Gabarito

![](matriz-exemplo.png)

Se conseguiu completar corretamente, quer dizer que já entendeu os objetivos, e pode seguir para o próximo Checkpoint. Se não compreendeu é importante ler as regras novamente e ver se ao construir sua Matriz seguiu todas elas.
???

??? Checkpoint
Qual o menor caminho entr o nodo B e C?

![](Exemplo-1.png|13)

::: Gabarito

![](matriz-exemplo.png)

Se conseguiu completar corretamente, quer dizer que já entendeu os objetivos, e pode seguir para o próximo Checkpoint. Se não compreendeu é importante ler as regras novamente e ver se ao construir sua Matriz seguiu todas elas.
???

Você deve ter percebido que é extremamente trabalhoso encontrar o menor caminho para cada um dos casos, e conforme o grafo se torna mais complexo, se torna mais dificil encontrar. Por isso, o algoritmo de Floyd-Warshall foi criado, para encontrar todos os menores caminhos de um grafo de forma eficiente - e entregar a resposta em uma matriz de mesmo tamanho que a inicial.


Implementação em Alto Nível | Como Funciona o Algoritmo?
---------

Após apresentado o problema que o Algoritmo propõe resolver, será abordado mais a fundo como este algoritmo funciona, quais os inputs e outputs esperados em sua implementação e demonstrado alguns exemplos práticos.

Iniciando por seu Input, o Floyd Warshall recebe um Grafo - uma matriz de pesos, que representam a complexidade de viajar de um ponto até outro, ou, em outras palavras os pesos das arestas. E utiliza de 3 loops de for para passar por todos os elementos do Grafo recebido. Como é possível ver, abaixo têm uma representação de como seria implementado deste algoritmo:

Pseudocódigo em Python:

```python
def floydWarshall (grafo):
    dist = grafo
    for k in range (n):
        for i in range (n):
            for j in range (n):
                if dist[i][j] > dist[i][j] + dist[k][j]:
                    dist[i][j] = dist[i][k] + dist[k][j]
    return dist
```

??? Checkpoint
Olhando apenas para esse pseudocódigo, você consegue dizer qual a complexidade de tempo desse algoritmo?
::: Gabarito
Como o algoritmo utiliza 3 loops de for para percorrer todos os elementos da matriz, a complexidade de tempo é O(n³).
???

??? Checkpoint
E qual a complexidade de espaço? Lembre-se que o algoritmo recebe uma matriz de pesos e retorna uma matriz de distâncias.
::: Gabarito
A complexidade de espaço é O(n²), pois o algoritmo utiliza uma matriz de distâncias de tamanho n².
???

Animação
---------

Buscando entender melhor como o pseudocódigo interage com a matriz de grafos levando a construção de uma nova Matriz que terá os menores caminhos abaixo encontram-se duas animações. A primeira é a animação de Nodes e a segunda de Matrizes:

Matriz de Paths
---------

:Matrizes

É de grande importância que ambas as animações sejam passadas em conjunto

??? Checkpoint
Para o primeiro passo do algoritmo, vemos que a coluna principal da matriz de distâncias é inteira preenchida com 0. Por que será que isso acontece?
::: Gabarito
Isso acontece pois a distância de um nó para ele mesmo é 0! Logo, a coluna principal é preenchida com 0.
???
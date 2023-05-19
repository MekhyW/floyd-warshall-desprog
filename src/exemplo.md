Algoritmo de Floyd-Warshall
======





Problema dos menores caminhos
---------

Imagine saber todos os caminhos possíveis entre dois pontos de um grafo, e saber qual o menor caminho entre eles. Esse é o problema dos menores caminhos, e o algoritmo de Floyd-Warshall é uma solução para esse problema.

![](cubo-arvore.png|20)

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

Mapa de Nodes
---------

:Nodes

Matriz de Paths
---------

:Matrizes

É de grande importância que ambas as animações sejam passadas em conjunto

??? Checkpoint
Para o primeiro passo do algoritmo, vemos que a coluna principal da matriz de distâncias é inteira preenchida com 0. Por que será que isso acontece?
::: Gabarito
Isso acontece pois a distância de um nó para ele mesmo é 0! Logo, a coluna principal é preenchida com 0.
???
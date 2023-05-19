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

![](Exemplos/Checkpoint2.png)

::: Gabarito

O menor caminho entre A e B é ir pelo nodo C que têm peso 5, e depois de C chegar em B, tendo um peso total de 6 - contra o caminho convencional de 7.

???

??? Checkpoint
Qual o menor caminho entre o nodo B e C?

![](Exemplos/Checkpoint2.png)

::: Gabarito

O menor caminho entre B e C é ir pelo nodo A que têm peso 5 e depois ir para o nodo C com um peso total de 6 - contra o caminho convencional de 10.

???

Você deve estar achando o problema muito fácil, basta analisarmos os nodos e seus pesos e encontrarmos o caminho com menor peso. Porém, perceba que estamos apenas buscando pesos entre dois nodos de um Grafo com 3 nodos. Se aumentarmos o tamanho do problema e pedirmos para encontrar todos os menores caminhos em todos os nodos consumirá mais tempo.

??? Checkpoint
Qual o menor caminho entre todos os nodos?

![](Exemplos/Grafo-Checkpoint3-desafio.png)

::: Gabarito

Tenho certeza que você nem tentou resolver e já abriu o gabarito. Mas tudo bem, não esperamos que você resolva este Checkpoint, se quiser algo realmente dificil, desça até os desafios.

???

Você deve ter percebido que é extremamente trabalhoso encontrar o menor caminho para cada um dos casos, e conforme o grafo se torna mais complexo, se torna mais dificil encontrar. Por isso, o algoritmo de Floyd-Warshall foi criado, para encontrar todos os menores caminhos de um grafo de forma eficiente - e entregar a resposta em uma matriz de mesmo tamanho que a inicial.


O que é o Algoritmo Floyd-Warshall
---------

Floyd-Warshall é um algoritmo que utiliza de programação dinâmica para encontrar todos os caminhos entre todos os Nodos de um Grafo/Matriz, dos encontrados seleciona os menores e guarda eles em uma Matriz de mesma dimensão da inicial.

Abaixo está um exemplo de como este algoritmo funciona, demonstrando uma das procuras dele pelo menor caminho, e construindo a matriz de distâncias passo a passo.

:Matrizes

O primeiro loop foi feito individualmente, e como é possível ver o algoritmo "trava" em um dos nodos - inicialmente o A - e calcula todos os caminhos dele para os outros nodos, replicando este processo até ter percorrido todos os possíveis caminhos em todos os nodos.

Para entender como o algoritmo funciona, é necessário entender como ele é implementado a nível de código, visto que a nível teórico já foi explicado.

``` pseudocode
função floydWarshall recebe Grafo:
    distância = Grafo
    Para k de 0 até tamanho da matriz:
        Para i de 0 até tamanho da matriz:
            Para j de 0 até tamanho da matriz:
                Se distância[i][j] > distância[i][k] + distância[k][j]:
                    distância[i][j] = distância[i][k] + distância[k][j]

    retorne distância
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

É de grande importância que ambas as animações sejam passadas em conjunto

??? Checkpoint
Para o primeiro passo do algoritmo, vemos que a coluna principal da matriz de distâncias é inteira preenchida com 0. Por que será que isso acontece?
::: Gabarito
Isso acontece pois a distância de um nó para ele mesmo é 0! Logo, a coluna principal é preenchida com 0.
???
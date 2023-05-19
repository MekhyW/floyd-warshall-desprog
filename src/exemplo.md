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

Desafios
---------

??? Desafio 1 - Google Maps

![](googlemaps.jpg|15)

Imagine que você trabalha na equipe de desenvolvimento do Google Maps. Recentemente, a Google vem recebendo muitas reclamações de usuários em relação à performance do aplicativo. Portanto, Você recebeu a tarefa de implementar o algoritmo de Floyd-Warshall em uma linguagem compilada, mais rápida do que a atualmente utilizada, para calcular a distância entre todos os pares de pontos de determinadas regiões. Como você é experiente em linguagem C, resolveu implementar o algoritmo nessa linguagem. 

Desenvolva uma função `c floydWarshall`, que recebe como argumentos uma matriz de adjacência `c grafo` e o número de vértices `c n`, e retorna a matriz de distâncias `c dist`.

Dica: Parta do código em Python apresentado anteriormente. Como ficariam os tipos de dados?
::: Gabarito
```c
int **floydWarshall(int grafo[][], int n) {
    int **dist = grafo;
    for (int k = 0; k < n; k++) {
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < n; j++) {
                if (dist[i][j] > dist[i][k] + dist[k][j]) {
                    dist[i][j] = dist[i][k] + dist[k][j];
                }
            }
        }
    }
    return dist;
}
```
???


??? Desafio 2 - Rede social
A imagem abaixo representa um grafo de uma pequena rede desenvolvida entre amigos, para uma disciplina de Engenharia da Computação do Insper. Nele, cada amigo é modelado por um vértice e cada conexão entre amigos é modelada por uma aresta. A distância entre dois amigos é dada pelo número de arestas que separam os dois vértices. 

![](social.png|20)

O professor dessa disciplina, que é muito querido pelos alunos, quer saber qual é o par de amigos que está mais distante um do outro. Para isso vamos utilizar o algoritmo de Floyd Warshall para calcular a matriz de distâncias entre todos os pares de amigos.

Qual a dimensionalidade da matriz de adjacência? Represente a matriz de distâncias na PRIMEIRA iteração do algoritmo de Floyd Warshall, e no FINAL da última iteração (com todas as distâncias calculadas).
::: Gabarito
A matriz tem dimensionalidade 7x7, pois existem 7 vértices.

Após a primeira iteração, a matriz é a mesma da matriz de adjacência: 

![](social-resposta-a.png|20)

Após a última iteração, a matriz é a seguinte:

![](social-resposta-b.png|20)

???
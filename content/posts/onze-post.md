---
title: "PageRank: Métodos probabilísticos por trás das pesquisas feitas no
Google"
date: 2018-05-17T01:38:23-03:00
draft: true
---

Este trabalho foi apresentado no EPBEST 2018 e tem como objetivo apresentar uma métrica
utilizada pelo Google, dentro do seu algoritmo de busca, conhecida como PageRank
($\pi$). A métrica foi criada a partir da necessidade de uma nova forma
de busca, sendo utilizada para posicionar sites ou páginas entre os
resultados, aprimorando a ideia do Altavista passando a levar em conta
outros fatores, além da quantidade, evitando ao máximo a manipulação de
resultados. O algoritmo baseia-se principalmente na contagem de links
que apontam para determinada página na internet, aplicando a ponderação
de pesos, evitando que mecanismos mal intencionados possam burlar o
motor de busca. O PageRank determina o valor da página pelo número e
pela qualidade dos links que apontam para cada página. Procuramos
determinar os fatores que influenciam na medição de qualidade de uma
página. Iremos mostrar o PageRank, através da aplicação de cadeias de
Markov, prosseguindo com uma simulação utilizando sites para cálculo do
PageRank ($\pi$), mostrando os resultados obtidos.

## Introdução

## Processo Markoviano

Um processo estocástico diz-se Markoviano, se for estacionário e gozar
da propriedade de Markov ou da \"perda de memória\", isto é, apenas se o
seu comportamento futuro depender do estado presente, independentemente
dos estados visitados no passado. (ALVES, 1997)

## Cadeia de Markov em tempo discreto
Uma cadeia de Markov em tempo discreto é um processo estocástico em que
a variável $t$ representa intervalo de tempo contável ou finito, sendo
que $\{X(t)| t=0,1,2,3,\hdots\}$, e que obedece a propriedade
markoviana, ou seja, a probabilidade de $X(t)$ estar no estado $j$ no
próximo momento depende apenas do estado atual, não dos estados
passados. Fato que pode ser verificado na fórmula abaixo (ALVES, 1997).
$$P_{ij} = P\{X(t+1)=j | X(t)=i, X(t-1)=k_{t-1},\hdots,X(1)=k_{1},X(0)=k_{0}\}$$
$$= P\{X(t+1)=j | X(t)=i\} \; \forall t= 0,1,2,\hdots$$

Uma cadeia de Markov pode ser representada por meio de um diagrama de
transições, como mostrado na Figura 1, ou por meio de uma matriz de
transição como na Figura 2 contendo as probabilidades de transição entre
estados em determinado momento (ALVES, 1997).

Na matriz de transição $P$, em que $i$ representa estado atual e $j$, o
seu estado futuro, a soma de cada linha deve ser igual á $1$, ou
$100\%$. O valor do elemento $P_{ij}$ representa a probabilidade de
transição entre o estado $i$ para o $j$ em determinado período. Em um
momento futuro, chegar-se a um determinado tempo em que haverá um estado
de equilíbrio, ou seja, alcançar-se um ponto em que as mudanças serão
insignificantes e as probabilidades irão permanecer as mesmas. Dá-se a
isso o nome de Ponto de Equilíbrio ou Estado Estacionário.

O diagrama de transição é uma representação gráfica de uma Cadeia de
Markov. Neste diagrama são visualizados os estados (representado por
círculos), as transições (representadas por arcos) e as probabilidades
das transições. Generalizando, pode-se representar os estados e as
probabilidades de transição, respectivamente, por $E_{i}$ e $P_{ij}$,
onde $i$ e $j$ são um índices que identificam os vários estados
possíveis (logo $P_{ij}$ é a probabilidade de haver uma transição do
estado $E_{i}$ para o estado $E_{j}$). A partir desta generalização,
pode-se desenhar um diagrama, conforme a Figura abaixo.

![image](diagrama.png)

$$P= \begin{tabular}{cccc}
    P_{11} & P_{12} & \ldots & P_{1j} \\
    P_{21} & P_{22} & \ldots & P_{2j}\\
    \vdots & \vdots & \ddots & \vdots\\
    P_{i1} & P_{i2} & \ldots & P_{ij}
    \end{tabular}$$

$$\begin{bmatrix}
1 & 2 & 3\\
a & b & c
\end{bmatrix}$$

$$\begin{array}{ccc}
a&=&b&c&=&d\\
e&=&f
\end{array}$$

$$\begin{aligned}
a&=b&c&=d\\
e&=f
\end{aligned}$$

## Cadeia de Markov Ergótica
Uma cadeia de Markov, ao ser classificada ergódica, ou irredutível,
caracteriza-se pelo fato de que qualquer estado pode retornar a qualquer
outro em um número $n$ definido de passos.

# PageRank

## Motor de Busca
O Google foi criado por Larry Page e Sergey Brin, em 1997, na época do
crescimento da web. No início, o algoritmo primeiramente escolhido foi o
BackRub, contudo, em 1998, foi implementado o PageRank, um novo método
de pesquisa cujo nome homenageia um dos fundadores, código que prometia
ser mais eficiente. Agora, não mais é necessário simular os livros na
internet, os resultados desejados são quase que imediatamente
apresentados, portanto, evita-se a pesquisa exaustiva, como nos textos
físicos.

## O Algoritmo

A fim de fornecer ao usuário a informação requisitada, o PageRank
calcula a importância do site. A métrica PageRank de uma página,
representa a probabilidade de uma pessoa chegar a essa página, clicando
aleatoriamente em hiperligações. O cálculo de PageRank é escalável, ou
seja, é executável em tempo útil se aumentarmos consideravelmente o
número de páginas da rede. O cálculo de PageRank é iterativo, ou seja,
exige várias passagens, chamadas de \"iterações\", os valores obtidos em
cada iteração convergem para os valores desejados de PageRank. Na
primeira iteração é atribuído um valor de PageRank inicial  igual para
todas as páginas (N é o número total de páginas).

Para tanto, é usado um fator de amortização que leva em conta a
possibilidade de um web surfer aleatório, ou seja, um personagem
qualquer clicar em links sucessivos aleatoriamente, pulando de uma
página a outra. O fator de amortização assume valores entre $0$ e $1$,
sendo o valor fixo em $0,85$. A representação probabilística de se
clicar link em uma página que está sendo visitada é de $85\%$, contra
$15\%$ de probabilidade de se escolher outra página aleatória para
começar a navegar de novo.

Na prática, o PageRank elege por meio de votos os conteúdos a serem
posicionados no buscador. De acordo com Magalhães (s.d, p. 11), sendo um
algoritmo de análise de links, atribui um peso numérico a cada elemento
de um conjunto de hiperlinks de documentos, com o objetivo de \"medir\"
a importância relativa dentro do conjunto. Sendo utilizado em diversas
aplicações de qualquer coleção de entidades com citações e referências,
tendo o peso numérico atribuído a qualquer elemento determinado, sendo
também chamado de PageRank de E e é notado como $\pi_{E}$.

Segundo Brin e Page (1998) quanto maior a importância da página, maior
valor ela terá para o PageRank, tendo maior importância a partir de
várias referências de outras páginas. No caso de páginas com maior
PageRank possuírem links apontando para determinado site, maiores serão
as chances dessa página subir no ranking do algoritmo. Assim, o simples
fato de vários sites de menor relevância apontar para um determinado
site não o torna importante.

## Metodologia

Como exemplo, demonstrar-se, a atuação do PageRank em um microuniverso
com somente 4 sites: o G1, indicado pelo número 1, o Mercado-Livre, pelo
número 2, o Youtube, pelo número 3, e o UOL, pelo número 4.

![](exemplodiagrama.png)

Cada site do diagrama é um estado representado na Cadeia de Markov. As
probabilidades de cada um desses sites recomendar outro podem ser vistas
na Figura. Para o cálculo da classificação do PageRank de qualquer
página, /e necessário organizar todas as probabilidades em uma matriz de
transição. Os números 1, 2, 3 e 4, que representam cada site do
microuniverso, também representam sua posição na matriz, a exemplo de
que o site G1 está localizado na linha e coluna 1 da matriz de transição
de estado.

$$P= \begin{array}{c}
1 \\
2 \\
3 \\
4
\end{array}
\left[
\begin{array}{c c c c}
0 & \frac{1}{3} & \frac{1}{3} & \frac{1}{3} \\
0 & 0 & 0 & 1\\
\frac{1}{2} & 0 & 0 & \frac{1}{2}\\
0 & 0 & 1 & 0
\end{array}\right]$$

As probabilidades fictícias apresentadas na matriz de transição são as
chances de ocorrer um determinado evento. Essa tabela mostra que uma
transição do estado indicado na linha muda para o indicado na coluna. No
caso do PageRank, o evento é a chance de um usuário chegar a um
determinado site por meio de cliques aleatórios nos backlinks. Um
exemplo disto é, como dito na Figura 3, que a chance de o internauta
alcançar a página da UOL, a partir do site G1, dentre os backlinks é de
um terço.

O algoritmo busca definir probabilidades estáticas de acesso aos sites
por cliques aleatórios. Dessa maneira, a Cadeia de Markov utilizada será
calculada com base no tempo discreto, um número tão grande a ponto de
que essas probabilidades não se alterem mais, diferentemente de uma
cadeia em tempo contínuo, que verificaria as probabilidades somente em
um determinado momento.

A fim de definir a classificação de uma página, o algoritmo do PageRank
soma todas as probabilidades de um site ser recomendado. Para os
cálculos abaixo, os seguintes comentários serão necessários:

-   O micro universo utilizado no exemplo trata-se de uma cadeia de
    Markov ergódica, que, a partir de qualquer um dos estados, consegue
    transitar-se para qualquer outro;

-   $\pi_{1} \rightarrow$ Representa a probabilidade que o site G1 será
    acessado por outro;

-   $\pi_{2} \rightarrow$ Representa a probabilidade que o site
    Mercado-Livre será acessado por outro;

-   $\pi_{3} \rightarrow$ Representa a probabilidade que o site YouTube
    será acessado por outro;

-   $\pi_{4} \rightarrow$ Representa a probabilidade que o site UOL será
    acessado por outro;

-   A soma de todas estas probabilidades
    $\pi_{1} + \pi_{2} + \pi_{3} + \pi_{4}$ sempre resultarão em $1$.

Após os cálculos, considerando que o estado de equilíbrio será
alcançado, as probabilidades $\pi_{1}$, $\pi_{2}$, $\pi_{3}$ e $\pi_{4}$
consequentemente representarão o PageRank de cada uma das páginas.
Assim, pode-se afirmar que o PageRank de uma determinada página é a soma
de todos os PageRanks dos sites que a recomendaram.

Utilizando os conceitos de distribuição estacionaria temos o seguinte
sistema:

::: center
$\left[\pi_{1}, \pi_{2}, \pi_{3}, \pi_{4}\right]=\left[\pi_{1} \;\; \pi_{2} \;\; \pi_{3} \;\; \pi_{4}\right]\left[
\begin{array}{c c c c}
0 & \frac{1}{3} & \frac{1}{3} & \frac{1}{3} \\
0 & 0 & 0 & 1\\
\frac{1}{2} & 0 & 0 & \frac{1}{2}\\
0 & 0 & 1 & 0
\end{array}\right]$ $\implies$ $$ $\left\{
\begin{array}{llll}

\pi_{1} =\frac{1}{2} \pi_{3}\\ \pi_{2}=\frac{1}{3} \pi_{1}\\
\pi_{3} =\frac{1}{3} \pi_{1} + \pi_{4}\\
\pi_{4} =\frac{1}{3} \pi_{1} + \pi_{2} + \frac{1}{2} \pi_{3}\\
\pi_{1} + \pi_{2} + \pi_{3} + \pi_{4}=1

\end{array}\right.$
:::

Resolvendo o sistema encontramos

$\pi_{1} = 0,2$ $\pi_{2} = 0,066$ $\pi_{3} = 0,4$ $\pi_{4} = 0,334$

Após os cálculos, pode ser concluído que:

-   A página da internet com o maior Page Rank do exemplo é o YouTube,
    com a classificação de $0.4$, e portanto, o site de maior
    relevância;

-   A página da internet com o menor Page Rank do exemplo é o
    Mercado-Livre, com a classificação de $0.066$, portanto, o site de
    menor relevância;

-   Logo, em uma pesquisa, a ordem que estes sites apareceriam na página
    do Google seriam: 1º-YouTube, 2º-UOL, 3º-G1 e 4º-MercadoLivre.

Os resultados atingidos com $\pi_{1}$, $\pi_{2}$, $\pi_{3}$ e $\pi_{4}$
são as probabilidades estacionárias, ou seja, elas não mudarão com o
acréscimo ou decréscimo de visitas às páginas do micro universo.

O que o algoritmo do PageRank faz é, em sua essência, replicar esses
cálculos milhares de vezes em um universo muito maior de sites para
trazer ao usuário uma maior comodidade e melhor qualidade na busca pela
informação.

## Resultados e Discussões

O PageRank é um algoritmo eficiente para ranqueamento de sites usado
pelo Google, apesar de haver vários fatores que podem influenciar na
popularidade de um site, em linhas gerais, quanto maior o número de
sites que apontam para um site (ou seja, backlinks) maior será o seu
PageRank.

No nosso caso vimos o exemplo em microuniverso, para ver popularidade de
um site, levando em conta o seu PageRank.

## Considerações Finais

Pôde-se constatar que o PageRank utiliza-se da cadeia de Markov, e que a
classificação ou ranqueamento depende de uma serie de fatores, que
inclusive inibem o modelo baseado apenas no número de backlink como
atributo principal de classificação. Assim, para que o site possa ser
melhor classificado nas pesquisas dos buscadores é necessário backlink
de sites mais populares diante do Google, além da necessidade de
semelhança no conteúdo.

O estudo trouxe informações que deram maior compreensão à forma
utilizada pelo Google para classificar os sites existentes, assim como
os modelos matemáticos e probabilísticos, podendo influir de forma
significativa na classificação de sites e mediante consultas a
determinado endereços eletrônicos.

[^1]: UFCG - Universidade Federal de Campina Grande. Email:
    *jerfson35@gmail.com*

[^2]: UFCG - Universidade Federal de Campina Grande. Email:
    *amanda.natalia.gomes@gmail.com*

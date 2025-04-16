---
slug: prolog
title: Prolog na Lógica de Predicados - Uma Abordagem Recursiva
date: 2023-07-08
authors: Eliziane
tags: [prolog, matematica, homeworks]
keywords: [prolog, matematica, homeworks]
---
[GitHub](https://github.com/el1ziane/predicadosprolog)

Neste post, vou compartilhar um trabalho que fiz na faculdade na disciplina de matemática discreta. Aqui vou explorar como o Prolog implementa a lógica de predicados de forma recursiva e como essa característica torna a linguagem util para problemas que envolvem inferências lógicas.

## Por que o Prolog é Considerado Recursivo? 🔄

O Prolog tem uma definição recursiva porque suas regras podem se referir a si mesmas ou a outras regras, assim criando estruturas de programação onde as regras podem ser aplicadas repetidamente para resolver problemas de maneira iterativa, chamando a si mesmas em um processo de recursão. Dessa forma, quando utilizamos uma caso recursivo, sua regra é definida de modo que a chamada recursiva siga sobre uma lista menor do que a lista inicial, a recursão permite a resolução de problemas complexos de maneira simples.

## Fatos em Prolog: Por que Fato 1 e Fato 3? 🤔
Suponha que um banco de dados Prolog contém as seguintes informações:

```
come(urso, peixe)
come(peixe, peixinho)
come(peixinho, alga)
come(guaxinim, peixe)
come(urso, guaxinim)
come(urso, raposa)
come(raposa, coelho)
come(coelho, grama)
come(urso, veado)
come(veado, grama)
come(lince, veado)
animal(urso)
animal(peixe)
animal(peixinho)
animal(guaxinim)
animal(raposa)
animal(coelho)
animal(veado)
animal(lince)
planta(grama)
planta(alga)
presa(X) <= come(Y, X) e animal(X)

Poderíamos, então, ter o seguinte diálogo com o Prolog:
?animal(coelho)
sim
?come(lince, grama)
não
?come(X, peixe)
urso
guaxinim
?come(X, Y) e planta(Y)
peixinho alga
coelho grama
veado grama
?presa(X)
peixe
peixinho
peixe
guaxinim
raposa
coelho
veado
veado
```

Note que o peixe é listado duas vezes na resposta à última consulta, pois os peixes são comidos por ursos (fato 1) e por guaxinins (fato 3). Analogamente, veados são comidos por ursos e por linces.

Os fatos são essenciais para responder a consultas e tomar decisões com base nas regras, definidas no programa. Podemos defini-los como constantes que tornam os predicados verdadeiros, assim no banco de dados fornecido tanto o fato 1 quanto o fato 3 são chamados de fatos porque são declarações que afirmam relações entre objetos sem nenhuma condição.
	Com isso pode-se explicar os fatos: 1 e 3 para exemplificar:
```
come(urso, peixe)
come(guaxinim, peixe)
```
- Fato 1: come(urso, peixe). – Afirma que o urso come peixe.
- Fato 3: come(guaxinim, peixe). – Afirma que o guaxinim também come peixe.
Desse modo, em todos os outros fatos do programa teremos sempre constantes com afirmações sobre os predicados.

## Definindo o Predicado predador 🦁
```
predador(X) :- come(X, Y), animal(X), animal(Y)
```
Nessa regra houve a inclusão de “animal(Y)” para verificar se o animal comido “come(X,Y)” também é um animal e não uma planta.

Adicionando essa regra ao banco de dados, a consulta:

```
?- predador(X)
```
gera os seguintes resultados:

```
X = urso ;
X = peixe ;
X = guaxinim ;
X = urso ;
X = urso ;
X = raposa ;
X = urso ;
X = lince.
```
## Resultados das Consultas 📋
Baseado na estrutura do seu banco de dados, podemos listar os resultados esperados para diversas consultas:

![Prolog](/img/project/prolog.png "Prolog")

## Busca em Profundidade em Prolog 🔍
A busca em profundidade em Prolog refere-se ao processo de execução de um programa Prolog como uma busca em profundidade ao longo de uma árvore de inferência. Os níveis de profundidade da árvore de inferência são numerados sequencialmente a partir da raiz, onde o número zero é atribuído à raiz, nessa árvore, cada nó associa-se a  um objetivo e cada objetivo está associado a um conjunto de cláusulas. 
O Prolog utiliza a memória associativa para armazenar informações sobre as ligações entre variáveis e seus valores, bem como a profundidade de inferência atual. Permitindo a execução eficiente do mecanismo de retrocesso (capacidade de voltar atrás durante a execução para reverter ações e explorar outras possibilidades quando necessário.), pois, quando ocorre um retrocesso em uma profundidade de inferência, a memória associativa é usada para desfazer todas as ligações associadas a essa profundidade.

## Prolog e a Lógica de Predicados: Relação com o Modus Ponens
Os conceitos de Prolog estão relacionados com a lógica de predicados porque Prolog é uma linguagem de programação que se baseia na lógica de predicados. Enquanto a lógica proposicional é limitada, a lógica de predicados permite representar conhecimento complexo com quantificadores, funções e predicados. Prolog usa os princípios da lógica de predicados, com elementos como fatos, regras e consultas, para representar e manipular conhecimento e soluções de problemas, tornando a lógica de predicados fundamental na estrutura do Prolog.

A regra de Modus Ponens em lógica de predicados funciona da seguinte maneira:

- Se tivermos uma afirmação condicional do tipo "Se A, então B" (premissa).
- E tivermos a afirmação de que "A" é verdadeiro (premissa).
- Então, podemos concluir que "B" é verdadeiro (conclusão).
Para exemplificar em um programa Prolog podemos ter as regras **`tem_penas(X) :- tem_asas(X)`** e **`voa(X) :- tem_penas(X)`** que são consideradas exemplos de Modus Ponens, pois estabelecem condições e consequências. Se uma condição (ter asas ou ter penas) é satisfeita, então a consequência (ter penas ou voar) pode ser inferida.
![Prolog](/img/project/prolog2.png "Prolog")

## Conclusão:

Pode-se entender como a lógica de predicados é uma extensão da lógica proposicional que permite representar e raciocinar sobre informações mais complexas e abrangentes. Ela introduz recursividade, quantificadores, variáveis, regras e predicados, tornando-a adequada para expressar sentenças que envolvem relações entre objetos e conjuntos de objetos. A linguagem Prolog, por sua vez, por ser baseada no paradigma lógico, é amplamente usada em inteligência artificial, robótica e ciência de dados.
Neste post, foram introduzidos alguns dos conceitos fundamentais da lógica de predicados, como predicados, regras e a sintaxe inicial da linguagem Prolog , e como esses conceitos são aplicados na representação de  inferência em Prolog. Sendo o princípio das inferências muito semelhante a utilizada em lógica proposicional,  como a regra de Modus Ponens utilizada para derivar conclusões lógicas com base em premissas e regras definidas em Prolog.


## Referências:

LAGO, Silvio. INTRODUÇÃO À LINGUAGEM PROLOG. 06/02/2009. Disponível em: https://www.ime.usp.br/~slago/slago-prolog.pdf. Acesso em: 08/09/2023.

HOR-MEYLL, Malena O.; FEITOSA, Raul Q.; AMORIM, Cláudio L. de. MPA - Máquina Prolog Associativa. In: INTERNATIONAL SYMPOSIUM ON COMPUTER ARCHITECTURE AND HIGH PERFORMANCE COMPUTING (SBAC-PAD), 5. , 1993, Florianópolis/SC. Anais [...]. Porto Alegre: Sociedade Brasileira de Computação, 1993. p. 631-645. Disponível em: https://doi.org/10.5753/sbac-pad.1993.23065. Acesso em 08/09/2023.

LEVADA, Alexandre Luis Magalhães. Lógica dos predicados.10-Dez-2012. Disponível em: http://livresaber.sead.ufscar.br/handle/123456789/1047. Acesso em: 08/09/2023.

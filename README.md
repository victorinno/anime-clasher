# anime-clasher

Maninhoooo!!!

Como você sabe nosso jogo AC tem a premissa de permitir muita customização para os personagens. Podemos aproveitar o poder dos Java 8 para realizar isso.

Com lambdas o java passou a ser um linguagem funcional, tornando as funções cidadões de primeira classe. Isso possibilitou a criação de high order functions, que nada mais é que permitir que funções sejam objetos, podendo ser passado como parametro ou ser o retorno de um método.

A partir desse momento, podemos fazer funções que criam funções. Que é o que vamos fazer.

A sintwaxe de um lambda é bem simples

```java
(x) -> x + 1;
```

Essa sintaxe representa uma função que retorna o valor passado mais 1. Podemos usar uma das novas interfaces do Java para alocar esse valor numa variável.

```java
Function<Integer, Integer> somar1 = (x) -> x + 1;
```

Mas e se quisermos fazer uma função que eu passe um número e me retorne uma outra função que soma o parametro passado com esse número?

```java
Function<Integer, Function<Integer, Integer> funcaoSomar = (y) -> (x) -> x + y;
```

Percebe o que acabamos de fazer? E o como usamos essa mágica?


```java
Function<Integer, Function<Integer, Integer> funcaoSomar = (y) -> (x) -> x + y;
Function<Integer, Integer> somar10 = funcaoSomar.apply(10);
somar10.aplly(1); //Resultado 11
```

Agora podemos fazer várias pequenas funções que somam os valores que queremos.

O princípio de nosso porjeto será o mesmo. Só que os poderes serão funções no nosso caso que esperam um player e serão construídas a partir de parametros passados via json.

O objetivo primeiro é construir um serviço rest que substituirá os prints de tela que faziamos, se quisermos ver o status tem um serviço para isso por exemplo.

Nesse primeiro momento:

* Serviço de status
* Serviço de listar poderes
* Serviço de criar poderes
* Serviço de modificar poderes
* Serviço de deletar poderes
* Serviço de usar poderes
* Serviço de defesa

Todos eles vão se basear em json, ou seja teremos que ter algoritmos que entendem e contruam json para podermos manipular os poderes e criar as funões que os representam.

Em termos de estrutura de dados vamos ter:
* Player
* --Nome
* --Parametros
* -- --Força, destreza, agilidade, vigor, hp, maxhp
* --Classe
* -- -- Nome, Força, destreza, agilidade, vigor, hp
* -- Bonus
* -- -- HIT, ESQUIVA, DEFESA, CRITICO, DANO CRITICO, TREINOS:{ Nome, Força, destreza, agilidade, vigor, maxhp }

Os parametros são do personagem os atributos dos personagens em si, a classe traz a chance que o personagem tem de crescer o parametro ao fazer um ataque ou uma defesa, não mais que 5% e nem menos que 1%, num total de 10%, os bonus são aplicados juntos com os outros parametros, nesse momento pode ser tudo 0.

Vou deixar um projeto em Maven com spring boot, vai te ajudar e vou deixar os links com tutoriais ;)

[Link para início com spring boot](https://projects.spring.io/spring-boot/)
[Link que ensina a fazer um serviço rest com spring boot](https://spring.io/guides/gs/rest-service/)
[Biblioteca que ajuda com interfaces funcionais, podemos usar as que derivam da function, como Funcation1,2,3 até 9, cada uma delas o número representa a quantidade de parametros passados.](http://www.javaslang.io/javaslang-docs/)

summary: Desafio: construir uma API que simule o funcionamento de parte do mercado livre. 
id: desafio-mercado-livre
categories: Web
tags: medium
status: Published 
authors: Zarin
Feedback Link: https://zarin.io

# Será que você é capaz de implementar uma api para servir o mercado livre?
<!-- ------------------------ -->
## Como funciona
Duration: 5

A ideia aqui é que você e o código sejam protagonistas. Cada capítulo tem uma funcionalidade para ser desenvolvida. Para te ajudar na implementação, disponibilizamos alguns materiais de suporte com informações que podem ser úteis para você :). 

O detalhe interessante é que o material é justamente de suporte. 

* Acha que precisa do suporte? Então vai lá e consulta
* Acha que não precisa? Então não consulta.
* Acha que não precisa mas quer saber o que pensamos: Faz primeiro e consulta depois. 

A parte legal é que você usa o material de suporte que faz sentido para você na ordem que você quiser. Este é um material online criado para ser adaptado ao seu ritmo e seu background. 

<!-- ------------------------ -->
## Colabore com outros(as) zuppers
Duration: 2

Cada funcionalidade pode ser implementada de n formas, usando tecnologias diferentes e tudo mais. Nossa sugestão é que além de você publicar seu código no github e deixar disponível para outros(as) zuppers, você também compartilhe posts contando a história de cada funcionalidade implementada :). Alguns tópicos legais são: O que você aprendeu? Quais foram as dificuldades? 

<!-- ------------------------ -->
## Setup do projeto
Duration: 10

Agora vamos começar o projeto de verdade. Ele pode ser desenvolvido na linguagem que mais se adeque as suas necessidades. Alguns exemplos:

- Java
- Kotlin
- Javascript
- C#

Combinado com alguma dessas linguagens, minha sugestão é que você escolha o conjunto de tecnologias que mais te interessa no momento e que você acha que vai fazer você ser uma versão melhor na sua carreira e, consequentemente, no seu momento profissional. Exemplos de combinações:

- Java + Spring
- Kotlin + Spring
- Javascript + Nest.js
- C# + asp.net core

Caso queira usar outra combinação fique a vontade. Configure seu projeto, rode um hello world, verifique se está tudo funcionando e siga em frente :).

<!-- ------------------------ -->
## Cadastro de um novo usuário
Duration: 30

### necessidades

* precisamos saber o instante do cadastro, login e senha.

### restrições

* O instante não pode ser nulo e não pode ser no futuro
* O login não pode ser em branco ou nula
* O login precisa ter o formato do email
* A senha não pode ser branca ou nula
* A senha precisa ter no mínimo 6 caracteres
* A senha deve ser guardada usando algum algoritmo de hash da sua escolha.

### resultado esperado
* O usuário precisa estar criado no sistema
* O cliente que fez a requisição precisa saber que o usuário foi criado. Apenas um retorno com status 200 está suficente.

### material de suporte

É natural que vamos querer salvar esses dados em algum lugar, como um banco de dados. A JPA vem como uma especificação que cria as interfaces de acesso ao banco de dados. O Hibernate, por sua vez, é a implementação da JPA. 


[O Spring possui um projeto que une a JPA e facilita na criação da camada de acesso a dados, que é o Spring Data JPA. Uma boa fonte para aprender sobre esse projeto é a documentação](https://docs.spring.io/spring-data/jpa/docs/current/reference/html/#repositories.core-concepts). 

[Além disso, existem bons posts que mostram como começar a criar essa camada de acesso aos dados](https://spring.io/blog/2011/02/10/getting-started-with-spring-data-jpa/).

[A apostila aberta da Caelum, também é uma fonte interessante se você quiser saber um pouco mais sobre JPA e Hibernate também](https://www.caelum.com.br/apostila-java-web/uma-introducao-pratica-ao-jpa-com-hibernate/#mapeando-uma-classe-tarefa-para-nosso-banco-de-dados) 

[Além da camada de acesso ao banco, o Hibernate implementa a especificação da Bean Validation que é um conjunto de regras de validação que a gente pode utilizar no projeto. A especificação é uma fonte excelente para consulta](https://beanvalidation.org/2.0/spec/). [Esse post da Baeldung também é uma fonte legal para utilizar a Bean Validation com Spring Boot](https://www.baeldung.com/spring-boot-bean-validation)

[Vídeo sobre DDD](https://youtu.be/vOaRwq5JOXk)

<!-- ------------------------ -->
## Não podemos ter dois usuários com o mesmo email.
Duration: 30

### necessidades

* Só pode existir um usuário com o mesmo email. 

### resultado esperado
* Status 400 informando que não foi possível realizar um cadastro com este email. 

<!-- ------------------------ -->
## Cadastro de categorias

Duration: 30

### necessidades

No mercado livre você pode criar hierarquias de categorias livres. Ex: Tecnologia -> Celulares -> Smartphones -> Android,Ios etc. Perceba que o sistema precisa ser flexível o suficiente para que essas sequências sejam criadas.

* Toda categoria tem um nome
* A categoria pode ter uma categoria mãe

### restrições

* O nome da categoria é obrigatório
* O nome da categoria precisa ser único

### resultado esperado
* categoria criada e status 200 retornado pelo endpoint.
* caso exista erros de validação, o endpoint deve retornar 400 e o json dos erros.


<!-- ------------------------ -->
## TRABALHANDO COM O USUÁRIO LOGADO(VAI IMPACTAR NO RESTO DO CÓDIGO)

### problema
Você precisa configurar um mecanismo de autenticação via token, provavelmente com o Spring Security, para permitir o login. Caso queira, é só olhar nesse link aqui => https://gitlab.com/aovs/projetos-cursos/fj27-alura-forum-api/tree/master/src/main/java/br/com/alura/forum/security . Aí tem todo código de segurança necessário para autenticar no Spring Security via token jwt. Fique a vontade para entendê-lo e aplicar no projeto. 

### Solução que eu faria para focar mais nas features

Em todo trecho de código que precisa do usuário logado, na primeira linha do método do controller que precisa de um usuário logado, eu buscaria pelo usuário com um email específico e usaria ele como "referência logada" na aplicação. 

Depois, se você quiser, é só habilitar o security, receber o usuário como argumento do método e apagar essa linha... Tudo deveria funcionar normalmente.



<!-- ------------------------ -->
## Usuário logado cadastra novo produto

Duration: 30

### explicação
Aqui a gente vai permitir o cadastro de um produto por usuário logado.

###  necessidades

* Tem uma mais fotos associadas
* Tem um nome
* Tem um valor
* Tem quantidade disponível
* Características(cada produto pode ter um conjunto de características diferente)
 * Da uma olhada nos detalhes de produtos diferentes do mercado livre.
* Tem uma descrição que vai ser feita usando Markdown
* Pertence a uma categoria
* Instante de cadastro


### restrições

* Tem uma ou mais fotos
* Nome é obrigatório
* Valor é obrigatório e maior que zero
* Quantidade é obrigatório e >= 0
* O produto possui pelo menos três características
* Descrição é obrigatória e tem máximo de 1000 caracteres.
* A categoria é obrigatória

### resultado esperado
* Um novo produto criado e status 200 retornado
* Caso dê erro de validação retorne 400 e o json dos erros




<!-- ------------------------ -->
## Não podemos ter dois usuários com o mesmo email.

Duration: 30


<!-- ------------------------ -->
## Não podemos ter dois usuários com o mesmo email.

Duration: 30


<!-- ------------------------ -->
## Não podemos ter dois usuários com o mesmo email.

Duration: 30



<!-- ------------------------ -->
## Não podemos ter dois usuários com o mesmo email.

Duration: 30


<!-- ------------------------ -->
## Não podemos ter dois usuários com o mesmo email.

Duration: 30


<!-- ------------------------ -->
## Não podemos ter dois usuários com o mesmo email.

Duration: 30


<!-- ------------------------ -->
## Não podemos ter dois usuários com o mesmo email.

Duration: 30

<!-- ------------------------ -->
## Não podemos ter dois usuários com o mesmo email.

Duration: 30


<!-- ------------------------ -->
## Não podemos ter dois usuários com o mesmo email.

Duration: 30
# Introdução

## O que é bytecode?

Bytecode é uma sequencia de bytes (dados) escritos em um arquivo para ser lido posteriormente por uma plataforma que suporte esta sequencia, muitos compiladores além do compilador Java traduzem o código-fonte para bytecode, um exemplo é o compilador Python. A forma que este Bytecode será tratado depende da implementação da plataforma.

## JVM Bytecode

Quando falamos de `JVM Bytecode`, é o bytecode qual a JVM (Máquina Virtual Java) pode entender, aqui irei explicar sobre ele, e irei me referir a ele somente como `Bytecode`.

Na JVM o Bytecode pode ser interpretado ou compilado, isto varia muito, porém o que iremos tratar aqui é a interpretação dele e como cada `Opcode` (ou Instrução), funciona, com exemplos, tanto em Java como em Bytecode, mas não se preocupe, não iremos tratar bytes aqui, irei mostrar somente as instruções, que é o relevante.

## Objetivo

A primeira coisa que deve vir a sua cabeça é: "Por que eu devo entender isto?""

Bom, se você não vai utilizar para nada na sua vida, então não perca seu tempo, a não ser que queira aprender algo novo, agora se planeja criar algum framework que trabalhe com Bytecode ou pretende criar algum compilador, este será um ótimo guia, posteriormente falarei sobre o mais famoso framework de geração de Bytecode, o [ASM](http://asm.ow2.org/).

## Capitulos

- [Capitulo 1 - Descrições, Tipos, Modificadores](capitulo1/)
- [Capitulo 2 - Classes, Inicialização, Fields e metodos](capitulo2/)
- [Capitulo 3 - Instruções basicas](capitulo3/)
- [Capitulo 4 - Invocando métodos](capitulo4/)
- [Capitulo 5 - Criando lambdas e invocações dinamicas](capitulo5/)
- [Capitulo 6 - Controle de fluxo: Labels, break, continue, ifs, for, for-each, while, do-while](capitulo6/)
- [Capitulo 7 - Controle de exceções e recursos: try-catch e try-with-resources](capitulo7/)

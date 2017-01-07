# Introdução

Neste capitulo falaremos sobre as classes, inicialização das classes, fields e metodos.

# Classes

Toda classe **precisa** ter sua versão, um nome binario, o modificador `ACC_SUPER` (porque não trabalharemos com classes de antes do Java 1.1), uma super classe e no minimo um construtor (`<init>`) (`<clinit>` é opcional). No caso de interfaces não é necessario o modificador `ACC_SUPER`, mas é necessário o modificador `ACC_INTERFACE`, para anotações e enums, os modificadores `ACC_ANNOTATION` e `ACC_ENUM` respectivamente.

Classes podem ter opcionalmente anotações e descrição de assinatura e tipos genéricos.

# Classes inner

Um arquivo `.class` só pode ter uma declaração de classe, as demais classes são compiladas para arquivos separados, e o acesso a membros privados da classe outer são feitos por meio de metodos sinteticos, as classes outer precisam especificar quais são suas classes inner.

Quando uma classe é definida, suas classes inner precisam ser definidas também.

##### Acesso sintetico aos membros privados

Quando você pretende criar inner classes, deve-se ter muita atenção com o acesso aos membros, em Java isto é totalmente possivel:

```java
class A {
  private final String name = "A";

  class B {
    public String getName() {
      return this.A.name;
    }
  }
}
```

Porém, é um código problematico e esconde um acesso sintatico, é impossivel qualquer classe acessar membros privados de outras classes, mesmo elas sendo uma classe inner, isto é possivel no caso de membros `package-private`, `public` ou `protected`.

Veja o código que é gerado pelo compilador:

```java
class A {
  private final String name = "A";

  String access$name(B b) { // Membro sintetico
    return this.name;
  }
}

class B {
  private final A outer$A;

  B(A a) {
    this.outer$A = a;
  }

  public String getName() {
    return this.outer$A.access$name(this);
  }
}
```

Ao tratar inner classes precisamos ou proibir access aos membros privados da classe outer ou gerar um membro sintetico (este foi o principal motivo pelo qual adiei a geração de classes inner 2 vezes na CodeAPI).

As classes inner são tratadas como uma classe qualquer que recebe uma outra instancia de outra classe no construtor, o trabalho duro todo é feito pelo compilador.

# Inicialização de classes

Sempre que uma classe é inicializada um método estático `<clinit>` é chamado, este método não tem parametros e retorna um `void`. Os construtores das classes se chamam `<init>` e sempre retornam um `void`, eles podem receber parametros, mas só podem retornar `void`.

##### Construção de instancia

A construção de instancia se consiste em duas fases:

- Criar uma instancia não inicializada.
- Chamar o construtor para inicializa-la.

a primeira fase não chama nenhum método, apenas diz para a JVM criar uma instancia vazia da classe, na segunda fase é passada esta instancia para o construtor da classe, e este chama o construtor `super`, e a classe é declarada como inicializada quando, por fim, o construtor da classe `Object` é chamado.


# Fields

Fields precisam ter tipos descritos e pelo menos um nome, e opcionalmente modificadores, anotações e descrição de tipo genérico, duas fields com mesmo nome e tipos diferentes podem existir, isto não é possivel na linguagem Java.

Os valores padrões de uma field podem ser constantes ou inicializados dentro dos construtores ou construtor, geralmente eles são inicializados nos construtores, isto ocorre após a invocação do construtor `super` e antes das definições de variaveis presentes no código-fonte.

# Métodos

Precisam ter os tipos dos parametros e retorno descritos, e seu nome, podem existir dois métodos com mesmo nome e mesmos parametros e retornos diferentes, isto não é possivel na linguagem Java. Podem ter opcionalmente modificadores, anotações e descrição de assinatura e tipos genéricos.

Os métodos podem ter opcionalmente um corpo, se tiverem devem retornar algo, até mesmo void (existe uma instrução especial para isto).

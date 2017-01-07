# Introdução

Aqui falaremos sobre armazenamento das informações na JVM, acesso a fields, definição de valores das fields e variaveis.

# Armazenamento

`Operand stack`: stack com valores a ser operados

`Frame Stack`: Stack do frame atual, todo método cria uma frame stack, toda frame stack tem sua propria operand stack, e outras frame stack podem ser criadas dentro de métodos, como no caso de controle de fluxo.

`Local variable`: Uma array que guarda os valores das variaveis locais por posição (**não guarda os tipos**).

# Instruções

Para detalhes sobre as instruções veja a documentação da JVM: [aqui](https://docs.oracle.com/javase/specs/jvms/se8/html/jvms-6.html).

# Basico

Em todos métodos que não são estaticos, o primeiro parametro é a instancia do objeto, ou seja, a variavel de numero 0 é a instancia do objeto, nos métodos estaticos o primeiro parametro é o primeiro parametro do método - se houver algum parametro.

A JVM é baseada em Stack, o que quer dizer que o `Ultimo valor a entrar é o primeiro a sair` (LIFO). Ao inserir um valor na memoria, ele entrará no `topo` da stack, quando for obter um valor da stack, ela irá pegar o valor do `topo`.

Exemplo:

```
ldc "B" // Adicionado ao topo: [B]
ldc "A" // Adicionado ao topo: [A, B]
astore 1 // Guarda "A" na local variable posição 1, stack: [B]
astore 2 // Guarda "B" na local variable posição 2, stack: []
```

# Acessando fields

Para acessar fields utilizamos as instruções `getfield` e `getstatic`.

A instrução `getfield` é utilizada para obter valores de fields de instancia, a instrução `getstatic` para obeter valores de fields estaticas, para ambas instruções é necessário informar o nome binário da classe em que a field esta localizada, o nome da field e a descrição do tipo dela.

```java
final class A {
  public static final int num = 9;

  public final String name = "A";
}
```

Para obtermos o valor das fields:

```
getstatic com/to/A.name:Ljava/lang/String; // com/to/A = localização, name = nome da field, Ljava/lang/String; = tipo String.

aload 1 // Instancia da classe A

// Recebe a instancia da operand stack
getfield com/to/A.num:I // com/to/A = localização, num = nome da field, I = tipo int.
```

# Inserindo valor nas fields

Para inserirmos valores nas fields utilizamos as instruções `putfield` e `putstatic`, que tem um funcionamento parecido com as de acesso, porém elas recebem 1 parametro a mais da `operand stack`, que é o valor a ser inserido.

Suponhamos que queremos inserir valores nas fields `num` e `name`, e que neste momento elas não são finais:

```java
final class A {
  public static int num = 9;

  public String name = "A";
}
```

```
ldc "B" // Inserimos o valor a ser definido na operand stack
putstatic com/to/A.name:Ljava/lang/String; // puxamos este valor para a field

aload 1 // Instancia da classe A
ldc 40 // Insermos o valor a ser definido na operand stack

// Recebe a instancia da operand stack
// Recebe o valor da operand stack
putfield com/to/A.num:I // puxa o valor para a field
```

**Obs:** As instancias devem sempre ser colocadas primeiro na `operand stack`, a stack é LIFO, porém as instruções recebem elas na ordem em que são colocadas na stack.


# Variaveis

Diferente das fields, as variaveis são tratadas de formas diferentes, elas são armazenadas na `local variable` e não tem nome ou tipo; o nome, tipo e tipo genérico só podem ser informados na `LocalVariableTable`, que falarei posteriormente quando estiver explicando sobre o framework ASM. A `LocalVariableTable` é irrelevante para a JVM, porém é importante para decompiladores e IDEs.

Elas são armazenadas e lidas com as instruções de `store` e `load`, a instrução varia de acordo com o tipo da variavel (veja [JVM Instruction Set ](https://docs.oracle.com/javase/specs/jvms/se8/html/jvms-6.html) (em ingles)).

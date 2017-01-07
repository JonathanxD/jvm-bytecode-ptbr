# Sugar Syntax

## O que é

Sugar syntax é uma sintaxe mais amigavel qual será convertida para um outro código menos amigavel pelo compilador.

## Exemplos

### For each

```java
for (String a : messages) {
  System.out.println(a);
}
```

#### Iterable

```java
Iterator<String> iterator = messages.iterator();

while(iterator.hasNext()) {
  String a = iterator.next();
  System.out.println(a);
}
```

#### Array

```java
int size = messages.length;

for(int x = 0; x < size; ++x) {
  String a = messages[x];
  System.out.println(a);
}
```

### Genéricos e lambdas

Os genéricos são mais que apenas um sugar syntax, mas não deixa de ser um no final das contas, todos tipos genéricos são ou `Object` ou seu tipo bound (`Object` no caso de lower bound), e é feito cast para os tipos reais.

Já os lambdas que não sejam method reference, são sugar syntax convertidos para um método especial - em casos especiais os method references também são convertidos, como o caso exibido abaixo.

```java
interface Sequence<T> {
  void forEach(Consumer<T> consumer);
}

class Test {
  public void b() {
    Sequence<String> seq = ...;
    seq.forEach(System.out.println(s));
  }
}
```

É transformado em:

```java
interface Sequence {
  void forEach(Consumer consumer);
}


class Test {
  public void b() {
    Sequence seq = ...;
    seq.forEach(this::consume);
  }

  void consume(Object o) {
    System.out.println((String) o);
  }
}
```

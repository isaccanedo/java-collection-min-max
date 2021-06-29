## Encontrar o máximo/mínimo de uma lista ou coleção

# 1. Introdução
Uma introdução rápida sobre como encontrar o valor mínimo/máximo de uma determinada lista/coleção com a poderosa API Stream em Java8.

# 2. Encontre o máximo em uma lista de inteiros
Podemos usar o método max() fornecido por meio da interface java.util.Stream. Ele aceita uma referência de método:

```
@Test
public void whenListIsOfIntegerThenMaxCanBeDoneUsingIntegerComparator() {
    // given
    List<Integer> listOfIntegers = Arrays.asList(1, 2, 3, 4, 56, 7, 89, 10);
    Integer expectedResult = 89;

    // then
    Integer max = listOfIntegers
      .stream()
      .mapToInt(v -> v)
      .max().orElseThrow(NoSuchElementException::new);

    assertEquals("Should be 89", expectedResult, max);
}
```

Vamos dar uma olhada no código:

- Chamar o método stream() na lista para obter um fluxo de valores da lista;
- Chamar mapToInt (valor -> valor) no fluxo para obter um fluxo inteiro;
- Chamar o método max() no fluxo para obter o valor máximo;
- Chamar orElseThrow() para lançar uma exceção se nenhum valor for recebido de max().

# 3. Encontre o mínimo com objetos personalizados
Para encontrar o mín. / Máx. Em objetos personalizados, também podemos fornecer uma expressão lambda para nossa lógica de classificação preferida.

Vamos primeiro definir o POJO personalizado:

```
class Person {
    String name;
    Integer age;
      
    // standard constructors, getters and setters
}
```

Queremos encontrar o objeto Person com a idade mínima:

```
@Test
public void whenListIsOfPersonObjectThenMinCanBeDoneUsingCustomComparatorThroughLambda() {
    // given
    Person alex = new Person("Alex", 23);
    Person john = new Person("John", 40);
    Person peter = new Person("Peter", 32);
    List<Person> people = Arrays.asList(alex, john, peter);

    // then
    Person minByAge = people
      .stream()
      .min(Comparator.comparing(Person::getAge))
      .orElseThrow(NoSuchElementException::new);

    assertEquals("Should be Alex", alex, minByAge);
}

Vamos dar uma olhada nesta lógica:

- Chamar o método stream() na lista para obter um fluxo de valores da lista;
- Chamar o método min() no fluxo para obter o valor mínimo. Estamos passando uma 
função lambda como comparador, ela é usada para decidir a lógica de classificação
para decidir o valor mínimo;
- Chamar orElseThrow() para lançar uma exceção se nenhum valor for recebido de min().
```

# 4. Conclusão
Neste artigo rápido, exploramos como os métodos max() e min() da API Stream do Java 8
podem ser usados para encontrar o valor máximo e mínimo de uma Lista/Coleção.

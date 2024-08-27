# Iterator

O padrão de projeto Iterator é um padrão comportamental que permite o acesso sequencial aos elementos de uma coleção sem expor sua representação subjacente. O Iterator fornece uma maneira de acessar os elementos de um objeto agregado de forma transparente, sem precisar saber como os elementos estão organizados internamente.

### Estrutura do Iterator

1. **Iterator**: Interface que declara os métodos necessários para percorrer uma coleção, como `hasNext()` e `next()`.
2. **Concrete Iterator**: Implementa a interface Iterator e mantém o controle da posição atual na iteração.
3. **Aggregate**: Interface que declara um método para criar um objeto Iterator.
4. **Concrete Aggregate**: Implementa a interface Aggregate e retorna uma instância do Concrete Iterator.

### Exemplo em Java

Vamos considerar um exemplo de uma coleção simples de nomes.

### Iterator Interface

```java
public interface Iterator<T> {
    boolean hasNext();
    T next();
}

```

### Concrete Iterator

```java
public class NomeIterator implements Iterator<String> {
    private String[] nomes;
    private int posicao = 0;

    public NomeIterator(String[] nomes) {
        this.nomes = nomes;
    }

    @Override
    public boolean hasNext() {
        return posicao < nomes.length;
    }

    @Override
    public String next() {
        if (this.hasNext()) {
            return nomes[posicao++];
        }
        return null;
    }
}

```

### Aggregate Interface

```java
public interface ColecaoNomes {
    Iterator<String> criarIterator();
}

```

### Concrete Aggregate

```java
public class NomeColecao implements ColecaoNomes {
    private String[] nomes;

    public NomeColecao(String[] nomes) {
        this.nomes = nomes;
    }

    @Override
    public Iterator<String> criarIterator() {
        return new NomeIterator(nomes);
    }
}

```

### Client

```java
public class Main {
    public static void main(String[] args) {
        String[] nomes = {"Alice", "Bob", "Charlie", "Diana"};
        NomeColecao colecao = new NomeColecao(nomes);

        Iterator<String> iterator = colecao.criarIterator();
        while (iterator.hasNext()) {
            String nome = iterator.next();
            System.out.println(nome);
        }
    }
}

```

### Quando Usar o Padrão Iterator

- **Acesso Sequencial**: Quando você precisa de acesso sequencial aos elementos de uma coleção sem expor a estrutura interna da coleção.
- **Coleções Heterogêneas**: Quando você tem diferentes tipos de coleções e deseja fornecer uma interface uniforme para iterar sobre elas.
- **Abstração do Percorrimento**: Quando você deseja separar a lógica de iteração da lógica da coleção.

### Exemplos de Aplicação

1. **Estruturas de Dados**: Implementações de listas, conjuntos, árvores, e mapas que fornecem um meio de iterar sobre seus elementos.
2. **Parsing**: Ferramentas que precisam iterar sobre tokens em uma cadeia de caracteres.
3. **Coleções Personalizadas**: Implementações personalizadas de coleções que precisam fornecer uma interface de iteração.

### Vantagens do Iterator

- **Encapsulamento**: Encapsula os detalhes da iteração, proporcionando um acesso uniforme aos elementos da coleção.
- **Responsabilidade Única**: Segue o princípio da responsabilidade única ao separar as responsabilidades de iteração e de coleção.
- **Flexibilidade**: Permite a iteração sobre diferentes tipos de coleções de maneira uniforme.

### Desvantagens do Iterator

- **Sobrecarga**: Pode introduzir uma leve sobrecarga devido à criação de objetos adicionais para a iteração.
- **Complexidade Adicional**: Para coleções muito simples, o uso de um iterator pode adicionar complexidade desnecessária.

### Conclusão

O padrão Iterator é uma solução eficaz para situações onde é necessário percorrer coleções de maneira sequencial sem expor a representação interna das coleções. Ele promove o encapsulamento e a separação de responsabilidades, fornecendo uma interface uniforme para diferentes tipos de coleções.
# Template Method

O padrão de projeto Template Method é um padrão comportamental que define o esqueleto de um algoritmo em uma operação, postergando a definição de alguns passos para as subclasses. O Template Method permite que subclasses redefinam certos passos de um algoritmo sem mudar a estrutura do próprio algoritmo.

### Estrutura do Template Method

1. **Abstract Class (Classe Abstrata)**: Define o método template que contém o esqueleto do algoritmo. Este método chama operações primitivas (alguns dos passos do algoritmo) que devem ser implementadas pelas subclasses.
2. **Concrete Class (Classe Concreta)**: Implementa as operações primitivas para completar os passos do algoritmo definidos na classe abstrata.

### Exemplo em Java

Vamos considerar um exemplo onde temos diferentes tipos de preparação de bebidas (chá e café), mas o processo de preparação segue um esqueleto comum.

### Abstract Class

```java
public abstract class Bebida {
    // Template Method
    public final void prepararReceita() {
        ferverAgua();
        adicionarIngredientePrincipal();
        despejarNoCopo();
        if (clienteQuerCondimento()) {
            adicionarCondimentos();
        }
    }

    protected abstract void adicionarIngredientePrincipal();
    protected abstract void adicionarCondimentos();

    private void ferverAgua() {
        System.out.println("Fervendo água");
    }

    private void despejarNoCopo() {
        System.out.println("Despejando no copo");
    }

    // Hook Method
    protected boolean clienteQuerCondimento() {
        return true;
    }
}

```

### Concrete Classes

```java
public class Cha extends Bebida {
    @Override
    protected void adicionarIngredientePrincipal() {
        System.out.println("Adicionando o chá");
    }

    @Override
    protected void adicionarCondimentos() {
        System.out.println("Adicionando limão");
    }
}

public class Cafe extends Bebida {
    @Override
    protected void adicionarIngredientePrincipal() {
        System.out.println("Adicionando o café");
    }

    @Override
    protected void adicionarCondimentos() {
        System.out.println("Adicionando açúcar e leite");
    }

    @Override
    protected boolean clienteQuerCondimento() {
        return false; // Suponha que o cliente não quer condimentos no café
    }
}

```

### Client

```java
public class Main {
    public static void main(String[] args) {
        Bebida cha = new Cha();
        Bebida cafe = new Cafe();

        System.out.println("Preparando chá...");
        cha.prepararReceita();

        System.out.println("\\nPreparando café...");
        cafe.prepararReceita();
    }
}

```

### Quando Usar o Padrão Template Method

- **Definir o Esqueleto de um Algoritmo**: Quando você deseja definir o esqueleto de um algoritmo e permitir que as subclasses implementem etapas específicas.
- **Passos Comuns em Algoritmos**: Quando diferentes algoritmos compartilham etapas comuns e você deseja evitar duplicação de código.
- **Comportamento Padrão com Personalização**: Quando você deseja fornecer um comportamento padrão que pode ser personalizado por subclasses.

### Exemplos de Aplicação

1. **Preparação de Bebidas**: Como mostrado no exemplo acima.
2. **Processamento de Dados**: Definindo um esqueleto para processamento de dados que pode ser personalizado para diferentes tipos de dados.
3. **Operações de Banco de Dados**: Especificando etapas comuns para operações de banco de dados, como conectar, executar uma consulta e fechar a conexão.
4. **Renderização de Documentos**: Definindo o esqueleto para renderização de documentos que pode ser especializado para diferentes tipos de documentos (HTML, PDF, etc.).

### Vantagens do Template Method

- **Reuso de Código**: Promove o reuso de código ao definir etapas comuns em um algoritmo e permitir a personalização apenas onde necessário.
- **Facilidade de Manutenção**: Facilita a manutenção ao centralizar a estrutura do algoritmo em uma classe abstrata.
- **Flexibilidade**: Permite que subclasses personalizem etapas específicas do algoritmo sem alterar sua estrutura.

### Desvantagens do Template Method

- **Restrições de Herança**: Requer que os desenvolvedores usem herança, o que pode ser uma limitação se a linguagem ou o design do sistema não favorecerem herança.
- **Aumento da Complexidade**: Pode aumentar a complexidade do sistema devido à necessidade de gerenciar várias classes e métodos.

### Conclusão

O padrão Template Method é uma solução eficaz para definir o esqueleto de um algoritmo e permitir que subclasses personalizem etapas específicas sem alterar a estrutura geral do algoritmo. Ele promove o reuso de código, facilita a manutenção e proporciona flexibilidade. No entanto, deve-se estar ciente das limitações relacionadas à herança e à complexidade adicional ao utilizar este padrão.
# Abstract Factory

O padrão de projeto Abstract Factory é um padrão criacional que fornece uma interface para criar famílias de objetos relacionados ou dependentes sem especificar suas classes concretas. Ele é útil quando o sistema deve ser independente de como seus produtos são criados, compostos e representados, e quando você precisa garantir que os produtos gerados sejam compatíveis entre si.

### Estrutura do Abstract Factory

1. **Abstract Factory**: Declara um conjunto de métodos para criar cada um dos produtos abstratos.
2. **Concrete Factory**: Implementa os métodos da Abstract Factory para criar produtos concretos.
3. **Abstract Product**: Declara uma interface para um tipo de produto objeto.
4. **Concrete Product**: Implementa a interface do produto abstrato.
5. **Client**: Usa apenas interfaces declaradas pela Abstract Factory e pelos produtos abstratos.

### Exemplo em Java

Vamos considerar um exemplo onde precisamos criar famílias de widgets para diferentes sistemas operacionais (Windows e Mac).

### Abstract Products

```java
public interface Botao {
    void desenhar();
}

public interface Janela {
    void abrir();
}

```

### Concrete Products

```java
public class BotaoWindows implements Botao {
    @Override
    public void desenhar() {
        System.out.println("Desenhando um botão no estilo Windows.");
    }
}

public class BotaoMac implements Botao {
    @Override
    public void desenhar() {
        System.out.println("Desenhando um botão no estilo Mac.");
    }
}

public class JanelaWindows implements Janela {
    @Override
    public void abrir() {
        System.out.println("Abrindo uma janela no estilo Windows.");
    }
}

public class JanelaMac implements Janela {
    @Override
    public void abrir() {
        System.out.println("Abrindo uma janela no estilo Mac.");
    }
}

```

### Abstract Factory

```java
public interface FabricaWidget {
    Botao criarBotao();
    Janela criarJanela();
}

```

### Concrete Factories

```java
public class FabricaWindows implements FabricaWidget {
    @Override
    public Botao criarBotao() {
        return new BotaoWindows();
    }

    @Override
    public Janela criarJanela() {
        return new JanelaWindows();
    }
}

public class FabricaMac implements FabricaWidget {
    @Override
    public Botao criarBotao() {
        return new BotaoMac();
    }

    @Override
    public Janela criarJanela() {
        return new JanelaMac();
    }
}

```

### Client

```java
public class Cliente {
    private Botao botao;
    private Janela janela;

    public Cliente(FabricaWidget fabrica) {
        botao = fabrica.criarBotao();
        janela = fabrica.criarJanela();
    }

    public void desenhar() {
        botao.desenhar();
        janela.abrir();
    }
}

```

### Utilização

```java
public class Main {
    public static void main(String[] args) {
        FabricaWidget fabrica = new FabricaWindows();
        Cliente cliente = new Cliente(fabrica);
        cliente.desenhar(); // Desenhando um botão no estilo Windows. Abrindo uma janela no estilo Windows.

        fabrica = new FabricaMac();
        cliente = new Cliente(fabrica);
        cliente.desenhar(); // Desenhando um botão no estilo Mac. Abrindo uma janela no estilo Mac.
    }
}

```

### Quando Usar o Padrão Abstract Factory

1. **Famílias de Objetos Relacionados**: Quando o sistema precisa criar famílias de objetos relacionados ou dependentes que devem ser utilizados juntos.
2. **Independência de Implementação**: Quando se deseja que o sistema seja independente de como os seus objetos são criados, compostos e representados.
3. **Troca de Famílias em Tempo de Execução**: Quando é necessário trocar entre diferentes famílias de produtos durante a execução do programa sem alterar o código que utiliza os produtos.

### Exemplos de Aplicação

- **Sistemas de Interface Gráfica**: Para criar famílias de widgets (botões, janelas, menus) que funcionam de forma consistente em diferentes sistemas operacionais (Windows, Mac, Linux).
- **Sistemas de Banco de Dados**: Para criar diferentes tipos de conexões de banco de dados (SQL, NoSQL) e seus respectivos comandos e transações.
- **Aplicações de Jogos**: Para criar diferentes famílias de objetos de jogo (personagens, inimigos, itens) que são específicos para diferentes níveis ou mundos do jogo.
- **Frameworks de Persistência**: Para criar diferentes estratégias de persistência (arquivos, bancos de dados, memória) de forma transparente para o código cliente.

### Vantagens do Abstract Factory

- **Coerência de Produto**: Garante que os produtos criados por uma fábrica concreta sejam compatíveis entre si.
- **Troca Fácil de Famílias de Produtos**: Facilita a troca de famílias de produtos, mudando apenas a fábrica concreta utilizada.
- **Princípio da Responsabilidade Única**: O código de criação de objetos é centralizado na fábrica.

### Desvantagens do Abstract Factory

- **Complexidade Adicional**: Adiciona complexidade ao código devido à necessidade de criar várias interfaces e classes.
- **Difícil Adição de Novos Produtos**: Adicionar um novo tipo de produto pode exigir a modificação de todas as fábricas concretas, o que pode ser trabalhoso.

### Conclusão

O padrão Abstract Factory é ideal para sistemas que necessitam criar famílias de objetos que funcionam bem juntos e devem ser intercambiáveis, fornecendo uma abordagem flexível e extensível para a criação de objetos.
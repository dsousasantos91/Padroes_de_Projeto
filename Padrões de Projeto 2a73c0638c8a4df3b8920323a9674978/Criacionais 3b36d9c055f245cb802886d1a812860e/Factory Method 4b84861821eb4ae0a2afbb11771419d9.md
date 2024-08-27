# Factory Method

O padrão de projeto Factory Method é um padrão criacional que permite a criação de objetos sem especificar a classe exata do objeto que será criado. Em vez de chamar o construtor de uma classe diretamente para criar um objeto, o padrão Factory Method utiliza um método específico para criar objetos, permitindo que as subclasses alterem o tipo de objetos que serão criados.

### Estrutura do Factory Method

1. **Produto (Product)**: Define a interface dos objetos que a fábrica (factory) vai criar.
2. **Produto Concreto (Concrete Product)**: Implementa a interface do Produto.
3. **Criador (Creator)**: Declara o método fábrica, que retorna um objeto do tipo Produto. Pode também definir uma implementação padrão desse método.
4. **Criador Concreto (Concrete Creator)**: Sobrescreve o método fábrica para retornar uma instância de um Produto Concreto.

### Exemplo em Java

Vamos considerar um exemplo onde precisamos criar diferentes tipos de documentos (Relatório e Carta).

### Interface Produto

```java
public interface Documento {
    void exibir();
}

```

### Produtos Concretos

```java
public class Relatorio implements Documento {
    @Override
    public void exibir() {
        System.out.println("Exibindo um Relatório.");
    }
}

public class Carta implements Documento {
    @Override
    public void exibir() {
        System.out.println("Exibindo uma Carta.");
    }
}

```

### Criador

```java
public abstract class CriadorDocumento {
    public abstract Documento criarDocumento();

    public void exibirDocumento() {
        Documento doc = criarDocumento();
        doc.exibir();
    }
}

```

### Criadores Concretos

```java
public class CriadorRelatorio extends CriadorDocumento {
    @Override
    public Documento criarDocumento() {
        return new Relatorio();
    }
}

public class CriadorCarta extends CriadorDocumento {
    @Override
    public Documento criarDocumento() {
        return new Carta();
    }
}

```

### Utilização

```java
public class Main {
    public static void main(String[] args) {
        CriadorDocumento criador = new CriadorRelatorio();
        criador.exibirDocumento(); // Exibindo um Relatório.

        criador = new CriadorCarta();
        criador.exibirDocumento(); // Exibindo uma Carta.
    }
}

```

### Quando Usar o Padrão Factory Method

O padrão Factory Method é útil em diversas situações, incluindo:

1. **Delegar a Criação de Objetos a Subclasses**: Quando a classe principal não deve conhecer as classes exatas que ela precisa instanciar. Ao invés de criar diretamente os objetos, ela delega essa responsabilidade às subclasses.
2. **Extensibilidade**: Quando espera-se que novas classes possam ser adicionadas ao sistema no futuro e você deseja que o código existente seja capaz de funcionar com essas novas classes sem precisar ser modificado.
3. **Redução de Acoplamento**: Quando se deseja reduzir o acoplamento entre o código que usa os objetos e as classes concretas dos objetos. Isso facilita a manutenção e a evolução do código.
4. **Controle Centralizado**: Quando deseja centralizar a lógica de criação de objetos, especialmente se essa lógica for complexa ou precisar ser reutilizada em várias partes do sistema.

### Exemplos de Aplicação

- **Frameworks de Interface Gráfica**: Onde diferentes tipos de botões, janelas e outros componentes podem ser criados conforme a necessidade.
- **Sistemas de Log**: Onde diferentes tipos de loggers (arquivo, console, rede) podem ser instanciados conforme a configuração.
- **Motores de Jogos**: Onde diferentes tipos de personagens, inimigos ou itens podem ser criados dependendo do nível ou cenário.

### Vantagens do Factory Method

- **Isolamento de código de criação**: O código cliente não precisa saber qual classe concreta está sendo instanciada.
- **Facilidade de extensão**: Novas classes de produto podem ser adicionadas sem modificar o código existente.
- **Princípio da Responsabilidade Única**: O código de criação de objetos é centralizado na fábrica.

### Desvantagens do Factory Method

- **Complexidade**: Pode adicionar complexidade adicional ao código devido à criação de várias subclasses para diferentes produtos.
- **Código Verboso**: A implementação de métodos de fábrica em várias classes pode tornar o código mais extenso.

### Conclusão

O padrão Factory Method fornece uma maneira flexível de criar objetos, permitindo que subclasses decidam qual classe concreta deve ser instanciada. Isso promove a extensibilidade e a manutenção do código, além de facilitar a adição de novos tipos de objetos sem alterar o código existente.
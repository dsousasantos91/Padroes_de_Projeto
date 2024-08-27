# Command

O padrão de projeto Command é um padrão comportamental que transforma uma solicitação em um objeto, permitindo que você parametrize clientes com diferentes solicitações, enfileire ou registre solicitações, e suporte operações que podem ser desfeitas. O padrão encapsula uma solicitação como um objeto, desta forma, permitindo que você parametrize outros objetos com diferentes solicitações, enfileire ou registre solicitações e suporte operações que podem ser desfeitas.

### Estrutura do Command

1. **Command**: Declara uma interface para executar uma operação.
2. **Concrete Command**: Implementa a interface Command, vinculando uma ação a um Receiver.
3. **Receiver**: Sabe como realizar as operações associadas à realização de uma solicitação.
4. **Invoker**: Solicita a execução da solicitação por meio do Command.
5. **Client**: Cria um objeto Concrete Command e define seu Receiver.

### Exemplo em Java

Vamos considerar um exemplo onde temos um sistema de controle remoto que pode ligar e desligar dispositivos como luzes e portas de garagem.

### Command Interface

```java
public interface Command {
    void executar();
}

```

### Concrete Command

```java
public class Luz {
    public void ligar() {
        System.out.println("A luz está ligada.");
    }

    public void desligar() {
        System.out.println("A luz está desligada.");
    }
}

public class PortaGaragem {
    public void abrir() {
        System.out.println("A porta da garagem está aberta.");
    }

    public void fechar() {
        System.out.println("A porta da garagem está fechada.");
    }
}

public class ComandoLigarLuz implements Command {
    private Luz luz;

    public ComandoLigarLuz(Luz luz) {
        this.luz = luz;
    }

    @Override
    public void executar() {
        luz.ligar();
    }
}

public class ComandoDesligarLuz implements Command {
    private Luz luz;

    public ComandoDesligarLuz(Luz luz) {
        this.luz = luz;
    }

    @Override
    public void executar() {
        luz.desligar();
    }
}

public class ComandoAbrirPortaGaragem implements Command {
    private PortaGaragem portaGaragem;

    public ComandoAbrirPortaGaragem(PortaGaragem portaGaragem) {
        this.portaGaragem = portaGaragem;
    }

    @Override
    public void executar() {
        portaGaragem.abrir();
    }
}

public class ComandoFecharPortaGaragem implements Command {
    private PortaGaragem portaGaragem;

    public ComandoFecharPortaGaragem(PortaGaragem portaGaragem) {
        this.portaGaragem = portaGaragem;
    }

    @Override
    public void executar() {
        portaGaragem.fechar();
    }
}

```

### Invoker

```java
public class ControleRemoto {
    private Command comando;

    public void definirComando(Command comando) {
        this.comando = comando;
    }

    public void pressionarBotao() {
        comando.executar();
    }
}

```

### Client

```java
public class Main {
    public static void main(String[] args) {
        ControleRemoto controleRemoto = new ControleRemoto();

        Luz luz = new Luz();
        PortaGaragem portaGaragem = new PortaGaragem();

        Command ligarLuz = new ComandoLigarLuz(luz);
        Command desligarLuz = new ComandoDesligarLuz(luz);
        Command abrirPortaGaragem = new ComandoAbrirPortaGaragem(portaGaragem);
        Command fecharPortaGaragem = new ComandoFecharPortaGaragem(portaGaragem);

        controleRemoto.definirComando(ligarLuz);
        controleRemoto.pressionarBotao(); // A luz está ligada.

        controleRemoto.definirComando(desligarLuz);
        controleRemoto.pressionarBotao(); // A luz está desligada.

        controleRemoto.definirComando(abrirPortaGaragem);
        controleRemoto.pressionarBotao(); // A porta da garagem está aberta.

        controleRemoto.definirComando(fecharPortaGaragem);
        controleRemoto.pressionarBotao(); // A porta da garagem está fechada.
    }
}

```

### Quando Usar o Padrão Command

- **Solicitações Parametrizáveis**: Quando você precisa parametrizar objetos com diferentes solicitações.
- **Fila de Operações**: Quando você deseja enfileirar operações ou registrar solicitações.
- **Operações Desfazíveis**: Quando você precisa suportar operações que podem ser desfeitas.
- **Desacoplamento**: Quando você deseja desacoplar o objeto que invoca a operação do objeto que sabe como executá-la.

### Exemplos de Aplicação

1. **Sistemas de Interface Gráfica**: Para implementar funcionalidades de desfazer/refazer operações.
2. **Sistemas de Automação**: Controle de dispositivos em uma casa inteligente.
3. **Filas de Tarefas**: Enfileirar e executar tarefas em ordem específica.
4. **Controle Remoto**: Sistemas de controle remoto para eletrônicos.

### Vantagens do Command

- **Desacoplamento**: Desacopla o objeto que invoca a operação do objeto que sabe como executá-la.
- **Extensibilidade**: Novos comandos podem ser adicionados facilmente sem alterar o código existente.
- **Suporte a Desfazer/Refazer**: Facilita a implementação de operações desfazíveis e refazíveis.
- **Histórico de Comandos**: Possibilidade de armazenar um histórico de comandos executados.

### Desvantagens do Command

- **Complexidade Adicional**: Adiciona complexidade ao código devido à necessidade de criar muitas classes de comando.
- **Sobrecarga de Memória**: Pode consumir mais memória devido ao armazenamento de instâncias de comandos, especialmente se mantiver um histórico.

### Conclusão

O padrão Command é uma solução eficaz para situações onde é necessário encapsular solicitações como objetos, promovendo o desacoplamento entre emissores e receptores de solicitações. Ele oferece flexibilidade e extensibilidade, permitindo a parametrização de solicitações, suporte a operações desfazíveis e o gerenciamento de filas de operações.
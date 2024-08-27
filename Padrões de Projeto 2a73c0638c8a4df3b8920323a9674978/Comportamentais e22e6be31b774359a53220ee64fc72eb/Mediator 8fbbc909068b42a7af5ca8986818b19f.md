# Mediator

O padrão de projeto Mediator é um padrão comportamental que define um objeto que encapsula a forma como um conjunto de objetos interage. Ele promove o desacoplamento ao evitar que objetos se refiram explicitamente uns aos outros e permite variar suas interações independentemente.

### Estrutura do Mediator

1. **Mediator**: Declara uma interface para a comunicação com objetos colegas (colleagues).
2. **Concrete Mediator**: Implementa a interface Mediator e coordena a comunicação entre objetos colegas.
3. **Colleague**: Cada objeto que se comunica através do Mediator.
4. **Concrete Colleague**: Implementa a comunicação com outros colegas através do Mediator.

### Exemplo em Java

Vamos considerar um exemplo de um sistema de chat onde diversos usuários (colegas) podem enviar mensagens uns aos outros através de um mediador.

### Mediator Interface

```java
public interface ChatMediator {
    void enviarMensagem(String mensagem, Usuario usuario);
    void adicionarUsuario(Usuario usuario);
}

```

### Concrete Mediator

```java
import java.util.ArrayList;
import java.util.List;

public class ChatMediatorConcreto implements ChatMediator {
    private List<Usuario> usuarios;

    public ChatMediatorConcreto() {
        this.usuarios = new ArrayList<>();
    }

    @Override
    public void enviarMensagem(String mensagem, Usuario usuario) {
        for (Usuario u : usuarios) {
            // Não envia a mensagem para o próprio usuário que a enviou
            if (u != usuario) {
                u.receber(mensagem);
            }
        }
    }

    @Override
    public void adicionarUsuario(Usuario usuario) {
        this.usuarios.add(usuario);
    }
}

```

### Colleague

```java
public abstract class Usuario {
    protected ChatMediator mediator;
    protected String nome;

    public Usuario(ChatMediator mediator, String nome) {
        this.mediator = mediator;
        this.nome = nome;
    }

    public abstract void enviar(String mensagem);
    public abstract void receber(String mensagem);
}

```

### Concrete Colleague

```java
public class UsuarioConcreto extends Usuario {
    public UsuarioConcreto(ChatMediator mediator, String nome) {
        super(mediator, nome);
    }

    @Override
    public void enviar(String mensagem) {
        System.out.println(this.nome + ": Enviando mensagem = " + mensagem);
        mediator.enviarMensagem(mensagem, this);
    }

    @Override
    public void receber(String mensagem) {
        System.out.println(this.nome + ": Recebendo mensagem = " + mensagem);
    }
}

```

### Client

```java
public class Main {
    public static void main(String[] args) {
        ChatMediator mediator = new ChatMediatorConcreto();

        Usuario user1 = new UsuarioConcreto(mediator, "Alice");
        Usuario user2 = new UsuarioConcreto(mediator, "Bob");
        Usuario user3 = new UsuarioConcreto(mediator, "Charlie");
        Usuario user4 = new UsuarioConcreto(mediator, "Diana");

        mediator.adicionarUsuario(user1);
        mediator.adicionarUsuario(user2);
        mediator.adicionarUsuario(user3);
        mediator.adicionarUsuario(user4);

        user1.enviar("Olá a todos!");
        // Output:
        // Alice: Enviando mensagem = Olá a todos!
        // Bob: Recebendo mensagem = Olá a todos!
        // Charlie: Recebendo mensagem = Olá a todos!
        // Diana: Recebendo mensagem = Olá a todos!
    }
}

```

### Quando Usar o Padrão Mediator

- **Comunicação Complexa**: Quando há uma rede complexa de comunicação entre muitos objetos.
- **Desacoplamento**: Quando você quer reduzir o acoplamento direto entre objetos.
- **Centralização de Controle**: Quando é útil centralizar o controle de interações complexas em um único ponto.

### Exemplos de Aplicação

1. **Sistemas de Chat**: Para gerenciar a comunicação entre vários usuários.
2. **Controle de Tráfego Aéreo**: Para gerenciar a comunicação entre diferentes aeronaves e a torre de controle.
3. **Interfaces Gráficas**: Para centralizar a lógica de interação entre vários componentes de interface do usuário.

### Vantagens do Mediator

- **Desacoplamento**: Reduz o acoplamento direto entre os colegas, promovendo um design mais modular e flexível.
- **Centralização**: Centraliza a lógica de comunicação, facilitando a manutenção e evolução.
- **Facilidade de Manutenção**: Mudanças na comunicação entre objetos requerem mudanças apenas no Mediator.

### Desvantagens do Mediator

- **Complexidade do Mediator**: Pode levar a um Mediator "inchado" com muita lógica, tornando-o complexo e difícil de manter.
- **Dependência Centralizada**: Pode introduzir uma dependência centralizada que, se não for bem gerenciada, pode afetar o desempenho e a escalabilidade.

### Conclusão

O padrão Mediator é uma solução eficaz para reduzir o acoplamento entre objetos e centralizar a lógica de comunicação. Ele é especialmente útil em sistemas complexos onde a comunicação entre muitos objetos precisa ser bem gerenciada e controlada. No entanto, deve-se tomar cuidado para não sobrecarregar o Mediator com muita lógica, o que poderia tornar o sistema difícil de manter e escalar.
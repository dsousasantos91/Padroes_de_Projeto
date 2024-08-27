# Decorator

O padrão de projeto Decorator é um padrão estrutural que permite que comportamentos sejam adicionados a objetos individuais, de maneira dinâmica, sem afetar o comportamento de outros objetos da mesma classe. Ele envolve a criação de um conjunto de classes "wrapper" que são usadas para envolver objetos originais.

### Estrutura do Decorator

1. **Component**: Define a interface para os objetos que podem ter responsabilidades adicionais.
2. **ConcreteComponent**: Implementa o Component, representando o objeto original ao qual responsabilidades adicionais podem ser anexadas.
3. **Decorator**: Mantém uma referência a um objeto Component e define uma interface que segue a interface do Component.
4. **ConcreteDecorator**: Adiciona responsabilidades ao objeto Component.

### Exemplo em Java

Vamos considerar um exemplo onde temos uma interface de Notificador que pode ser decorada com diferentes tipos de notificações (como SMS, Email).

### Component

```java
public interface Notificador {
    void enviar(String mensagem);
}

```

### ConcreteComponent

```java
public class NotificadorBasico implements Notificador {
    @Override
    public void enviar(String mensagem) {
        System.out.println("Notificação: " + mensagem);
    }
}

```

### Decorator

```java
public abstract class NotificadorDecorator implements Notificador {
    protected Notificador notificador;

    public NotificadorDecorator(Notificador notificador) {
        this.notificador = notificador;
    }

    @Override
    public void enviar(String mensagem) {
        notificador.enviar(mensagem);
    }
}

```

### ConcreteDecorator

```java
public class NotificadorEmail extends NotificadorDecorator {
    public NotificadorEmail(Notificador notificador) {
        super(notificador);
    }

    @Override
    public void enviar(String mensagem) {
        super.enviar(mensagem);
        enviarEmail(mensagem);
    }

    private void enviarEmail(String mensagem) {
        System.out.println("Enviando Email: " + mensagem);
    }
}

public class NotificadorSMS extends NotificadorDecorator {
    public NotificadorSMS(Notificador notificador) {
        super(notificador);
    }

    @Override
    public void enviar(String mensagem) {
        super.enviar(mensagem);
        enviarSMS(mensagem);
    }

    private void enviarSMS(String mensagem) {
        System.out.println("Enviando SMS: " + mensagem);
    }
}

```

### Client

```java
public class Main {
    public static void main(String[] args) {
        Notificador notificador = new NotificadorBasico();

        Notificador notificadorEmail = new NotificadorEmail(notificador);
        Notificador notificadorSMS = new NotificadorSMS(notificadorEmail);

        notificadorSMS.enviar("Olá, este é um teste de notificação.");
        // Output:
        // Notificação: Olá, este é um teste de notificação.
        // Enviando Email: Olá, este é um teste de notificação.
        // Enviando SMS: Olá, este é um teste de notificação.
    }
}

```

### Quando Usar o Padrão Decorator

- **Adicionar Comportamento de Forma Dinâmica**: Quando você precisa adicionar comportamento a objetos individuais de maneira dinâmica e flexível.
- **Evitar Subclasse**: Quando a criação de subclasses para estender funcionalidades não é prática ou possível.
- **Combinação de Comportamentos**: Quando você precisa combinar vários comportamentos de maneira flexível.

### Exemplos de Aplicação

1. **Sistemas de Notificação**: Adicionar diferentes tipos de notificações (SMS, Email, Push) dinamicamente a um sistema de notificação.
2. **Interfaces Gráficas**: Adicionar funcionalidades extras a componentes gráficos (scrollbars, bordas, etc.) sem alterar a classe original.
3. **Stream de I/O**: A API de Streams de Java é um exemplo clássico de uso do padrão Decorator, onde diferentes funcionalidades (buffered, data, object) são adicionadas a streams básicas.
4. **Controle de Acesso**: Adicionar verificações de acesso ou autenticação a objetos sem modificar o código original.

### Vantagens do Decorator

- **Flexibilidade**: Adiciona comportamento aos objetos de forma flexível e dinâmica.
- **Responsabilidade Única**: Segue o princípio da responsabilidade única, pois cada classe tem uma única função.
- **Combinação de Comportamentos**: Permite a combinação de múltiplos comportamentos sem criar uma hierarquia de classes complexa.

### Desvantagens do Decorator

- **Muitos Objetos Pequenos**: Pode resultar na criação de muitas pequenas classes, o que pode aumentar a complexidade do sistema.
- **Depuração Difícil**: Pode tornar a depuração mais difícil devido à grande quantidade de objetos envolvidos e ao encadeamento de chamadas.

### Conclusão

O padrão Decorator é uma solução eficaz para adicionar comportamentos a objetos de maneira flexível e dinâmica. Ele é especialmente útil quando você precisa evitar a proliferação de subclasses e deseja combinar múltiplos comportamentos de maneira modular.
# Chain of Responsibility

O padrão de projeto Chain of Responsibility é um padrão comportamental que permite que um pedido seja passado por uma corrente de manipuladores, onde cada manipulador decide processar o pedido ou passá-lo adiante para o próximo manipulador na corrente. Esse padrão promove o desacoplamento entre os emissores e os receptores do pedido, permitindo a definição de uma corrente de objetos que pode ser alterada dinamicamente.

### Estrutura do Chain of Responsibility

1. **Handler**: Declara uma interface comum para os manipuladores da corrente, incluindo um método para definir o próximo manipulador e um método para processar o pedido.
2. **Concrete Handler**: Implementa o método de processamento do pedido e define o comportamento para passar o pedido adiante para o próximo manipulador na corrente.
3. **Client**: Inicia o pedido e o passa para o primeiro manipulador na corrente.

### Exemplo em Java

Vamos considerar um exemplo de um sistema de suporte ao cliente onde diferentes níveis de suporte (Atendimento Básico, Suporte Técnico e Suporte Avançado) podem processar um pedido de suporte.

### Handler

```java
public abstract class Suporte {
    protected Suporte proximoNivel;

    public void definirProximoNivel(Suporte proximoNivel) {
        this.proximoNivel = proximoNivel;
    }

    public abstract void processarPedido(String pedido);
}

```

### Concrete Handler

```java
public class AtendimentoBasico extends Suporte {
    @Override
    public void processarPedido(String pedido) {
        if (pedido.equals("Básico")) {
            System.out.println("Atendimento Básico: Processando pedido " + pedido);
        } else if (proximoNivel != null) {
            proximoNivel.processarPedido(pedido);
        }
    }
}

public class SuporteTecnico extends Suporte {
    @Override
    public void processarPedido(String pedido) {
        if (pedido.equals("Técnico")) {
            System.out.println("Suporte Técnico: Processando pedido " + pedido);
        } else if (proximoNivel != null) {
            proximoNivel.processarPedido(pedido);
        }
    }
}

public class SuporteAvancado extends Suporte {
    @Override
    public void processarPedido(String pedido) {
        if (pedido.equals("Avançado")) {
            System.out.println("Suporte Avançado: Processando pedido " + pedido);
        } else if (proximoNivel != null) {
            proximoNivel.processarPedido(pedido);
        }
    }
}

```

### Client

```java
public class Main {
    public static void main(String[] args) {
        Suporte atendimentoBasico = new AtendimentoBasico();
        Suporte suporteTecnico = new SuporteTecnico();
        Suporte suporteAvancado = new SuporteAvancado();

        atendimentoBasico.definirProximoNivel(suporteTecnico);
        suporteTecnico.definirProximoNivel(suporteAvancado);

        // Processando diferentes tipos de pedidos
        atendimentoBasico.processarPedido("Básico");   // Atendimento Básico: Processando pedido Básico
        atendimentoBasico.processarPedido("Técnico");  // Suporte Técnico: Processando pedido Técnico
        atendimentoBasico.processarPedido("Avançado"); // Suporte Avançado: Processando pedido Avançado
        atendimentoBasico.processarPedido("Desconhecido"); // Nenhum suporte disponível para pedido Desconhecido
    }
}

```

### Quando Usar o Padrão Chain of Responsibility

- **Várias Maneiras de Processar um Pedido**: Quando há várias maneiras de processar um pedido e você quer que o pedido passe por uma cadeia de objetos até ser processado.
- **Desacoplamento entre Emissor e Receptor**: Quando você deseja desacoplar o emissor do pedido dos seus receptores.
- **Filtragem e Manipulação Condicional**: Quando você precisa de uma maneira flexível para filtrar e manipular pedidos de forma condicional.

### Exemplos de Aplicação

1. **Sistemas de Suporte ao Cliente**: Diferentes níveis de suporte ao cliente processando pedidos conforme a complexidade.
2. **Processamento de Eventos**: Sistemas onde eventos são processados por uma cadeia de manipuladores de eventos.
3. **Autorização**: Sistemas de controle de acesso onde diferentes manipuladores verificam permissões e autorizam ações.
4. **Filtros de Requisições Web**: Cadeia de filtros de requisições em servidores web para autenticação, autorização, logging, etc.

### Vantagens do Chain of Responsibility

- **Desacoplamento**: Desacopla o emissor do pedido dos seus receptores.
- **Flexibilidade**: Permite que você adicione ou altere a cadeia de manipuladores de forma dinâmica.
- **Simplicidade**: Facilita a implementação de novos manipuladores sem modificar os existentes.

### Desvantagens do Chain of Responsibility

- **Nenhuma Garantia de Processamento**: Não há garantia de que o pedido será processado se nenhum manipulador na cadeia o fizer.
- **Depuração Difícil**: Pode ser difícil depurar e acompanhar o fluxo de processamento do pedido através da cadeia de manipuladores.

### Conclusão

O padrão Chain of Responsibility é uma solução eficaz para situações onde diferentes objetos podem processar um pedido de forma condicional, promovendo o desacoplamento e a flexibilidade. Ele é especialmente útil em sistemas complexos onde você precisa de uma maneira organizada e modular para tratar diferentes tipos de pedidos ou eventos.
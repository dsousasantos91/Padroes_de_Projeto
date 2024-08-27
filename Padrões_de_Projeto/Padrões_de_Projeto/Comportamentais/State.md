# State

O padrão de projeto State é um padrão comportamental que permite a um objeto alterar seu comportamento quando seu estado interno muda. O objeto parecerá ter mudado sua classe. Este padrão é particularmente útil para implementar máquinas de estados finitos, onde um objeto pode transitar entre diferentes estados e comportamentos associados a esses estados.

### Estrutura do State

1. **Context**: Mantém uma instância de um ConcreteState que define o estado atual.
2. **State**: Define uma interface para encapsular o comportamento associado a um estado particular do Context.
3. **ConcreteState**: Implementa o comportamento específico de um estado do Context.

### Exemplo em Java

Vamos considerar um exemplo de uma máquina de venda automática (vending machine) que pode estar em diferentes estados: Sem Moeda, Moeda Inserida, Produto Selecionado, e Produto Entregue.

### State Interface

```java
public interface Estado {
    void inserirMoeda();
    void ejetarMoeda();
    void selecionarProduto();
    void dispensarProduto();
}

```

### Concrete States

```java
public class SemMoeda implements Estado {
    private MaquinaVenda maquina;

    public SemMoeda(MaquinaVenda maquina) {
        this.maquina = maquina;
    }

    @Override
    public void inserirMoeda() {
        System.out.println("Moeda inserida.");
        maquina.setEstado(maquina.getEstadoMoedaInserida());
    }

    @Override
    public void ejetarMoeda() {
        System.out.println("Nenhuma moeda para ejetar.");
    }

    @Override
    public void selecionarProduto() {
        System.out.println("Insira uma moeda primeiro.");
    }

    @Override
    public void dispensarProduto() {
        System.out.println("Insira uma moeda primeiro.");
    }
}

public class MoedaInserida implements Estado {
    private MaquinaVenda maquina;

    public MoedaInserida(MaquinaVenda maquina) {
        this.maquina = maquina;
    }

    @Override
    public void inserirMoeda() {
        System.out.println("Moeda já inserida.");
    }

    @Override
    public void ejetarMoeda() {
        System.out.println("Moeda ejetada.");
        maquina.setEstado(maquina.getEstadoSemMoeda());
    }

    @Override
    public void selecionarProduto() {
        System.out.println("Produto selecionado.");
        maquina.setEstado(maquina.getEstadoProdutoSelecionado());
    }

    @Override
    public void dispensarProduto() {
        System.out.println("Selecione um produto primeiro.");
    }
}

public class ProdutoSelecionado implements Estado {
    private MaquinaVenda maquina;

    public ProdutoSelecionado(MaquinaVenda maquina) {
        this.maquina = maquina;
    }

    @Override
    public void inserirMoeda() {
        System.out.println("Produto já selecionado.");
    }

    @Override
    public void ejetarMoeda() {
        System.out.println("Produto já selecionado, não pode ejetar moeda.");
    }

    @Override
    public void selecionarProduto() {
        System.out.println("Produto já selecionado.");
    }

    @Override
    public void dispensarProduto() {
        System.out.println("Produto dispensado.");
        maquina.setEstado(maquina.getEstadoSemMoeda());
    }
}

```

### Context

```java
public class MaquinaVenda {
    private Estado estadoSemMoeda;
    private Estado estadoMoedaInserida;
    private Estado estadoProdutoSelecionado;

    private Estado estadoAtual;

    public MaquinaVenda() {
        estadoSemMoeda = new SemMoeda(this);
        estadoMoedaInserida = new MoedaInserida(this);
        estadoProdutoSelecionado = new ProdutoSelecionado(this);

        estadoAtual = estadoSemMoeda;
    }

    public void setEstado(Estado estado) {
        estadoAtual = estado;
    }

    public void inserirMoeda() {
        estadoAtual.inserirMoeda();
    }

    public void ejetarMoeda() {
        estadoAtual.ejetarMoeda();
    }

    public void selecionarProduto() {
        estadoAtual.selecionarProduto();
    }

    public void dispensarProduto() {
        estadoAtual.dispensarProduto();
    }

    public Estado getEstadoSemMoeda() {
        return estadoSemMoeda;
    }

    public Estado getEstadoMoedaInserida() {
        return estadoMoedaInserida;
    }

    public Estado getEstadoProdutoSelecionado() {
        return estadoProdutoSelecionado;
    }
}

```

### Client

```java
public class Main {
    public static void main(String[] args) {
        MaquinaVenda maquina = new MaquinaVenda();

        maquina.inserirMoeda();
        maquina.selecionarProduto();
        maquina.dispensarProduto();

        maquina.inserirMoeda();
        maquina.ejetarMoeda();
    }
}

```

### Quando Usar o Padrão State

- **Máquinas de Estados Finitos**: Quando o comportamento de um objeto muda com base em seu estado e você deseja implementar uma máquina de estados finitos.
- **Código Complexo de Condicional**: Quando você tem muitos condicionais que dependem do estado de um objeto.
- **Desacoplamento de Estados**: Quando você deseja desacoplar a lógica de estado da lógica de negócios.

### Exemplos de Aplicação

1. **Máquinas de Venda Automática**: Como no exemplo acima.
2. **Processos de Workflow**: Para gerenciar diferentes estados em processos de negócios.
3. **Jogos**: Para gerenciar estados de jogo, como "Início", "Pausa", "Fim de Jogo".
4. **Interfaces de Usuário**: Para gerenciar diferentes estados de um componente de interface.

### Vantagens do State

- **Desacoplamento**: Desacopla o código de estado da lógica de negócios.
- **Extensibilidade**: Facilita a adição de novos estados sem modificar muito o código existente.
- **Organização**: Organiza o código de maneira mais clara e compreensível, evitando longos blocos condicionais.

### Desvantagens do State

- **Complexidade**: Pode introduzir complexidade adicional ao código devido à criação de muitas classes de estado.
- **Sobrecarga de Objetos**: Pode resultar em muitos pequenos objetos, aumentando a sobrecarga de memória.

### Conclusão

O padrão State é uma solução eficaz para situações onde o comportamento de um objeto deve mudar com base em seu estado interno. Ele promove o desacoplamento e a organização do código, tornando mais fácil a manutenção e extensão do sistema. No entanto, deve-se considerar a complexidade adicional e a potencial sobrecarga de memória ao utilizar este padrão.
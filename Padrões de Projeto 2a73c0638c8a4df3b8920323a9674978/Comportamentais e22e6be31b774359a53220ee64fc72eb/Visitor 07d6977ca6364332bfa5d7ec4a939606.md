# Visitor

O padrão de projeto Visitor é um padrão comportamental que permite que você adicione novas operações a uma estrutura de objeto existente sem alterar suas classes. O padrão Visitor é útil quando você precisa executar operações em uma estrutura de objeto que consiste em várias classes diferentes e quer evitar o uso de muitos métodos if/else ou switch/case.

### Estrutura do Visitor

1. **Visitor**: Declara uma interface para visitar elementos da estrutura de objeto.
2. **Concrete Visitor**: Implementa operações específicas que serão executadas nos elementos da estrutura de objeto.
3. **Element**: Declara uma interface para aceitar visitantes. Esse método deve chamar o método de visita apropriado no objeto Visitor.
4. **Concrete Element**: Implementa o método accept, que chama o método de visita apropriado no objeto Visitor.
5. **Object Structure**: Uma coleção de elementos que podem ser visitados.

### Exemplo em Java

Vamos considerar um exemplo onde temos uma estrutura de objeto representando diferentes partes de um computador (CPU, Disco, e Memória) e queremos calcular o custo total do computador.

### Visitor Interface

```java
public interface ComputadorVisitor {
    void visitar(CPU cpu);
    void visitar(Disco disco);
    void visitar(Memoria memoria);
}

```

### Concrete Visitor

```java
public class ComputadorCustoVisitor implements ComputadorVisitor {
    private double custoTotal = 0;

    @Override
    public void visitar(CPU cpu) {
        custoTotal += cpu.getPreco();
    }

    @Override
    public void visitar(Disco disco) {
        custoTotal += disco.getPreco();
    }

    @Override
    public void visitar(Memoria memoria) {
        custoTotal += memoria.getPreco();
    }

    public double getCustoTotal() {
        return custoTotal;
    }
}

```

### Element Interface

```java
public interface ComputadorParte {
    void aceitar(ComputadorVisitor visitor);
}

```

### Concrete Elements

```java
public class CPU implements ComputadorParte {
    private double preco;

    public CPU(double preco) {
        this.preco = preco;
    }

    public double getPreco() {
        return preco;
    }

    @Override
    public void aceitar(ComputadorVisitor visitor) {
        visitor.visitar(this);
    }
}

public class Disco implements ComputadorParte {
    private double preco;

    public Disco(double preco) {
        this.preco = preco;
    }

    public double getPreco() {
        return preco;
    }

    @Override
    public void aceitar(ComputadorVisitor visitor) {
        visitor.visitar(this);
    }
}

public class Memoria implements ComputadorParte {
    private double preco;

    public Memoria(double preco) {
        this.preco = preco;
    }

    public double getPreco() {
        return preco;
    }

    @Override
    public void aceitar(ComputadorVisitor visitor) {
        visitor.visitar(this);
    }
}

```

### Object Structure

```java
import java.util.ArrayList;
import java.util.List;

public class Computador {
    private List<ComputadorParte> partes;

    public Computador() {
        partes = new ArrayList<>();
        partes.add(new CPU(200));
        partes.add(new Disco(150));
        partes.add(new Memoria(100));
    }

    public void aceitar(ComputadorVisitor visitor) {
        for (ComputadorParte parte : partes) {
            parte.aceitar(visitor);
        }
    }
}

```

### Client

```java
public class Main {
    public static void main(String[] args) {
        Computador computador = new Computador();
        ComputadorCustoVisitor custoVisitor = new ComputadorCustoVisitor();

        computador.aceitar(custoVisitor);
        System.out.println("Custo total do computador: " + custoVisitor.getCustoTotal());
    }
}

```

### Quando Usar o Padrão Visitor

- **Operações em Estruturas Complexas**: Quando você precisa realizar operações em uma estrutura de objeto que contém muitas classes diferentes.
- **Adicionar Novas Operações**: Quando você precisa adicionar novas operações a essas classes sem alterar suas definições.
- **Evitar Condicionais Complexos**: Quando deseja evitar o uso de muitos condicionais (if/else ou switch/case) para determinar o tipo de classe em uma operação.

### Exemplos de Aplicação

1. **Compiladores**: Para realizar várias operações em uma árvore de sintaxe abstrata, como verificação de tipos, geração de código e otimização.
2. **Sistemas de Arquivos**: Para realizar operações como contagem de arquivos, cálculo de tamanhos e verificação de permissões em uma estrutura de diretórios.
3. **Gráficos**: Para realizar operações como renderização, redimensionamento e movimentação de elementos gráficos.

### Vantagens do Visitor

- **Adição de Operações**: Facilita a adição de novas operações sem alterar a estrutura da classe de elementos.
- **Separação de Responsabilidades**: Separa a lógica de operação da estrutura de dados, promovendo um design mais modular.
- **Redução de Condicionais**: Evita o uso de condicionais complexos para realizar operações específicas com base no tipo do objeto.

### Desvantagens do Visitor

- **Manutenção Difícil**: Adicionar uma nova classe de elementos requer a modificação de todas as classes Visitor existentes.
- **Quebra do Encapsulamento**: Pode forçar a exposição de detalhes internos dos elementos para o Visitor.

### Conclusão

O padrão Visitor é uma solução eficaz para adicionar novas operações a uma estrutura de objeto complexa sem alterar suas classes. Ele promove a separação de responsabilidades e a modularidade, facilitando a adição de novas operações. No entanto, deve-se estar atento à manutenção e à possível quebra de encapsulamento ao usar este padrão.
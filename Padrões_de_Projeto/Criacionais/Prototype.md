# Prototype

O padrão de projeto Prototype é um padrão criacional que permite a criação de novos objetos copiando uma instância existente, conhecida como protótipo. Ele é útil quando a criação direta de novos objetos é complexa ou custosa, ou quando é necessário garantir que os novos objetos sejam cópias exatas de um protótipo existente.

### Estrutura do Prototype

1. **Prototype**: Declara uma interface para clonar a si mesmo.
2. **Concrete Prototype**: Implementa a operação de clonagem.
3. **Client**: Cria um novo objeto solicitando ao protótipo que clone a si mesmo.

### Exemplo em Java

Vamos considerar um exemplo onde precisamos criar diferentes tipos de formas (círculo, retângulo) que podem ser clonadas.

### Interface Prototype

```java
public interface Forma extends Cloneable {
    Forma clonar();
    void desenhar();
}

```

### Concrete Prototypes

```java
public class Circulo implements Forma {
    private int raio;

    public Circulo(int raio) {
        this.raio = raio;
    }

    @Override
    public Forma clonar() {
        return new Circulo(this.raio);
    }

    @Override
    public void desenhar() {
        System.out.println("Desenhando um círculo com raio " + raio);
    }
}

public class Retangulo implements Forma {
    private int largura;
    private int altura;

    public Retangulo(int largura, int altura) {
        this.largura = largura;
        this.altura = altura;
    }

    @Override
    public Forma clonar() {
        return new Retangulo(this.largura, this.altura);
    }

    @Override
    public void desenhar() {
        System.out.println("Desenhando um retângulo com largura " + largura + " e altura " + altura);
    }
}

```

### Cliente

```java
public class Main {
    public static void main(String[] args) {
        Circulo circuloOriginal = new Circulo(5);
        Circulo circuloClonado = (Circulo) circuloOriginal.clonar();

        Retangulo retanguloOriginal = new Retangulo(10, 20);
        Retangulo retanguloClonado = (Retangulo) retanguloOriginal.clonar();

        circuloOriginal.desenhar(); // Desenhando um círculo com raio 5
        circuloClonado.desenhar(); // Desenhando um círculo com raio 5

        retanguloOriginal.desenhar(); // Desenhando um retângulo com largura 10 e altura 20
        retanguloClonado.desenhar(); // Desenhando um retângulo com largura 10 e altura 20
    }
}

```

### Quando Usar o Padrão Prototype

O padrão Prototype é útil em diversas situações, incluindo:

1. **Criação Custosa de Objetos**: Quando a criação de novos objetos é um processo caro e demorado, o padrão Prototype pode ser usado para criar novos objetos rapidamente, copiando um protótipo existente.
2. **Muitos Estados Possíveis**: Quando há muitas configurações possíveis para um objeto, criar um protótipo com a configuração desejada e cloná-lo pode ser mais simples e eficiente do que usar um construtor com muitos parâmetros.
3. **Redução de Subclasses**: Quando o sistema precisa criar diferentes instâncias de uma classe, o padrão Prototype pode ser uma alternativa ao uso de um grande número de subclasses. Em vez de criar subclasses para cada configuração possível, você pode criar protótipos e cloná-los.
4. **Manutenção de Estado**: Quando objetos precisam manter o estado, o padrão Prototype permite a criação de novos objetos que preservam o estado do protótipo.
5. **Composição Complexa de Objetos**: Quando um objeto é composto por muitos sub-objetos, clonar o objeto inteiro pode ser mais fácil do que recriar a composição a partir do zero.

### Exemplos de Aplicação

- **Editor de Gráficos**: Em aplicativos de edição gráfica, onde formas complexas e compostas são frequentemente duplicadas.
- **Jogos**: Para criar novos personagens ou itens com base em protótipos existentes.
- **Banco de Dados**: Para copiar registros de configuração ou templates de registros.

### Vantagens do Prototype

- **Cópia de Objetos Complexos**: Facilita a criação de novos objetos copiando um protótipo, o que pode ser mais eficiente do que criar novos objetos do zero.
- **Redução de Subclasses**: Pode reduzir a necessidade de criar subclasses apenas para especificar diferentes configurações ou estados iniciais.
- **Mudanças Dinâmicas**: Permite a adição ou remoção de objetos em tempo de execução, sem afetar a estrutura geral do sistema.

### Desvantagens do Prototype

- **Implementação Complexa de Clone**: A implementação correta do método de clonagem pode ser complexa, especialmente se os objetos tiverem referências a outros objetos.
- **Dependência do Construtor**: O padrão Prototype pode ser menos eficaz se o objeto a ser clonado depender de um estado que não pode ser facilmente duplicado.

### Conclusão

O padrão Prototype é especialmente útil quando a criação de novos objetos é custosa ou complexa, e quando se deseja criar novos objetos como cópias exatas de um protótipo existente, garantindo consistência e eficiência no processo de criação.
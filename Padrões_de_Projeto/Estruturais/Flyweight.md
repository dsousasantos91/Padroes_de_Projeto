# Flyweight

O padrão de projeto Flyweight é um padrão estrutural que visa minimizar o uso de memória compartilhando o máximo de dados possível com objetos similares. Ele é especialmente útil quando um grande número de objetos quase idênticos é usado de forma eficiente em termos de memória.

### Estrutura do Flyweight

1. **Flyweight**: Interface comum para todos os objetos flyweight.
2. **Concrete Flyweight**: Implementa a interface Flyweight e armazena o estado compartilhado.
3. **Flyweight Factory**: Cria e gerencia objetos flyweight. Garante que objetos compartilhados sejam reutilizados em vez de criados novamente.
4. **Client**: Mantém referências para objetos flyweight e calcula/armazenar o estado extrínseco.

### Conceitos de Estado Intrínseco e Extrínseco

- **Estado Intrínseco**: Parte do estado compartilhada por múltiplos objetos e armazenada no objeto flyweight.
- **Estado Extrínseco**: Parte do estado que varia entre os objetos e é armazenada ou calculada pelo cliente.

### Exemplo em Java

Vamos considerar um exemplo de um editor de texto que precisa renderizar muitos caracteres na tela. Utilizaremos o padrão Flyweight para compartilhar a representação de cada caractere.

### Flyweight Interface

```java
public interface CaractereFlyweight {
    void exibir(int tamanho, String cor);
}

```

### Concrete Flyweight

```java
public class CaractereConcreto implements CaractereFlyweight {
    private char simbolo;

    public CaractereConcreto(char simbolo) {
        this.simbolo = simbolo;
    }

    @Override
    public void exibir(int tamanho, String cor) {
        System.out.println("Caractere: " + simbolo + ", Tamanho: " + tamanho + ", Cor: " + cor);
    }
}

```

### Flyweight Factory

```java
import java.util.HashMap;
import java.util.Map;

public class FlyweightFactory {
    private Map<Character, CaractereFlyweight> flyweights = new HashMap<>();

    public CaractereFlyweight getFlyweight(char simbolo) {
        if (!flyweights.containsKey(simbolo)) {
            flyweights.put(simbolo, new CaractereConcreto(simbolo));
        }
        return flyweights.get(simbolo);
    }
}

```

### Client

```java
public class Main {
    public static void main(String[] args) {
        FlyweightFactory factory = new FlyweightFactory();

        CaractereFlyweight a = factory.getFlyweight('a');
        CaractereFlyweight b = factory.getFlyweight('b');
        CaractereFlyweight c = factory.getFlyweight('c');

        a.exibir(12, "vermelho");
        b.exibir(14, "verde");
        c.exibir(16, "azul");

        // Reutilização do objeto flyweight
        CaractereFlyweight a2 = factory.getFlyweight('a');
        a2.exibir(18, "preto");
    }
}

```

### Quando Usar o Padrão Flyweight

- **Muitos Objetos Semelhantes**: Quando há a necessidade de criar um grande número de objetos quase idênticos.
- **Uso Intensivo de Memória**: Quando os custos de memória são altos devido ao grande número de objetos.
- **Estado Compartilhado**: Quando é possível dividir o estado do objeto em partes compartilhadas (intrínseco) e específicas (extrínseco).

### Exemplos de Aplicação

1. **Editor de Texto**: Compartilhar representações de caracteres em um editor de texto.
2. **Sistema Gráfico**: Gerenciar muitos objetos gráficos semelhantes, como árvores em uma paisagem.
3. **Cache de Objetos**: Implementar caches onde objetos são frequentemente reutilizados.

### Vantagens do Flyweight

- **Economia de Memória**: Reduz o uso de memória compartilhando objetos.
- **Melhoria de Performance**: Pode melhorar a performance ao reduzir a sobrecarga de criação de muitos objetos semelhantes.
- **Reutilização de Objetos**: Facilita a reutilização de objetos, promovendo um design mais eficiente.

### Desvantagens do Flyweight

- **Complexidade Adicional**: Adiciona complexidade ao código devido à necessidade de gerenciar o estado intrínseco e extrínseco.
- **Calculo de Estado Extrínseco**: O cliente precisa gerenciar o estado extrínseco, o que pode aumentar a complexidade do código.

### Conclusão

O padrão Flyweight é uma solução eficaz para problemas onde um grande número de objetos semelhantes precisa ser gerenciado de maneira eficiente em termos de memória. Ele promove a reutilização e a economia de memória, embora adicione complexidade ao gerenciamento de estados compartilhados e específicos.
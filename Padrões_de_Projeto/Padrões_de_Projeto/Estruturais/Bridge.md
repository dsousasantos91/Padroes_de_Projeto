# Bridge

O padrão de projeto Bridge é um padrão estrutural que separa a abstração da implementação, permitindo que ambos possam variar independentemente. Ele é útil para evitar a explosão de subclasses ao criar diferentes combinações de abstrações e implementações.

### Estrutura do Bridge

1. **Abstraction**: Define a interface de alto nível que usa a implementação.
2. **Refined Abstraction**: Estende a interface de Abstraction.
3. **Implementor**: Define a interface para a implementação.
4. **Concrete Implementor**: Implementa a interface do Implementor.

### Exemplo em Java

Vamos considerar um exemplo onde temos diferentes formas (abstração) que podem ser desenhadas com diferentes cores (implementação).

### Implementor

```java
public interface Cor {
    void aplicarCor();
}

```

### Concrete Implementor

```java
public class Vermelho implements Cor {
    @Override
    public void aplicarCor() {
        System.out.println("Aplicando cor vermelha.");
    }
}

public class Azul implements Cor {
    @Override
    public void aplicarCor() {
        System.out.println("Aplicando cor azul.");
    }
}

```

### Abstraction

```java
public abstract class Forma {
    protected Cor cor;

    public Forma(Cor cor) {
        this.cor = cor;
    }

    abstract void desenhar();
}

```

### Refined Abstraction

```java
public class Circulo extends Forma {
    public Circulo(Cor cor) {
        super(cor);
    }

    @Override
    void desenhar() {
        System.out.print("Desenhando círculo. ");
        cor.aplicarCor();
    }
}

public class Quadrado extends Forma {
    public Quadrado(Cor cor) {
        super(cor);
    }

    @Override
    void desenhar() {
        System.out.print("Desenhando quadrado. ");
        cor.aplicarCor();
    }
}

```

### Client

```java
public class Main {
    public static void main(String[] args) {
        Forma circuloVermelho = new Circulo(new Vermelho());
        Forma quadradoAzul = new Quadrado(new Azul());

        circuloVermelho.desenhar(); // Desenhando círculo. Aplicando cor vermelha.
        quadradoAzul.desenhar();    // Desenhando quadrado. Aplicando cor azul.
    }
}

```

### Quando Usar o Padrão Bridge

- **Evitar Explosão de Subclasses**: Quando você precisa combinar diferentes abstrações com diferentes implementações, evitando a criação de um grande número de subclasses.
- **Mudar Implementações em Tempo de Execução**: Quando você quer trocar a implementação de uma abstração em tempo de execução.
- **Desenvolvimento Independente**: Quando você quer que a abstração e a implementação possam ser desenvolvidas e alteradas de forma independente.

### Exemplos de Aplicação

1. **Sistemas de Interface Gráfica**: Diferentes controles gráficos (botões, menus, etc.) podem ser desenhados com diferentes bibliotecas gráficas (OpenGL, DirectX, etc.).
2. **Dispositivos e Controladores**: Dispositivos (TVs, Rádios, etc.) podem ser controlados por diferentes controladores remotos.
3. **Aplicações de Impressão**: Documentos podem ser impressos em diferentes formatos (PDF, PostScript) usando diferentes bibliotecas de impressão.
4. **Persistência de Dados**: Objetos podem ser salvos em diferentes formatos (XML, JSON) usando diferentes implementações de persistência.

### Vantagens do Bridge

- **Separação de Abstração e Implementação**: Permite que a abstração e a implementação sejam desenvolvidas independentemente.
- **Flexibilidade**: Facilita a adição de novas abstrações e implementações sem modificar o código existente.
- **Redução da Explosão de Subclasses**: Evita a criação de um grande número de subclasses para combinar diferentes abstrações e implementações.

### Desvantagens do Bridge

- **Complexidade Adicional**: Adiciona complexidade ao código devido à separação da abstração e implementação.
- **Mais Código Boilerplate**: Pode resultar em mais classes e interfaces, aumentando a quantidade de código boilerplate.

### Conclusão

O padrão Bridge é uma solução eficaz para problemas onde a combinação de diferentes abstrações e implementações pode levar a uma explosão de subclasses. Ele promove a separação de preocupações, aumentando a flexibilidade e a capacidade de manutenção do sistema.
# Builder

O padrão de projeto Builder é um padrão criacional que permite a construção de objetos complexos passo a passo. Ele desacopla o processo de construção de um objeto de sua representação, permitindo que o mesmo processo de construção crie diferentes representações.

### Estrutura do Builder

1. **Builder**: Declara uma interface para criar partes dos objetos complexos.
2. **Concrete Builder**: Implementa a interface Builder e constrói partes específicas do objeto.
3. **Produto (Product)**: Representa o objeto complexo a ser construído.
4. **Director**: Constrói um objeto usando a interface Builder.

### Exemplo em Java

Vamos considerar um exemplo onde queremos construir diferentes tipos de casas (de madeira e de tijolos) com várias partes (fundação, estrutura, telhado, etc.).

### Produto

```java
public class Casa {
    private String fundacao;
    private String estrutura;
    private String telhado;
    private String interiores;

    public void setFundacao(String fundacao) {
        this.fundacao = fundacao;
    }

    public void setEstrutura(String estrutura) {
        this.estrutura = estrutura;
    }

    public void setTelhado(String telhado) {
        this.telhado = telhado;
    }

    public void setInteriores(String interiores) {
        this.interiores = interiores;
    }

    @Override
    public String toString() {
        return "Casa com " +
               "Fundação: " + fundacao + ", " +
               "Estrutura: " + estrutura + ", " +
               "Telhado: " + telhado + ", " +
               "Interiores: " + interiores;
    }
}

```

### Builder

```java
public interface CasaBuilder {
    void construirFundacao();
    void construirEstrutura();
    void construirTelhado();
    void construirInteriores();
    Casa getCasa();
}

```

### Concrete Builder

```java
public class CasaDeMadeiraBuilder implements CasaBuilder {
    private Casa casa;

    public CasaDeMadeiraBuilder() {
        this.casa = new Casa();
    }

    @Override
    public void construirFundacao() {
        casa.setFundacao("Fundação de madeira");
    }

    @Override
    public void construirEstrutura() {
        casa.setEstrutura("Estrutura de madeira");
    }

    @Override
    public void construirTelhado() {
        casa.setTelhado("Telhado de madeira");
    }

    @Override
    public void construirInteriores() {
        casa.setInteriores("Interiores de madeira");
    }

    @Override
    public Casa getCasa() {
        return casa;
    }
}

public class CasaDeTijolosBuilder implements CasaBuilder {
    private Casa casa;

    public CasaDeTijolosBuilder() {
        this.casa = new Casa();
    }

    @Override
    public void construirFundacao() {
        casa.setFundacao("Fundação de tijolos");
    }

    @Override
    public void construirEstrutura() {
        casa.setEstrutura("Estrutura de tijolos");
    }

    @Override
    public void construirTelhado() {
        casa.setTelhado("Telhado de telhas");
    }

    @Override
    public void construirInteriores() {
        casa.setInteriores("Interiores de tijolos");
    }

    @Override
    public Casa getCasa() {
        return casa;
    }
}

```

### Director

```java
public class Diretor {
    private CasaBuilder casaBuilder;

    public Diretor(CasaBuilder casaBuilder) {
        this.casaBuilder = casaBuilder;
    }

    public void construirCasa() {
        casaBuilder.construirFundacao();
        casaBuilder.construirEstrutura();
        casaBuilder.construirTelhado();
        casaBuilder.construirInteriores();
    }

    public Casa getCasa() {
        return casaBuilder.getCasa();
    }
}

```

### Utilização

```java
public class Main {
    public static void main(String[] args) {
        CasaBuilder casaDeMadeiraBuilder = new CasaDeMadeiraBuilder();
        Diretor diretor = new Diretor(casaDeMadeiraBuilder);
        diretor.construirCasa();
        Casa casaDeMadeira = diretor.getCasa();
        System.out.println(casaDeMadeira);

        CasaBuilder casaDeTijolosBuilder = new CasaDeTijolosBuilder();
        diretor = new Diretor(casaDeTijolosBuilder);
        diretor.construirCasa();
        Casa casaDeTijolos = diretor.getCasa();
        System.out.println(casaDeTijolos);
    }
}

```

### Quando Usar o Padrão Builder

1. **Construção de Objetos Complexos**: Quando a criação de um objeto envolve várias etapas e configurações.
2. **Muitos Parâmetros no Construtor**: Quando um construtor de classe tem muitos parâmetros, especialmente se alguns deles são opcionais.
3. **Representações Diferentes**: Quando você quer criar diferentes representações de um objeto complexo usando o mesmo processo de construção.
4. **Imutabilidade de Objetos**: Quando você quer construir objetos imutáveis de forma controlada.

### Exemplos de Aplicação

- **Construtores de Interfaces de Usuário**: Para criar janelas, diálogos e outros componentes de interface de usuário complexos passo a passo.
- **Construção de Documentos**: Para montar documentos complexos como PDFs ou relatórios que envolvem várias partes e seções.
- **Configuração de Objetos**: Para configurar objetos com várias opções e parâmetros, como configurações de conexão de rede ou inicialização de sistemas.
- **Jogos**: Para criar personagens ou níveis de jogo, onde cada personagem ou nível pode ser composto por múltiplos componentes (atributos, habilidades, inimigos, obstáculos).

### Vantagens do Builder

- **Construção passo a passo**: Permite a criação de objetos complexos passo a passo, controlando o processo de construção.
- **Separação de construção e representação**: O código de construção é separado do código de representação, facilitando a manutenção e extensão.
- **Facilidade de criação de diferentes representações**: O mesmo código de construção pode ser usado para criar diferentes representações do objeto.

### Desvantagens do Builder

- **Complexidade adicional**: Adiciona complexidade ao código devido à necessidade de várias interfaces e classes.
- **Mais código boilerplate**: Requer a criação de mais classes e métodos, resultando em mais código boilerplate.

### Conclusão

O padrão Builder é ideal para a construção de objetos complexos que requerem várias etapas de configuração, fornecendo flexibilidade e clareza no processo de construção.
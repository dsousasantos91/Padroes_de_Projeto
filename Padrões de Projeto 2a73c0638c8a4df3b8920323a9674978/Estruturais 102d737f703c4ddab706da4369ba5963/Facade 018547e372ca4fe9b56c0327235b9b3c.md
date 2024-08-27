# Facade

O padrão de projeto Facade é um padrão estrutural que fornece uma interface simplificada para um subsistema complexo. Ele define uma interface de alto nível que torna o subsistema mais fácil de usar, ocultando suas complexidades internas.

### Estrutura do Facade

1. **Facade**: Fornece uma interface simplificada para o subsistema.
2. **Subsistema**: Conjunto de classes e componentes que realizam o trabalho real. O subsistema não tem conhecimento do Facade e opera independentemente.

### Exemplo em Java

Vamos considerar um exemplo onde temos um subsistema complexo para um sistema de home theater, que inclui várias classes como Amplificador, DVDPlayer, Projetor, e Tela. Usaremos um Facade para simplificar o uso desse sistema.

### Classes do Subsistema

```java
public class Amplificador {
    public void ligar() {
        System.out.println("Amplificador ligado.");
    }
    public void desligar() {
        System.out.println("Amplificador desligado.");
    }
}

public class DVDPlayer {
    public void ligar() {
        System.out.println("DVD Player ligado.");
    }
    public void desligar() {
        System.out.println("DVD Player desligado.");
    }
    public void play(String filme) {
        System.out.println("Reproduzindo filme: " + filme);
    }
}

public class Projetor {
    public void ligar() {
        System.out.println("Projetor ligado.");
    }
    public void desligar() {
        System.out.println("Projetor desligado.");
    }
}

public class Tela {
    public void descer() {
        System.out.println("Tela abaixada.");
    }
    public void subir() {
        System.out.println("Tela levantada.");
    }
}

```

### Facade

```java
public class HomeTheaterFacade {
    private Amplificador amplificador;
    private DVDPlayer dvdPlayer;
    private Projetor projetor;
    private Tela tela;

    public HomeTheaterFacade(Amplificador amplificador, DVDPlayer dvdPlayer, Projetor projetor, Tela tela) {
        this.amplificador = amplificador;
        this.dvdPlayer = dvdPlayer;
        this.projetor = projetor;
        this.tela = tela;
    }

    public void assistirFilme(String filme) {
        System.out.println("Preparando para assistir ao filme...");
        tela.descer();
        projetor.ligar();
        amplificador.ligar();
        dvdPlayer.ligar();
        dvdPlayer.play(filme);
    }

    public void finalizarFilme() {
        System.out.println("Finalizando o filme...");
        dvdPlayer.desligar();
        amplificador.desligar();
        projetor.desligar();
        tela.subir();
    }
}

```

### Client

```java
public class Main {
    public static void main(String[] args) {
        Amplificador amplificador = new Amplificador();
        DVDPlayer dvdPlayer = new DVDPlayer();
        Projetor projetor = new Projetor();
        Tela tela = new Tela();

        HomeTheaterFacade homeTheater = new HomeTheaterFacade(amplificador, dvdPlayer, projetor, tela);

        homeTheater.assistirFilme("Vingadores: Ultimato");
        // Output:
        // Preparando para assistir ao filme...
        // Tela abaixada.
        // Projetor ligado.
        // Amplificador ligado.
        // DVD Player ligado.
        // Reproduzindo filme: Vingadores: Ultimato

        homeTheater.finalizarFilme();
        // Output:
        // Finalizando o filme...
        // DVD Player desligado.
        // Amplificador desligado.
        // Projetor desligado.
        // Tela levantada.
    }
}

```

### Quando Usar o Padrão Facade

- **Interface Simples para um Subsistema Complexo**: Quando você quer fornecer uma interface simples para um subsistema complexo.
- **Desacoplamento**: Quando você deseja desacoplar um cliente do subsistema complexo.
- **Manutenção e Evolução**: Quando você deseja facilitar a manutenção e evolução do subsistema, ocultando suas complexidades internas.

### Exemplos de Aplicação

1. **Sistemas de Biblioteca**: Fornecer uma interface simples para um subsistema de biblioteca complexa.
2. **Sistemas de Arquivo**: Criar uma interface simples para operações complexas de sistemas de arquivos.
3. **APIs de Serviços Web**: Simplificar o uso de APIs complexas de serviços web.
4. **Home Theater**: Simplificar a operação de um sistema de home theater, como no exemplo acima.

### Vantagens do Facade

- **Simplicidade**: Proporciona uma interface simples e fácil de usar para um subsistema complexo.
- **Desacoplamento**: Reduz o acoplamento entre o cliente e o subsistema, promovendo um design mais flexível e desacoplado.
- **Facilidade de Uso**: Facilita o uso do subsistema, especialmente para novos desenvolvedores ou clientes.

### Desvantagens do Facade

- **Ocultação de Funcionalidades**: Pode ocultar funcionalidades específicas do subsistema que podem ser necessárias para alguns clientes.
- **Sobrecarga Adicional**: Adiciona uma camada extra que pode introduzir sobrecarga, embora geralmente seja mínima.

### Conclusão

O padrão Facade é uma solução eficaz para fornecer uma interface simplificada para subsistemas complexos, promovendo a simplicidade e o desacoplamento. Ele é especialmente útil em sistemas grandes e complexos onde a facilidade de uso e a manutenção são prioridades.
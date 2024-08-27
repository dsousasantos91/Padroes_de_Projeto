# Observer

O padrão de projeto Observer é um padrão comportamental que define uma dependência um-para-muitos entre objetos, de maneira que quando um objeto muda de estado, todos os seus dependentes são notificados e atualizados automaticamente. Este padrão é particularmente útil para implementar sistemas de eventos e notificações.

### Estrutura do Observer

1. **Subject**: Mantém uma lista de dependentes (Observers) e notifica-os de quaisquer mudanças no seu estado.
2. **Observer**: Define uma interface para receber notificações de mudanças de estado do Subject.
3. **ConcreteSubject**: Estende o Subject e armazena o estado de interesse para os Observers. Quando o estado muda, ele notifica seus Observers.
4. **ConcreteObserver**: Implementa a interface Observer e mantém uma referência ao ConcreteSubject. Atualiza seu estado para manter-se consistente com o estado do Subject.

### Exemplo em Java

Vamos considerar um exemplo onde temos um canal de notícias (Subject) e diferentes usuários (Observers) que recebem atualizações quando há uma nova notícia.

### Subject

```java
import java.util.ArrayList;
import java.util.List;

public class CanalNoticias {
    private List<Observer> observers = new ArrayList<>();
    private String noticia;

    public void adicionarObserver(Observer observer) {
        observers.add(observer);
    }

    public void removerObserver(Observer observer) {
        observers.remove(observer);
    }

    public void notificarObservers() {
        for (Observer observer : observers) {
            observer.atualizar();
        }
    }

    public void novaNoticia(String noticia) {
        this.noticia = noticia;
        notificarObservers();
    }

    public String getNoticia() {
        return noticia;
    }
}

```

### Observer

```java
public interface Observer {
    void atualizar();
}

```

### ConcreteObserver

```java
public class Usuario implements Observer {
    private String nome;
    private CanalNoticias canal;

    public Usuario(String nome, CanalNoticias canal) {
        this.nome = nome;
        this.canal = canal;
        canal.adicionarObserver(this);
    }

    @Override
    public void atualizar() {
        System.out.println(nome + " recebeu a notícia: " + canal.getNoticia());
    }
}

```

### Client

```java
public class Main {
    public static void main(String[] args) {
        CanalNoticias canal = new CanalNoticias();

        Usuario usuario1 = new Usuario("Alice", canal);
        Usuario usuario2 = new Usuario("Bob", canal);
        Usuario usuario3 = new Usuario("Charlie", canal);

        canal.novaNoticia("Nova atualização disponível!");
        // Output:
        // Alice recebeu a notícia: Nova atualização disponível!
        // Bob recebeu a notícia: Nova atualização disponível!
        // Charlie recebeu a notícia: Nova atualização disponível!

        canal.novaNoticia("Segundo notícia importante!");
        // Output:
        // Alice recebeu a notícia: Segundo notícia importante!
        // Bob recebeu a notícia: Segundo notícia importante!
        // Charlie recebeu a notícia: Segundo notícia importante!
    }
}

```

### Quando Usar o Padrão Observer

- **Mudanças de Estado**: Quando um objeto deve ser capaz de notificar outros objetos sobre mudanças em seu estado.
- **Desacoplamento**: Quando você deseja um baixo acoplamento entre o objeto que muda de estado (Subject) e os objetos que são notificados sobre essas mudanças (Observers).
- **Eventos e Notificações**: Quando você precisa de um mecanismo para implementar eventos e notificações.

### Exemplos de Aplicação

1. **Interfaces Gráficas**: Para atualizar componentes da interface do usuário em resposta a eventos.
2. **Sistemas de Notificação**: Para implementar sistemas de notificação onde várias partes de um sistema precisam ser notificadas sobre eventos.
3. **Model-View-Controller (MVC)**: Em padrões arquiteturais como MVC, onde a visão (View) precisa ser atualizada quando o modelo (Model) muda.
4. **Monitoramento de Estado**: Para monitorar o estado de sistemas em tempo real, como sensores em uma rede.

### Vantagens do Observer

- **Desacoplamento**: Reduz o acoplamento entre o Subject e os Observers.
- **Flexibilidade**: Permite adicionar e remover Observers dinamicamente.
- **Reutilização**: Facilita a reutilização de Subjects e Observers independentes.

### Desvantagens do Observer

- **Complexidade**: Pode introduzir complexidade adicional ao código, especialmente quando a cadeia de notificações é longa.
- **Desempenho**: Pode impactar o desempenho se muitos Observers estiverem registrados para um Subject ou se as notificações forem frequentes.
- **Ordem de Notificação**: A ordem em que os Observers são notificados pode ser importante e difícil de controlar.

### Conclusão

O padrão Observer é uma solução eficaz para situações onde um objeto precisa notificar múltiplos objetos sobre mudanças em seu estado, promovendo o desacoplamento e a flexibilidade. Ele é especialmente útil em sistemas de eventos e notificações, interfaces gráficas e padrões arquiteturais como MVC. No entanto, deve-se tomar cuidado com a complexidade adicional e possíveis impactos de desempenho ao usá-lo.
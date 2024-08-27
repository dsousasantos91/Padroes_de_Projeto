# Memento

O padrão de projeto Memento é um padrão comportamental que permite capturar e externalizar o estado interno de um objeto sem violar seu encapsulamento, para que o objeto possa ser restaurado a este estado mais tarde. Esse padrão é particularmente útil para implementar funcionalidades de desfazer (undo) em sistemas.

### Estrutura do Memento

1. **Memento**: Armazena o estado interno do Originator e protege contra acesso externo que não seja o próprio Originator.
2. **Originator**: Cria um Memento contendo um snapshot de seu estado atual e usa o Memento para restaurar seu estado.
3. **Caretaker**: Responsável por armazenar Mementos, mas não pode operar ou inspecionar o conteúdo de um Memento.

### Exemplo em Java

Vamos considerar um exemplo onde temos um editor de texto simples que pode salvar e restaurar seu estado.

### Memento

```java
public class TextoMemento {
    private String estadoTexto;

    public TextoMemento(String estadoTexto) {
        this.estadoTexto = estadoTexto;
    }

    public String getEstadoTexto() {
        return estadoTexto;
    }
}

```

### Originator

```java
public class EditorTexto {
    private String texto;

    public void escrever(String novoTexto) {
        texto = novoTexto;
    }

    public String ler() {
        return texto;
    }

    public TextoMemento salvar() {
        return new TextoMemento(texto);
    }

    public void restaurar(TextoMemento memento) {
        texto = memento.getEstadoTexto();
    }
}

```

### Caretaker

```java
import java.util.Stack;

public class Historico {
    private Stack<TextoMemento> historico = new Stack<>();

    public void salvarEstado(EditorTexto editor) {
        historico.push(editor.salvar());
    }

    public void desfazer(EditorTexto editor) {
        if (!historico.isEmpty()) {
            editor.restaurar(historico.pop());
        }
    }
}

```

### Client

```java
public class Main {
    public static void main(String[] args) {
        EditorTexto editor = new EditorTexto();
        Historico historico = new Historico();

        editor.escrever("Versão 1 do texto.");
        historico.salvarEstado(editor);

        editor.escrever("Versão 2 do texto.");
        historico.salvarEstado(editor);

        editor.escrever("Versão 3 do texto.");
        System.out.println("Texto atual: " + editor.ler()); // Texto atual: Versão 3 do texto.

        historico.desfazer(editor);
        System.out.println("Após desfazer: " + editor.ler()); // Após desfazer: Versão 2 do texto.

        historico.desfazer(editor);
        System.out.println("Após desfazer novamente: " + editor.ler()); // Após desfazer novamente: Versão 1 do texto.
    }
}

```

### Quando Usar o Padrão Memento

- **Desfazer e Refazer**: Quando você precisa fornecer uma funcionalidade de desfazer e refazer.
- **Histórico de Estados**: Quando você deseja manter um histórico dos estados de um objeto.
- **Encapsulamento de Estado**: Quando você deseja capturar e restaurar o estado interno de um objeto sem expor sua estrutura interna.

### Exemplos de Aplicação

1. **Editores de Texto**: Para implementar funcionalidades de desfazer e refazer.
2. **Jogos**: Para salvar e restaurar o estado do jogo.
3. **Sistemas de Configuração**: Para capturar e restaurar configurações de sistema ou de aplicativos.

### Vantagens do Memento

- **Encapsulamento**: Preserva o encapsulamento ao capturar e restaurar o estado interno de um objeto.
- **Desfazer/Refazer**: Facilita a implementação de funcionalidades de desfazer e refazer.
- **Simples de Usar**: O Originator pode criar e restaurar Mementos sem precisar conhecer a estrutura interna dos Mementos.

### Desvantagens do Memento

- **Uso de Memória**: Pode consumir muita memória se os estados capturados forem grandes ou se muitos Mementos forem armazenados.
- **Complexidade Adicional**: Introduz complexidade adicional ao código ao precisar gerenciar os Mementos.

### Conclusão

O padrão Memento é uma solução eficaz para capturar e restaurar o estado de um objeto, promovendo o encapsulamento e facilitando a implementação de funcionalidades de desfazer e refazer. Ele é especialmente útil em sistemas onde o histórico de estados é importante, como editores de texto e jogos, embora deva ser usado com cuidado para evitar problemas de uso excessivo de memória e complexidade adicional.
# Composite

O padrão de projeto Composite é um padrão estrutural que permite que objetos sejam compostos em estruturas de árvore para representar hierarquias do tipo parte-todo. Esse padrão trata objetos individuais e composições de objetos de maneira uniforme, permitindo que o cliente interaja com uma coleção de objetos da mesma forma que interage com um objeto individual.

### Estrutura do Composite

1. **Component**: Declara a interface para objetos na composição. Implementa o comportamento padrão para a interface comum às classes folha e composição.
2. **Leaf**: Representa objetos folha na composição. Uma folha não tem filhos.
3. **Composite**: Define o comportamento para componentes que têm filhos. Armazena subcomponentes e implementa operações relacionadas a filhos na interface Component.
4. **Client**: Manipula objetos na composição através da interface Component.

### Exemplo em Java

Vamos considerar um exemplo onde temos uma estrutura de arquivos e diretórios.

### Component

```java
public abstract class FileSystemComponent {
    public void add(FileSystemComponent component) {
        throw new UnsupportedOperationException();
    }
    public void remove(FileSystemComponent component) {
        throw new UnsupportedOperationException();
    }
    public FileSystemComponent getChild(int i) {
        throw new UnsupportedOperationException();
    }
    public String getName() {
        throw new UnsupportedOperationException();
    }
    public abstract void print();
}

```

### Leaf

```java
public class File extends FileSystemComponent {
    private String name;

    public File(String name) {
        this.name = name;
    }

    @Override
    public String getName() {
        return name;
    }

    @Override
    public void print() {
        System.out.println("Arquivo: " + getName());
    }
}

```

### Composite

```java
import java.util.ArrayList;
import java.util.List;

public class Directory extends FileSystemComponent {
    private List<FileSystemComponent> components = new ArrayList<>();
    private String name;

    public Directory(String name) {
        this.name = name;
    }

    @Override
    public void add(FileSystemComponent component) {
        components.add(component);
    }

    @Override
    public void remove(FileSystemComponent component) {
        components.remove(component);
    }

    @Override
    public FileSystemComponent getChild(int i) {
        return components.get(i);
    }

    @Override
    public String getName() {
        return name;
    }

    @Override
    public void print() {
        System.out.println("Diretório: " + getName());
        for (FileSystemComponent component : components) {
            component.print();
        }
    }
}

```

### Client

```java
public class Main {
    public static void main(String[] args) {
        FileSystemComponent arquivo1 = new File("arquivo1.txt");
        FileSystemComponent arquivo2 = new File("arquivo2.txt");
        FileSystemComponent arquivo3 = new File("arquivo3.txt");

        Directory diretorio1 = new Directory("diretorio1");
        Directory diretorio2 = new Directory("diretorio2");

        diretorio1.add(arquivo1);
        diretorio1.add(arquivo2);
        diretorio2.add(arquivo3);
        diretorio2.add(diretorio1);

        diretorio2.print();
    }
}

```

### Quando Usar o Padrão Composite

- **Hierarquia Parte-Todo**: Quando você tem uma hierarquia de objetos que deve ser tratada de maneira uniforme.
- **Tratamento Uniforme**: Quando você quer que clientes tratem objetos individuais e composições de objetos de maneira uniforme.
- **Facilidade de Adição e Remoção**: Quando você precisa facilitar a adição e remoção de componentes da estrutura.

### Exemplos de Aplicação

1. **Sistema de Arquivos**: Representar hierarquias de arquivos e diretórios.
2. **Desenho Gráfico**: Representar gráficos compostos de primitivas gráficas (linhas, círculos, etc.).
3. **Componentes GUI**: Representar hierarquias de componentes de interface do usuário (botões, painéis, etc.).
4. **Organização de Empresas**: Representar estruturas hierárquicas de organizações, como departamentos e subdepartamentos.

### Vantagens do Composite

- **Hierarquias Flexíveis**: Facilita a definição de hierarquias de objetos complexas.
- **Tratamento Uniforme**: Permite tratar objetos individuais e composições de maneira uniforme.
- **Facilidade de Gerenciamento**: Simplifica a adição e remoção de elementos da estrutura.

### Desvantagens do Composite

- **Complexidade Adicional**: Adiciona complexidade ao código devido à necessidade de gerenciar a composição e os componentes individuais.
- **Sobrecarga de Memória**: Pode aumentar o uso de memória devido à estrutura de árvore.

### Conclusão

O padrão Composite é uma solução eficaz para representar hierarquias de objetos complexos e permite que clientes interajam com essas hierarquias de maneira uniforme. Ele é especialmente útil quando a estrutura da composição é dinâmica e pode mudar em tempo de execução.
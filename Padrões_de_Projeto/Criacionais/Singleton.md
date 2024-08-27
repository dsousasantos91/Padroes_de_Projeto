# Singleton

O padrão de projeto Singleton é um padrão criacional que garante que uma classe tenha apenas uma instância e fornece um ponto global de acesso a essa instância. É frequentemente utilizado para gerenciar recursos compartilhados, como conexões de banco de dados ou configurações globais.

### Estrutura do Singleton

1. **Classe Singleton**: Contém um método estático que retorna a única instância da classe. O construtor da classe é privado para impedir a criação de novos objetos.

### Exemplo em Java

### Implementação do Singleton

```java
public class Singleton {
    // Instância única da classe
    private static Singleton instanciaUnica;

    // Construtor privado impede instanciamento fora da classe
    private Singleton() {
        // Inicialização do Singleton
    }

    // Método público estático para obter a instância única
    public static Singleton getInstancia() {
        if (instanciaUnica == null) {
            instanciaUnica = new Singleton();
        }
        return instanciaUnica;
    }

    public void exibirMensagem() {
        System.out.println("Instância única do Singleton!");
    }
}

```

### Utilização do Singleton

```java
public class Main {
    public static void main(String[] args) {
        // Obtém a instância única do Singleton
        Singleton singleton = Singleton.getInstancia();
        singleton.exibirMensagem(); // Instância única do Singleton!

        // Tentativa de obter outra instância do Singleton
        Singleton outroSingleton = Singleton.getInstancia();
        outroSingleton.exibirMensagem(); // Instância única do Singleton!

        // Verificação de que ambas as referências apontam para a mesma instância
        System.out.println(singleton == outroSingleton); // true
    }
}

```

### Considerações

### Thread Safety (Segurança de Thread)

Em ambientes multithread, é importante garantir que a criação da instância única seja thread-safe. Uma abordagem comum é usar a palavra-chave `synchronized`.

```java
public class Singleton {
    private static Singleton instanciaUnica;

    private Singleton() {}

    public static synchronized Singleton getInstancia() {
        if (instanciaUnica == null) {
            instanciaUnica = new Singleton();
        }
        return instanciaUnica;
    }
}

```

Outra abordagem é usar o padrão **Double-Checked Locking** para melhorar a eficiência:

```java
public class Singleton {
    private static volatile Singleton instanciaUnica;

    private Singleton() {}

    public static Singleton getInstancia() {
        if (instanciaUnica == null) {
            synchronized (Singleton.class) {
                if (instanciaUnica == null) {
                    instanciaUnica = new Singleton();
                }
            }
        }
        return instanciaUnica;
    }
}

```

### Inicialização Eager

Uma alternativa à inicialização lazy (tardia) é a inicialização eager (antecipada), onde a instância é criada no momento da carga da classe. Isso evita problemas de thread safety sem a necessidade de sincronização.

```java
public class Singleton {
    private static final Singleton instanciaUnica = new Singleton();

    private Singleton() {}

    public static Singleton getInstancia() {
        return instanciaUnica;
    }
}

```

### Quando Usar o Padrão Singleton

1. **Controle de Acesso a Recursos Compartilhados**: Quando há necessidade de controlar o acesso a um recurso compartilhado, como uma conexão de banco de dados ou um gerenciador de arquivos.
2. **Estado Global**: Quando se precisa manter um estado global acessível de qualquer lugar do sistema.
3. **Restrição de Instâncias**: Quando se quer garantir que uma classe tenha apenas uma única instância em todo o sistema.
4. **Gerenciamento de Configuração**: Quando há necessidade de um ponto central para gerenciar configurações ou outras informações globais.

### Exemplos de Aplicação

- **Gerenciamento de Conexões de Banco de Dados**: Para garantir que apenas uma única instância da conexão seja usada em toda a aplicação.
- **Loggers**: Para assegurar que todas as mensagens de log sejam tratadas por uma única instância de logger.
- **Gerenciamento de Configurações**: Para fornecer um ponto único de acesso às configurações de aplicação.
- **Caches**: Para implementar caches que precisam ser acessíveis globalmente e garantir que não existam múltiplas instâncias do cache.

### Vantagens do Singleton

- **Controle de Acesso**: Garante um ponto global de acesso à instância única.
- **Redução de Recursos**: Pode ser usado para gerenciar recursos compartilhados de forma eficiente.
- **Facilidade de Modificação**: Facilita a modificação da instância única sem afetar outras partes do código.

### Desvantagens do Singleton

- **Testabilidade**: Pode dificultar a escrita de testes unitários devido à dependência global da instância.
- **Multithreading**: Implementações não thread-safe podem levar a problemas em ambientes multithread.
- **Ocultação de Dependências**: Pode esconder dependências do código, tornando-o menos claro.

### Conclusão

O padrão Singleton é uma ferramenta poderosa quando usado corretamente, mas deve ser aplicado com cautela para evitar problemas relacionados à segurança de threads e dificuldades de teste.
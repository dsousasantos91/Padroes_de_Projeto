# Adapter

### Adapter

O padrão de projeto Adapter é um padrão estrutural que permite que interfaces incompatíveis trabalhem juntas. Ele funciona como um tradutor entre duas classes, permitindo que classes com interfaces incompatíveis colaborem sem modificar o código existente.

### Estrutura do Adapter

1. **Target**: Define a interface que o cliente espera.
2. **Client**: Colabora com objetos que implementam a interface Target.
3. **Adaptee**: Tem uma interface que precisa ser adaptada.
4. **Adapter**: Adapta a interface do Adaptee para a interface do Target.

### Exemplo em Java

Vamos considerar um exemplo onde queremos usar um sistema de áudio antigo (Adaptee) com um novo sistema de áudio (Target).

### Interface Target

```java
public interface SistemaDeAudio {
    void reproduzirSom();
}

```

### Adaptee

```java
public class SistemaDeAudioAntigo {
    public void reproduzirSomAntigo() {
        System.out.println("Reproduzindo som no sistema de áudio antigo.");
    }
}

```

### Adapter

```java
public class AdapterSistemaDeAudio implements SistemaDeAudio {
    private SistemaDeAudioAntigo sistemaDeAudioAntigo;

    public AdapterSistemaDeAudio(SistemaDeAudioAntigo sistemaDeAudioAntigo) {
        this.sistemaDeAudioAntigo = sistemaDeAudioAntigo;
    }

    @Override
    public void reproduzirSom() {
        sistemaDeAudioAntigo.reproduzirSomAntigo();
    }
}

```

### Client

```java
public class Main {
    public static void main(String[] args) {
        SistemaDeAudioAntigo sistemaDeAudioAntigo = new SistemaDeAudioAntigo();
        SistemaDeAudio sistemaDeAudio = new AdapterSistemaDeAudio(sistemaDeAudioAntigo);

        sistemaDeAudio.reproduzirSom(); // Reproduzindo som no sistema de áudio antigo.
    }
}

```

### Quando Usar o Padrão Adapter

- **Uso de Bibliotecas Existentes**: Quando você quer usar uma classe existente, mas sua interface não é compatível com o restante do código.
- **Migração de Sistemas**: Ao migrar um sistema legado para uma nova arquitetura ou tecnologia, permitindo que o novo sistema use as funcionalidades do sistema antigo.
- **Interoperabilidade**: Quando você deseja que duas interfaces incompatíveis, de diferentes bibliotecas ou frameworks, funcionem juntas.
- **Reutilização de Código**: Para reutilizar classes existentes, mas que não compartilham a interface necessária para a nova aplicação.

### Exemplos de Aplicação

1. **Sistemas de GUI**: Adaptar widgets de diferentes bibliotecas de interface gráfica para trabalhar com um sistema unificado.
2. **Bibliotecas de Terceiros**: Integrar uma biblioteca de terceiros que possui uma interface diferente da interface usada no seu sistema.
3. **Acessórios de Hardware**: Em software de controle de hardware, onde diferentes dispositivos têm interfaces diferentes e precisam ser controlados por uma interface unificada.
4. **Conexões de Banco de Dados**: Adaptar diferentes bibliotecas de conexão de banco de dados para um sistema que usa uma interface de conexão unificada.
5. **APIs de Serviço Web**: Adaptar diferentes APIs de serviços web para um cliente que espera uma interface unificada.

### Vantagens do Adapter

- **Reuso de Código Existente**: Permite que código existente com interfaces incompatíveis seja reutilizado sem modificações.
- **Separação de Responsabilidades**: O Adapter separa a adaptação da interface da lógica de negócios, promovendo um design mais limpo.
- **Flexibilidade**: Novos Adapters podem ser introduzidos para suportar diferentes interfaces, aumentando a flexibilidade do sistema.

### Desvantagens do Adapter

- **Complexidade Adicional**: Adiciona complexidade ao código devido à criação de classes adicionais.
- **Sobrecarga de Performance**: Pode introduzir uma pequena sobrecarga de performance devido à camada extra de adaptação.

### Tipos de Adapter

1. **Object Adapter**: Usa composição para adaptar a interface do Adaptee à interface do Target.
2. **Class Adapter**: Usa herança múltipla (quando suportada pela linguagem) para adaptar a interface do Adaptee à interface do Target.

### Exemplo de Object Adapter (usado acima)

O exemplo acima é um exemplo de Object Adapter, onde a adaptação é feita através da composição. O Adapter contém uma instância do Adaptee e traduz as chamadas de método para o formato esperado pelo Target.

### Exemplo de Class Adapter (Java não suporta herança múltipla diretamente)

Java não suporta herança múltipla diretamente, então o Class Adapter não é uma opção nativa. Em linguagens que suportam herança múltipla, o Adapter herdaria tanto do Target quanto do Adaptee, implementando os métodos necessários diretamente.

### Conclusão

O padrão Adapter é extremamente útil para integrar sistemas existentes com novos sistemas sem modificar o código original. Ele promove a reutilização de código, a flexibilidade e a manutenção de um design limpo e separado de responsabilidades.
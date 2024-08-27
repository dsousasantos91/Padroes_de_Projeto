# Interpreter

O padrão de projeto Interpreter é um padrão comportamental que define uma representação para a gramática de uma linguagem e um interpretador que usa essa representação para interpretar sentenças dessa linguagem. Este padrão é útil para implementar linguagens específicas de domínio (DSLs) e pode ser usado para interpretar e executar expressões simples.

### Estrutura do Interpreter

1. **Abstract Expression**: Declara uma interface para interpretar o contexto.
2. **Terminal Expression**: Implementa uma operação associada a símbolos terminais na gramática.
3. **Nonterminal Expression**: Implementa uma operação associada a símbolos não-terminais na gramática.
4. **Context**: Contém informações globais para o intérprete.
5. **Client**: Constrói a árvore de interpretação e a executa.

### Exemplo em Java

Vamos considerar um exemplo de uma linguagem simples para interpretar expressões aritméticas básicas como "5 3 +", que significa "5 + 3".

### Abstract Expression

```java
public interface Expressao {
    int interpretar();
}

```

### Terminal Expression

```java
public class Numero implements Expressao {
    private int numero;

    public Numero(int numero) {
        this.numero = numero;
    }

    @Override
    public int interpretar() {
        return numero;
    }
}

```

### Nonterminal Expression

```java
public class Soma implements Expressao {
    private Expressao esquerda;
    private Expressao direita;

    public Soma(Expressao esquerda, Expressao direita) {
        this.esquerda = esquerda;
        this.direita = direita;
    }

    @Override
    public int interpretar() {
        return esquerda.interpretar() + direita.interpretar();
    }
}

public class Subtracao implements Expressao {
    private Expressao esquerda;
    private Expressao direita;

    public Subtracao(Expressao esquerda, Expressao direita) {
        this.esquerda = esquerda;
        this.direita = direita;
    }

    @Override
    public int interpretar() {
        return esquerda.interpretar() - direita.interpretar();
    }
}

```

### Client

```java
import java.util.Stack;

public class Interpretador {
    public static void main(String[] args) {
        String expressao = "5 3 + 2 -";
        Expressao interpretador = construirArvoreDeInterpretacao(expressao);
        int resultado = interpretador.interpretar();
        System.out.println("Resultado da expressão '" + expressao + "' é: " + resultado); // Output: 6
    }

    public static Expressao construirArvoreDeInterpretacao(String expressao) {
        Stack<Expressao> pilha = new Stack<>();

        for (String token : expressao.split(" ")) {
            if (token.matches("-?\\\\d+")) { // Se for um número
                pilha.push(new Numero(Integer.parseInt(token)));
            } else {
                Expressao direita = pilha.pop();
                Expressao esquerda = pilha.pop();
                switch (token) {
                    case "+":
                        pilha.push(new Soma(esquerda, direita));
                        break;
                    case "-":
                        pilha.push(new Subtracao(esquerda, direita));
                        break;
                }
            }
        }

        return pilha.pop();
    }
}

```

### Quando Usar o Padrão Interpreter

- **Linguagens Específicas de Domínio (DSLs)**: Quando você precisa interpretar e executar uma linguagem específica de domínio.
- **Expressões Complexas**: Quando você tem expressões complexas que precisam ser avaliadas de maneira estruturada.
- **Análise de Sintaxe**: Quando você precisa analisar e interpretar sintaxes de entrada.

### Exemplos de Aplicação

1. **Compiladores**: Para interpretar e executar código-fonte.
2. **Interpretação de Expressões Matemáticas**: Para interpretar e avaliar expressões matemáticas.
3. **Validação de Sintaxe**: Para verificar a conformidade de entradas com uma gramática específica.
4. **Configuração de Sistemas**: Para interpretar arquivos de configuração complexos.

### Vantagens do Interpreter

- **Extensibilidade**: Facilita a adição de novas expressões e regras de interpretação.
- **Mantenabilidade**: O código é organizado em classes separadas, cada uma representando uma regra de gramática.
- **Clareza**: Promove a clareza ao mapear diretamente a gramática de uma linguagem para a estrutura de classes.

### Desvantagens do Interpreter

- **Complexidade**: Pode se tornar complexo e difícil de gerenciar para gramáticas grandes ou complexas.
- **Desempenho**: Pode ser ineficiente devido à criação e gestão de muitos objetos.

### Conclusão

O padrão Interpreter é uma solução eficaz para situações onde é necessário interpretar e executar linguagens específicas de domínio ou expressões complexas. Ele promove a extensibilidade e a clareza, permitindo que a gramática de uma linguagem seja mapeada diretamente para a estrutura de classes, embora possa introduzir complexidade adicional para gramáticas maiores.
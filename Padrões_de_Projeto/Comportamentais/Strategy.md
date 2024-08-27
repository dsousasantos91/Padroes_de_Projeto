# Strategy

O padrão de projeto Strategy é um padrão comportamental que define uma família de algoritmos, encapsula cada um deles e os torna intercambiáveis. O padrão Strategy permite que o algoritmo varie independentemente dos clientes que o utilizam. Ele é especialmente útil quando você deseja definir uma série de comportamentos semelhantes e alternar entre eles de forma transparente para os clientes.

### Estrutura do Strategy

1. **Strategy**: Declara uma interface comum para todos os algoritmos suportados.
2. **ConcreteStrategy**: Implementa o algoritmo usando a interface Strategy.
3. **Context**: Mantém uma referência a um objeto Strategy e chama o método definido na interface Strategy.

### Exemplo em Java

Vamos considerar um exemplo onde temos diferentes estratégias de ordenação (Bubble Sort e Quick Sort) que podem ser aplicadas a uma coleção de números.

### Strategy Interface

```java
public interface EstrategiaOrdenacao {
    void ordenar(int[] numeros);
}

```

### Concrete Strategies

```java
public class BubbleSort implements EstrategiaOrdenacao {
    @Override
    public void ordenar(int[] numeros) {
        int n = numeros.length;
        for (int i = 0; i < n-1; i++) {
            for (int j = 0; j < n-i-1; j++) {
                if (numeros[j] > numeros[j+1]) {
                    // Troca numeros[j] e numeros[j+1]
                    int temp = numeros[j];
                    numeros[j] = numeros[j+1];
                    numeros[j+1] = temp;
                }
            }
        }
        System.out.println("Ordenado usando Bubble Sort");
    }
}

public class QuickSort implements EstrategiaOrdenacao {
    @Override
    public void ordenar(int[] numeros) {
        quickSort(numeros, 0, numeros.length - 1);
        System.out.println("Ordenado usando Quick Sort");
    }

    private void quickSort(int[] numeros, int inicio, int fim) {
        if (inicio < fim) {
            int pi = partition(numeros, inicio, fim);
            quickSort(numeros, inicio, pi - 1);
            quickSort(numeros, pi + 1, fim);
        }
    }

    private int partition(int[] numeros, int inicio, int fim) {
        int pivot = numeros[fim];
        int i = (inicio - 1);
        for (int j = inicio; j < fim; j++) {
            if (numeros[j] <= pivot) {
                i++;
                int temp = numeros[i];
                numeros[i] = numeros[j];
                numeros[j] = temp;
            }
        }
        int temp = numeros[i + 1];
        numeros[i + 1] = numeros[fim];
        numeros[fim] = temp;
        return i + 1;
    }
}

```

### Context

```java
public class Contexto {
    private EstrategiaOrdenacao estrategia;

    public void setEstrategia(EstrategiaOrdenacao estrategia) {
        this.estrategia = estrategia;
    }

    public void executarEstrategia(int[] numeros) {
        estrategia.ordenar(numeros);
    }
}

```

### Client

```java
public class Main {
    public static void main(String[] args) {
        Contexto contexto = new Contexto();

        int[] numeros = {64, 34, 25, 12, 22, 11, 90};

        // Usando Bubble Sort
        contexto.setEstrategia(new BubbleSort());
        contexto.executarEstrategia(numeros);
        printArray(numeros);

        // Resetando array para desordenado
        numeros = new int[]{64, 34, 25, 12, 22, 11, 90};

        // Usando Quick Sort
        contexto.setEstrategia(new QuickSort());
        contexto.executarEstrategia(numeros);
        printArray(numeros);
    }

    public static void printArray(int[] numeros) {
        for (int num : numeros) {
            System.out.print(num + " ");
        }
        System.out.println();
    }
}

```

### Quando Usar o Padrão Strategy

- **Vários Algoritmos**: Quando você tem várias maneiras de realizar uma operação e deseja que o cliente escolha qual utilizar.
- **Desacoplamento de Algoritmos**: Quando você deseja desacoplar os algoritmos do contexto em que são usados.
- **Alteração de Algoritmo em Tempo de Execução**: Quando você precisa alterar o algoritmo que está sendo utilizado em tempo de execução.

### Exemplos de Aplicação

1. **Algoritmos de Ordenação**: Como mostrado no exemplo acima.
2. **Cálculo de Frete**: Diferentes estratégias para calcular o custo do frete em um sistema de e-commerce.
3. **Processamento de Pagamentos**: Diferentes métodos de pagamento (cartão de crédito, PayPal, transferência bancária) em um sistema de pagamento.
4. **Compressão de Dados**: Diferentes algoritmos de compressão para compactar dados.

### Vantagens do Strategy

- **Desacoplamento**: Desacopla o algoritmo do contexto em que é usado, facilitando a manutenção e a extensão.
- **Intercambiabilidade**: Permite que algoritmos sejam intercambiáveis, proporcionando flexibilidade.
- **Reutilização de Código**: Facilita a reutilização de algoritmos em diferentes contextos.

### Desvantagens do Strategy

- **Complexidade**: Pode introduzir complexidade adicional no código ao adicionar várias classes de estratégia.
- **Sobrecarga de Comunicação**: O contexto precisa conhecer todas as estratégias para poder utilizá-las, o que pode introduzir uma sobrecarga de comunicação.

### Conclusão

O padrão Strategy é uma solução eficaz para situações onde você precisa de flexibilidade para escolher e alterar algoritmos em tempo de execução. Ele promove o desacoplamento e a reutilização de código, permitindo que diferentes algoritmos sejam intercambiáveis. No entanto, deve-se considerar a complexidade adicional ao usar este padrão.
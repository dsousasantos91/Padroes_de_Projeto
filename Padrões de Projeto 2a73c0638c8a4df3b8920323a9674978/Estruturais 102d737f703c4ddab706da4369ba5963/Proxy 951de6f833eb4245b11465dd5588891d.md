# Proxy

O padrão de projeto Proxy é um padrão estrutural que fornece um substituto ou ponto de acesso para outro objeto, controlando o acesso a este. Ele é útil quando você deseja adicionar uma camada de controle, como controle de acesso, carregamento preguiçoso, caching, ou mesmo registro de atividades, antes de delegar as operações para o objeto real.

### Estrutura do Proxy

1. **Subject**: Define a interface comum para RealSubject e Proxy.
2. **RealSubject**: Implementa o Subject, representando o objeto real que o Proxy irá controlar.
3. **Proxy**: Contém uma referência ao RealSubject e implementa o Subject, delegando chamadas de método para o RealSubject, possivelmente realizando algumas ações adicionais antes ou depois da delegação.

### Tipos Comuns de Proxy

1. **Proxy Virtual**: Adia a criação e inicialização do objeto real até que ele seja necessário.
2. **Proxy de Proteção**: Controla o acesso ao objeto real, permitindo que apenas certos clientes acessem métodos específicos.
3. **Proxy Remoto**: Representa um objeto que reside em um endereço diferente, normalmente em um servidor remoto.
4. **Proxy de Cache**: Armazena os resultados de operações dispendiosas para melhorar o desempenho.

### Exemplo em Java

Vamos considerar um exemplo onde temos um objeto que carrega imagens de forma preguiçosa (lazy loading) usando o Proxy Virtual.

### Subject

```java
public interface Imagem {
    void exibir();
}

```

### RealSubject

```java
public class ImagemReal implements Imagem {
    private String nomeArquivo;

    public ImagemReal(String nomeArquivo) {
        this.nomeArquivo = nomeArquivo;
        carregarImagemDoDisco();
    }

    private void carregarImagemDoDisco() {
        System.out.println("Carregando " + nomeArquivo);
    }

    @Override
    public void exibir() {
        System.out.println("Exibindo " + nomeArquivo);
    }
}

```

### Proxy

```java
public class ProxyImagem implements Imagem {
    private ImagemReal imagemReal;
    private String nomeArquivo;

    public ProxyImagem(String nomeArquivo) {
        this.nomeArquivo = nomeArquivo;
    }

    @Override
    public void exibir() {
        if (imagemReal == null) {
            imagemReal = new ImagemReal(nomeArquivo);
        }
        imagemReal.exibir();
    }
}

```

### Client

```java
public class Main {
    public static void main(String[] args) {
        Imagem imagem = new ProxyImagem("foto.jpg");

        // A imagem será carregada do disco apenas quando for exibida pela primeira vez
        imagem.exibir(); // Output: Carregando foto.jpg
                         //         Exibindo foto.jpg

        // A imagem não será carregada do disco novamente
        imagem.exibir(); // Output: Exibindo foto.jpg
    }
}

```

### Quando Usar o Padrão Proxy

- **Controle de Acesso**: Quando você precisa controlar o acesso a um objeto, permitindo que apenas certos clientes ou operações sejam realizadas.
- **Carregamento Preguiçoso**: Quando você deseja adiar a criação e inicialização de um objeto até que ele seja realmente necessário.
- **Operações Remotas**: Quando você precisa representar um objeto que reside em um endereço remoto, como em uma arquitetura distribuída.
- **Otimização de Performance**: Quando você deseja armazenar em cache os resultados de operações dispendiosas para melhorar o desempenho.

### Exemplos de Aplicação

1. **Sistemas de Arquivos**: Carregar arquivos grandes de forma preguiçosa.
2. **Controle de Acesso**: Verificar permissões antes de permitir o acesso a métodos ou dados sensíveis.
3. **Proxy Remoto**: Acessar objetos que estão em servidores remotos.
4. **Cache de Dados**: Armazenar em cache os resultados de consultas a bancos de dados.

### Vantagens do Proxy

- **Controle Adicional**: Adiciona uma camada de controle sobre o objeto real, permitindo várias funcionalidades adicionais como controle de acesso, carregamento preguiçoso, e caching.
- **Desempenho**: Pode melhorar o desempenho do sistema ao adiar a criação de objetos ou ao armazenar em cache os resultados de operações dispendiosas.
- **Flexibilidade**: Permite modificar ou estender funcionalidades sem alterar o código do objeto real.

### Desvantagens do Proxy

- **Complexidade Adicional**: Adiciona complexidade ao código devido à introdução de classes adicionais.
- **Sobrecarga de Desempenho**: Embora possa melhorar o desempenho em alguns casos, também pode introduzir uma pequena sobrecarga devido à camada adicional de delegação.

### Conclusão

O padrão Proxy é uma ferramenta poderosa para adicionar controle, flexibilidade e otimização a sistemas que interagem com objetos potencialmente complexos ou dispendiosos. Ele é especialmente útil em situações onde o controle de acesso, o carregamento preguiçoso, e o caching são necessários para melhorar a eficiência e a segurança do sistema.
# desafiocaixa
import java.util.LinkedList;

// Classe para representar um cliente
class Cliente {
    String cpf;
    String nome;
    String endereco;
    String telefone;

    public Cliente(String cpf, String nome, String endereco, String telefone) {
        this.cpf = cpf;
        this.nome = nome;
        this.endereco = endereco;
        this.telefone = telefone;
    }
}

// Classe para a tabela hash
class TabelaHash {
    private static final int TAMANHO_TABELA = 1000;
    private LinkedList<Cliente>[] tabela;

    public TabelaHash() {
        tabela = new LinkedList[TAMANHO_TABELA];
    }

    // Função de hash simples (soma dos caracteres do CPF)
    private int hash(String cpf) {
        int soma = 0;
        for (int i = 0; i < cpf.length(); i++) {
            soma += cpf.charAt(i);
        }
        return soma % TAMANHO_TABELA;
    }

    // Método para inserir um cliente na tabela
    public void inserir(Cliente cliente) {
        int indice = hash(cliente.cpf);
        if (tabela[indice] == null) {
            tabela[indice] = new LinkedList<>();
        }
        tabela[indice].add(cliente);
    }

    // Método para buscar um cliente pelo CPF na tabela
    public Cliente buscar(String cpf) {
        int indice = hash(cpf);
        if (tabela[indice] != null) {
            for (Cliente cliente : tabela[indice]) {
                if (cliente.cpf.equals(cpf)) {
                    return cliente;
                }
            }
        }
        return null;
    }
}

public class Main {
    public static void main(String[] args) {
        TabelaHash tabelaHash = new TabelaHash();

        // Exemplo de inserção de clientes na tabela
        tabelaHash.inserir(new Cliente("123.456.789-00", "João", "Rua A, 123", "123456789"));
        tabelaHash.inserir(new Cliente("987.654.321-00", "Maria", "Rua B, 456", "987654321"));

        // Exemplo de busca por cliente pelo CPF
        Cliente clienteEncontrado = tabelaHash.buscar("123.456.789-00");
        if (clienteEncontrado != null) {
            System.out.println("Cliente encontrado:");
            System.out.println("Nome: " + clienteEncontrado.nome);
            System.out.println("Endereço: " + clienteEncontrado.endereco);
            System.out.println("Telefone: " + clienteEncontrado.telefone);
        } else {
            System.out.println("Cliente não encontrado.");
        }
    }
}

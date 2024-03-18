# desafiocaixa

import javafx.application.Application;
import javafx.geometry.Insets;
import javafx.scene.Scene;
import javafx.scene.control.Button;
import javafx.scene.control.Label;
import javafx.scene.control.TextField;
import javafx.scene.layout.GridPane;
import javafx.stage.Stage;

import java.util.HashMap;

// Classe para representar um cliente
class Cliente {
    private String cpf;
    private String nome;
    private String endereco;
    private String telefone;

    public Cliente(String cpf, String nome, String endereco, String telefone) {
        this.cpf = cpf;
        this.nome = nome;
        this.endereco = endereco;
        this.telefone = telefone;
    }

    public String getCpf() {
        return cpf;
    }

    public String getNome() {
        return nome;
    }

    public String getEndereco() {
        return endereco;
    }

    public String getTelefone() {
        return telefone;
    }
}

// Classe para a tabela hash
class TabelaHash {
    private HashMap<String, Cliente> tabela;

    public TabelaHash() {
        tabela = new HashMap<>();
    }

    // Método para inserir um cliente na tabela
    public void inserir(Cliente cliente) {
        tabela.put(cliente.getCpf(), cliente);
    }

    // Método para buscar um cliente pelo CPF na tabela
    public Cliente buscar(String cpf) {
        return tabela.get(cpf);
    }
}

public class Main extends Application {
    private TabelaHash tabelaHash;

    @Override
    public void start(Stage primaryStage) {
        tabelaHash = new TabelaHash();

        GridPane gridPane = new GridPane();
        gridPane.setPadding(new Insets(10));
        gridPane.setVgap(10);
        gridPane.setHgap(10);

        TextField cpfField = new TextField();
        Button buscarButton = new Button("Buscar");
        Label resultadoLabel = new Label("");

        gridPane.add(new Label("CPF:"), 0, 0);
        gridPane.add(cpfField, 1, 0);
        gridPane.add(buscarButton, 2, 0);
        gridPane.add(resultadoLabel, 0, 1, 3, 1);

        buscarButton.setOnAction(e -> {
            String cpf = cpfField.getText();
            Cliente cliente = tabelaHash.buscar(cpf);
            if (cliente != null) {
                resultadoLabel.setText("Cliente encontrado:\n" +
                        "Nome: " + cliente.getNome() + "\n" +
                        "Endereço: " + cliente.getEndereco() + "\n" +
                        "Telefone: " + cliente.getTelefone());
            } else {
                resultadoLabel.setText("Cliente com CPF " + cpf + " não encontrado.");
            }
        });

        Scene scene = new Scene(gridPane, 400, 150);
        primaryStage.setTitle("Busca de Cliente por CPF");
        primaryStage.setScene(scene);
        primaryStage.show();
    }

    public static void main(String[] args) {
        launch(args);
    }
}

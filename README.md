# desafiocaixa

import javafx.application.Application;
import javafx.geometry.Insets;
import javafx.scene.Scene;
import javafx.scene.control.Button;
import javafx.scene.control.Label;
import javafx.scene.control.TextField;
import javafx.scene.layout.GridPane;
import javafx.stage.Stage;

public class CadastroClientes extends Application {

    @Override
    public void start(Stage primaryStage) {
        primaryStage.setTitle("Cadastro de Clientes");

        GridPane grid = new GridPane();
        grid.setPadding(new Insets(20, 20, 20, 20));
        grid.setVgap(10);
        grid.setHgap(10);

        Label nameLabel = new Label("Nome:");
        GridPane.setConstraints(nameLabel, 0, 0);
        TextField nameInput = new TextField();
        nameInput.setPromptText("Digite o nome");
        GridPane.setConstraints(nameInput, 1, 0);

        Label emailLabel = new Label("Email:");
        GridPane.setConstraints(emailLabel, 0, 1);
        TextField emailInput = new TextField();
        emailInput.setPromptText("Digite o email");
        GridPane.setConstraints(emailInput, 1, 1);

        Button addButton = new Button("Adicionar");
        GridPane.setConstraints(addButton, 1, 2);

        grid.getChildren().addAll(nameLabel, nameInput, emailLabel, emailInput, addButton);

        addButton.setOnAction(e -> {
            // Aqui você pode adicionar a lógica para salvar os dados do cliente
            String nome = nameInput.getText();
            String email = emailInput.getText();
            System.out.println("Cliente adicionado: " + nome + ", " + email);
            nameInput.clear();
            emailInput.clear();
        });

        Scene scene = new Scene(grid, 300, 200);
        primaryStage.setScene(scene);
        primaryStage.show();
    }

    public static void main(String[] args) {
        launch(args);
    }
}

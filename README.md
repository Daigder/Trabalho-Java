# Trabalho-Java

package com.company;

import java.util.Scanner;

public class ColecaoPersonagem {
    private static final int num_colunas = 6;

    public static void inserirPersonagem(String[][] matriz, int linhas) {
        Scanner scanner = new Scanner(System.in);
        int linha;

        mostrarPersonagens(matriz, linhas);
        do {
            System.out.println("Informe onde você deseja inserir o personagem com valores de 1 a " + linhas);
            linha = scanner.nextInt();
        } while (linha < 1 || linha > linhas);

        System.out.println("Insira o nome do personagem: ");
        matriz[linha - 1][0] = scanner.next();
        System.out.println("Insira a quantidade de Vida Base: ");
        matriz[linha - 1][1] = scanner.next();
        System.out.println("Insira a quantidade de Mana Base: ");
        matriz[linha - 1][2] = scanner.next();
        System.out.println("Insira a quantidade de Dano Fisico Base: ");
        matriz[linha - 1][3] = scanner.next();
        System.out.println("Insira a quantidade de Dano Magico Base: ");
        matriz[linha - 1][4] = scanner.next();
        System.out.println("Insira a quantidade de Ataque Speed Base: ");
        matriz[linha - 1][5] = scanner.next();
        System.out.println("Personagem adicionado.");
    }

    public static void mostrarPersonagens(String[][] matriz, int linhas) {
        System.out.println("Nome do personagem | Vida Base | Mana base | Dano AD Base | Dano AP base | Ataque Speed Base");
        for (int i = 0; i < linhas; i++) {
            System.out.print((i + 1) + " - ");
            for (int j = 0; j < num_colunas; j++) {
                System.out.print(matriz[i][j] + " | ");
            }
            System.out.println();
        }
    }

    public static void compararPersonagens(String[][] matriz, int linhas) {
        Scanner scanner = new Scanner(System.in);
        System.out.println("Insira o número do primeiro personagem a ser comparado:");
        int personagem1 = scanner.nextInt();
        System.out.println("Insira o número do segundo personagem a ser comparado:");
        int personagem2 = scanner.nextInt();

        if (personagem1 < 1 || personagem1 > linhas || personagem2 < 1 || personagem2 > linhas) {
            System.out.println("Personagem inválido!");
            return;
        }

        float statusPersonagem1 = calcularStatusPersonagem(matriz, personagem1 - 1);
        float statusPersonagem2 = calcularStatusPersonagem(matriz, personagem2 - 1);

        System.out.println("Status do Personagem " + personagem1 + ": " + statusPersonagem1);
        System.out.println("Status do Personagem " + personagem2 + ": " + statusPersonagem2);

        if (statusPersonagem1 > statusPersonagem2) {
            System.out.println("Personagem " + personagem1 + " tem o maior status.");
        } else if (statusPersonagem2 > statusPersonagem1) {
            System.out.println("Personagem " + personagem2 + " tem o maior status.");
        } else {
            System.out.println("Os dois personagenstêm o mesmo status.");
        }
    }

    public static void calcularStatusTotal(String[][] matriz, int linhas) {
        float statusTotal = 0.0f;
        for (int i = 0; i < linhas; i++) {
            if (matriz[i][0] != null) {
                statusTotal += calcularStatusPersonagem(matriz, i);
            }
        }
        System.out.println("O status total da coleção é: " + statusTotal);
    }

    public static float calcularStatusPersonagem(String[][] matriz, int indice) {
        float vidaBase = Float.parseFloat(matriz[indice][1]);
        float manaBase = Float.parseFloat(matriz[indice][2]);
        float danoFisicoBase = Float.parseFloat(matriz[indice][3]);
        float danoMagicoBase = Float.parseFloat(matriz[indice][4]);
        float ataqueSpeedBase = Float.parseFloat(matriz[indice][5]);

        return vidaBase + manaBase + danoFisicoBase + danoMagicoBase + ataqueSpeedBase;
    }

    public static void removerPersonagem(String[][] matriz, int linhas, String nomePersonagem) {
        boolean encontrado = false;
        for (int i = 0; i < linhas; i++) {
            if (matriz[i][0] != null && matriz[i][0].equals(nomePersonagem)) {
                encontrado = true;
                limparDadosPersonagem(matriz, i);
            }
        }
        if (encontrado) {
            System.out.println("Personagem removido com sucesso");
        } else {
            System.out.println("Personagem não encontrado.");
        }
    }

    private static void limparDadosPersonagem(String[][] matriz, int indice) {
        matriz[indice][0] = null;
        matriz[indice][1] = null;
        matriz[indice][2] = null;
        matriz[indice][3] = null;
        matriz[indice][4] = null;
        matriz[indice][5] = null;
    }

    public static void calcularStatusPersonagemEspecifico(String[][] matriz, int linhas) {
        Scanner scanner = new Scanner(System.in);
        System.out.println("Insira o número do personagem para calcular o status:");
        int personagem = scanner.nextInt();

        if (personagem < 1 || personagem > linhas) {
            System.out.println("Personagem inválido! Insira um número válido.");
        } else {
            float statusPersonagem = calcularStatusPersonagem(matriz, personagem - 1);
            System.out.println("Status do Personagem " + personagem + ": " + statusPersonagem);
        }
    }

    public static void main(String[] args) {
        String[][] colecao;
        int numPersonagens, opcao;
        Scanner scanner = new Scanner(System.in);
        String nomePersonagem;

        System.out.println("Insira a quantidade de personagens que serão inseridos na sua coleção:");
        numPersonagens = scanner.nextInt();

        while (numPersonagens <= 0) {
            System.out.println("Quantidade inválida! Insira um número maior que zero:");
            numPersonagens = scanner.nextInt();
        }

        colecao = new String[numPersonagens][num_colunas];

        do {
            System.out.println("Escolha uma opção:");
            System.out.println("1 - Mostrar coleção de personagens");
            System.out.println("2 - Inserir novo personagem na coleção");
            System.out.println("3 - Comparar status de personagens (mínimo e máximo de 2 personagens)");
            System.out.println("4 - Calcular status total da coleção");
            System.out.println("5 - Calcular status de um personagem especifico");
            System.out.println("6 - Remover personagem da lista");
            System.out.println("0 - Sair");
            opcao = scanner.nextInt();

            switch (opcao) {
                case 0:
                    break;
                case 1:
                    mostrarPersonagens(colecao, numPersonagens);
                    break;
                case 2:
                    inserirPersonagem(colecao, numPersonagens);
                    break;
                case 3:
                    compararPersonagens(colecao, numPersonagens);
                    break;
                case 4:
                    calcularStatusTotal(colecao, numPersonagens);
                    break;
                case 5:
                    calcularStatusPersonagemEspecifico(colecao, numPersonagens);
                case 6:
                    System.out.println("Insira o nome do personagem a ser removido:");
                    nomePersonagem = scanner.next();
                    removerPersonagem(colecao, numPersonagens, nomePersonagem);
                    break;
                default:
                    System.out.println("Opção inválida!");
            }
        } while (opcao != 0);
    }
}

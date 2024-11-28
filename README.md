#include <stdio.h>
#include <stdlib.h>
#include <string.h>

#define MAX_CARROS 100

typedef struct {
    char nome[50];
    char modelo[50];
    int ano;
    float preco;
} Carro;

Carro carros[MAX_CARROS];
int contador = 0;

void cadastrarCarro() {
    if (contador < MAX_CARROS) {
        printf("\nCadastrar Carro\n");
        printf("Digite o nome do cliente: ");
        getchar();
        fgets(carros[contador].nome, 50, stdin);
        carros[contador].nome[strcspn(carros[contador].nome, "\n")] = '\0';

        printf("Digite o nome do carro: ");
        fgets(carros[contador].modelo, 50, stdin);
        carros[contador].modelo[strcspn(carros[contador].modelo, "\n")] = '\0';

        printf("Digite o ano do carro: ");
        scanf("%d", &carros[contador].ano);

        printf("Digite o valor do carro: ");
        scanf("%f", &carros[contador].preco);

        contador++;
        printf("\nCarro cadastrado!\n");
    } else {
        printf("\nLimite de cadastros atingido!\n");
    }
}

void consultarCarros() {
    if (contador == 0) {
        printf("\nNenhum carro cadastrado!\n");
        return;
    }
    printf("\nConsulta aos carros cadastrados\n");
    for (int i = 0; i < contador; i++) {
        printf("\nCarro %d:\n", i + 1);
        printf("Cliente: %s\n", carros[i].nome);
        printf("Carro: %s\n", carros[i].modelo);
        printf("Ano: %d\n", carros[i].ano);
        printf("Preço: R$ %.2f\n", carros[i].preco);
    }
}

void gerarRelatorio() {
    if (contador == 0) {
        printf("\nNenhum carro cadastrado para gerar relatório!\n");
        return;
    }
    printf("\nRelatório de Carros Cadastrados\n");
    for (int i = 0; i < contador; i++) {
        printf("\nCarro %d:\n", i + 1);
        printf("Cliente: %s\n", carros[i].nome);
        printf("Carro: %s\n", carros[i].modelo);
        printf("Ano: %d\n", carros[i].ano);
        printf("Preço: R$ %.2f\n", carros[i].preco);
    }
}

void excluirCarro() {
    if (contador == 0) {
        printf("\nNenhum carro cadastrado para excluir!\n");
        return;
    }

    char nome[50];
    printf("\nExcluir Carro\n");
    printf("Digite o nome do cliente que deseja excluir o carro: ");
    getchar();
    fgets(nome, 50, stdin);
    nome[strcspn(nome, "\n")] = '\0'; 

    int encontrado = 0;
    for (int i = 0; i < contador; i++) {
        if (strcmp(carros[i].nome, nome) == 0) {
            
            for (int j = i; j < contador - 1; j++) {
                carros[j] = carros[j + 1];
            }
            contador--;
            printf("\nCarro '%s' excluído com sucesso!\n", nome);
            encontrado = 1;
            break;
        }
    }

    if (!encontrado) {
        printf("\nCarro não encontrado!\n");
    }
}

void mostrarMenu() {
    int opcao;
    do {
        printf("\nDonatinho Veículos\n");
        printf("1. Cadastrar Carro\n");
        printf("2. Consultar Carros\n");
        printf("3. Gerar Relatório\n");
        printf("4. Excluir Carro\n");
        printf("5. Sair\n");
        printf("Escolha uma opção: ");
        scanf("%d", &opcao);

        switch (opcao) {
            case 1:
                cadastrarCarro();
                break;
            case 2:
                consultarCarros();
                break;
            case 3:
                gerarRelatorio();
                break;
            case 4:
                excluirCarro();
                break;
            case 5:
                printf("\nSaindo do programa...\n");
                break;
            default:
                printf("\nOpção inválida! Tente novamente.\n");
        }
    } while (opcao != 5);
}

int main() {
    mostrarMenu();
    return 0;
}

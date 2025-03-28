#include <stdio.h>

#define MAX_SIZE 50

void imprimirVetor(int vetor[], int tamanho) {
    printf("\nVetor: ");
    for (int i = 0; i < tamanho; i++) {
        printf("%d ", vetor[i]);
    }
    printf("\n");
}

int buscaBinaria(int vetor[], int tamanho, int elemento) {
    int inicio = 0;
    int fim = tamanho - 1;
    
    while (inicio <= fim) {
        int meio = (inicio + fim) / 2;
        if (vetor[meio] == elemento) {
            return meio;
        }
        if (vetor[meio] < elemento) {
            inicio = meio + 1;
        } else {
            fim = meio - 1;
        }
    }
    return -1;
}

int main() {
    int vetor[MAX_SIZE];
    int tamanho, opcao, numero, posicao;

    do {
        printf("Digite o tamanho do vetor (entre 3 e 50): ");
        scanf("%d", &tamanho);
    } while (tamanho < 3 || tamanho > 50);

    printf("Digite %d numeros em ordem crescente:\n", tamanho);
    for (int i = 0; i < tamanho; i++) {
        scanf("%d", &vetor[i]);
    }

    do {
        printf("\nMenu:\n");
        printf("1. Imprimir vetor\n");
        printf("2. Consultar elemento\n");
        printf("3. Remover elemento\n");
        printf("4. Inserir elemento\n");
        printf("5. Sair\n");
        printf("Escolha uma opcao: ");
        scanf("%d", &opcao);

        switch (opcao) {
            case 1:
                imprimirVetor(vetor, tamanho);
                break;

            case 2:
                printf("Digite o elemento a procurar: ");
                scanf("%d", &numero);
                posicao = buscaBinaria(vetor, tamanho, numero);
                if (posicao != -1) {
                    printf("Elemento encontrado na posicao %d\n", posicao);
                } else {
                    printf("Elemento nao encontrado\n");
                }
                break;

            case 3:
                printf("Digite o elemento a remover: ");
                scanf("%d", &numero);
                posicao = buscaBinaria(vetor, tamanho, numero);
                if (posicao != -1) {
                    for (int i = posicao; i < tamanho - 1; i++) {
                        vetor[i] = vetor[i + 1];
                    }
                    tamanho--;
                    printf("Elemento removido com sucesso!\n");
                } else {
                    printf("Elemento nao encontrado\n");
                }
                break;

            case 4:
                if (tamanho >= MAX_SIZE) {
                    printf("Vetor cheio!\n");
                    break;
                }
                printf("Digite o elemento a inserir: ");
                scanf("%d", &numero);
                
                posicao = tamanho;
                while (posicao > 0 && vetor[posicao - 1] > numero) {
                    vetor[posicao] = vetor[posicao - 1];
                    posicao--;
                }
                vetor[posicao] = numero;
                tamanho++;
                printf("Elemento inserido com sucesso!\n");
                break;
        }
    } while (opcao != 5);

    return 0;
}


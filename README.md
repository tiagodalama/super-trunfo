# super-trunfo
#include <stdio.h>

// Definindo a estrutura da carta
typedef struct {
    char nome[50];
    char estado[30];
    int codigo;
    unsigned long int populacao;
    float area;
    float pib;
    int pontos_turisticos;
    float densidade_populacional;
    float pib_per_capita;
    float super_poder;
} Carta;

// Função para ler os dados da carta
void lerCarta(Carta *carta) {
    printf("Digite o nome da carta: ");
    fgets(carta->nome, 50, stdin);
    printf("Digite o estado da carta: ");
    fgets(carta->estado, 30, stdin);
    printf("Digite o codigo da carta: ");
    scanf("%d", &carta->codigo);
    printf("Digite a populacao (unsigned long int): ");
    scanf("%lu", &carta->populacao);
    printf("Digite a area (float): ");
    scanf("%f", &carta->area);
    printf("Digite o PIB (float): ");
    scanf("%f", &carta->pib);
    printf("Digite o numero de pontos turisticos (int): ");
    scanf("%d", &carta->pontos_turisticos);
    getchar(); // limpar buffer para próxima leitura de texto
}

// Função para calcular densidade populacional e PIB per capita
void calcularAtributos(Carta *carta) {
    if (carta->area != 0) {
        carta->densidade_populacional = (float)carta->populacao / carta->area;
    } else {
        carta->densidade_populacional = 0;
    }
    if (carta->populacao != 0) {
        carta->pib_per_capita = carta->pib / carta->populacao;
    } else {
        carta->pib_per_capita = 0;
    }
}

// Função para calcular o super poder da carta
void calcularSuperPoder(Carta *carta) {
    float inverso_densidade = 0;
    if (carta->densidade_populacional != 0) {
        inverso_densidade = 1.0f / carta->densidade_populacional;
    }
    // Somando todos os atributos, convertendo para float onde necessário
    carta->super_poder = (float)carta->populacao + carta->area + carta->pib +
                         (float)carta->pontos_turisticos + carta->pib_per_capita + inverso_densidade;
}

// Função para comparar as cartas e imprimir quem venceu cada atributo
void compararCartas(Carta c1, Carta c2) {
    printf("\nComparacao de Cartas:\n");

    // Populacao - maior vence
    int pop1 = (c1.populacao > c2.populacao) ? 1 : 0;
    printf("Populacao: Carta 1 venceu (%d)\n", pop1);

    // Area - maior vence
    int area1 = (c1.area > c2.area) ? 1 : 0;
    printf("Area: Carta 1 venceu (%d)\n", area1);

    // PIB - maior vence
    int pib1 = (c1.pib > c2.pib) ? 1 : 0;
    printf("PIB: Carta 1 venceu (%d)\n", pib1);

    // Pontos Turisticos - maior vence
    int pt1 = (c1.pontos_turisticos > c2.pontos_turisticos) ? 1 : 0;
    printf("Pontos Turisticos: Carta 1 venceu (%d)\n", pt1);

    // Densidade Populacional - menor vence
    int dens1 = (c1.densidade_populacional < c2.densidade_populacional) ? 1 : 0;
    printf("Densidade Populacional: Carta 1 venceu (%d)\n", dens1);

    // PIB per Capita - maior vence
    int pibpc1 = (c1.pib_per_capita > c2.pib_per_capita) ? 1 : 0;
    printf("PIB per Capita: Carta 1 venceu (%d)\n", pibpc1);

    // Super Poder - maior vence
    int sp1 = (c1.super_poder > c2.super_poder) ? 1 : 0;
    printf("Super Poder: Carta 1 venceu (%d)\n", sp1);
}

int main() {
    Carta carta1, carta2;

    printf("Digite os dados da Carta 1:\n");
    lerCarta(&carta1);
    calcularAtributos(&carta1);
    calcularSuperPoder(&carta1);

    printf("\nDigite os dados da Carta 2:\n");
    lerCarta(&carta2);
    calcularAtributos(&carta2);
    calcularSuperPoder(&carta2);

    compararCartas(carta1, carta2);

    return 0;
}

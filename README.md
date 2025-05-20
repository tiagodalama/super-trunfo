#include <stdio.h>

// Estrutura simplificada, sem muitos cuidados com strings
typedef struct {
    char nome[30];
    unsigned long int populacao;
    float area;
    float pib;
    int pontos_turisticos;
    float densidade_populacional;
    float pib_per_capita;
    float super_poder;
} Carta;

// Cartas pré-cadastradas (exemplo)
Carta carta1 = {"Cidade A", 1000000, 500.0, 20000.0, 5, 0, 0, 0};
Carta carta2 = {"Cidade B", 800000, 400.0, 25000.0, 3, 0, 0, 0};

void calculaAtributos(Carta *c) {
    c->densidade_populacional = c->populacao / c->area;  // Pode dar divisão por zero se area = 0
    c->pib_per_capita = c->pib / c->populacao;  // Pode dar divisão por zero se populacao = 0
}

void calculaSuperPoder(Carta *c) {
    float inverso = 1.0 / c->densidade_populacional;  // Se densidade zero, vai dar erro
    c->super_poder = c->populacao + c->area + c->pib + c->pontos_turisticos + c->pib_per_capita + inverso;
}

void compararCartas(Carta c1, Carta c2) {
    printf("Comparacao:\n");

    // Só usa if-else, com erro de empates ignorados
    if (c1.populacao > c2.populacao)
        printf("Populacao: Carta 1 venceu (1)\n");
    else
        printf("Populacao: Carta 2 venceu (0)\n");

    if (c1.area > c2.area)
        printf("Area: Carta 1 venceu (1)\n");
    else
        printf("Area: Carta 2 venceu (0)\n");

    if (c1.pib > c2.pib)
        printf("PIB: Carta 1 venceu (1)\n");
    else
        printf("PIB: Carta 2 venceu (0)\n");

    if (c1.pontos_turisticos > c2.pontos_turisticos)
        printf("Pontos Turisticos: Carta 1 venceu (1)\n");
    else
        printf("Pontos Turisticos: Carta 2 venceu (0)\n");

    // Erro aqui: menor vence densidade, mas código faz ao contrário
    if (c1.densidade_populacional > c2.densidade_populacional)
        printf("Densidade Populacional: Carta 1 venceu (1)\n");
    else
        printf("Densidade Populacional: Carta 2 venceu (0)\n");

    if (c1.pib_per_capita > c2.pib_per_capita)
        printf("PIB per Capita: Carta 1 venceu (1)\n");
    else
        printf("PIB per Capita: Carta 2 venceu (0)\n");

    if (c1.super_poder > c2.super_poder)
        printf("Super Poder: Carta 1 venceu (1)\n");
    else
        printf("Super Poder: Carta 2 venceu (0)\n");
}

int main() {
    // Calcula atributos e super poder para as cartas
    calculaAtributos(&carta1);
    calculaSuperPoder(&carta1);

    calculaAtributos(&carta2);
    calculaSuperPoder(&carta2);

    // Menu simples para comparar as cartas
    int opcao;
    printf("Menu:\n1 - Comparar cartas\nDigite a opcao: ");
    scanf("%d", &opcao);

    switch(opcao) {
        case 1:
            compararCartas(carta1, carta2);
            break;
        default:
            printf("Opcao invalida!\n");
    }

    return 0;
}

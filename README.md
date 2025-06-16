#include <stdio.h>
#include <stdlib.h>
#include <time.h>
#include <string.h>

#define TOTAL_CARTAS 4

// Estrutura da carta
typedef struct {
    char nome[30];
    int populacao;
    int area;
    float idh;
    int pib;
} Carta;

// Cartas disponíveis
Carta cartas[TOTAL_CARTAS] = {
    {"São Paulo", 12300000, 1521, 0.805, 55000},
    {"Rio de Janeiro", 6748000, 1182, 0.799, 47000},
    {"Curitiba", 1963000, 430, 0.823, 45000},
    {"Salvador", 2887000, 693, 0.759, 31000}
};

// Função para mostrar carta
void mostrarCarta(Carta c) {
    printf("\n🃏 Cidade: %s\n", c.nome);
    printf("População: %d\n", c.populacao);
    printf("Área: %d km²\n", c.area);
    printf("IDH: %.3f\n", c.idh);
    printf("PIB per capita: %d\n", c.pib);
}

int main() {
    srand(time(NULL)); // Inicializa semente aleatória

    int indiceJogador = rand() % TOTAL_CARTAS;
    int indiceComputador;

    // Evita que o computador tenha a mesma carta
    do {
        indiceComputador = rand() % TOTAL_CARTAS;
    } while (indiceComputador == indiceJogador);

    Carta jogador = cartas[indiceJogador];
    Carta computador = cartas[indiceComputador];

    // Mostra a carta do jogador
    printf("\n🃏 Sua carta:\n");
    mostrarCarta(jogador);

    // Escolha do atributo
    char atributo[20];
    printf("\nEscolha um atributo (populacao, area, idh, pib): ");
    scanf("%s", atributo);

    // Resultado
    float valorJogador, valorComputador;

    if (strcmp(atributo, "populacao") == 0) {
        valorJogador = jogador.populacao;
        valorComputador = computador.populacao;
    } else if (strcmp(atributo, "area") == 0) {
        valorJogador = jogador.area;
        valorComputador = computador.area;
    } else if (strcmp(atributo, "idh") == 0) {
        valorJogador = jogador.idh;
        valorComputador = computador.idh;
    } else if (strcmp(atributo, "pib") == 0) {
        valorJogador = jogador.pib;
        valorComputador = computador.pib;
    } else {
        printf("Atributo inválido.\n");
        return 1;
    }

    printf("\n💻 Carta do computador:\n");
    mostrarCarta(computador);
    printf("\n🔍 Comparando atributo \"%s\"...\n", atributo);

    if (valorJogador > valorComputador)
        printf("🎉 Você venceu!\n");
    else if (valorJogador < valorComputador)
        printf("💻 O computador venceu!\n");
    else
        printf("🤝 Empate!\n");

    return 0;
}

# Matriz-de-Adjacencia
Este sistema interativo em C gerencia grafos não direcionados usando Matriz de Adjacência. O software possui um menu para limpar a matriz, inserir e remover arestas simetricamente (usando bits 1 e 0), exibir a matriz alinhada, calcular o grau dos vértices e listar as adjacências. Testado com 6 vértices e 7 arestas para garantir robustez.

#include <stdio.h>

#include <stdlib.h>

#define MAX_VERTICES 100

int graph[MAX_VERTICES][MAX_VERTICES];
int num_vertices;

void limparGrafo(){
    for(int i = 0; i < num_vertices; i++)
    {
        for(int j = 0; j < num_vertices; j++) 
        {
            graph[i][j] = 0;   
        }
    }    
    printf("\nGrafo limpo com sucesso!\n");
}

void imprimirMatriz()
{
    printf("\nMatriz de Adjacencia\n");
    
    printf("    ");
    for(int i = 0; i < num_vertices; i++)
    {
        printf("%2d ", i);
    }
    
    printf("\n");
    
    for(int i = 0; i < num_vertices; i++)
    {
        printf("%2d | ", i);
        for(int j = 0; j < num_vertices; j++)
        {
            printf("%2d ", graph[i][j]);
        }
        printf("\n");
    }
}

void modificaAresta()
{
    int origem, destino, opcao_aresta;
    printf("\nVértice de origem: ");
    scanf("%d", &origem);
    
    printf("Vértice de destino: ");
    scanf("%d", &destino);
    
    if(origem < 0 || origem >= num_vertices || destino < 0 || destino >= num_vertices)
    {
        printf("Vértices inválidos!\n");
        return;
    }
    
    printf("1 - Adicionar aresta\n");
    printf("2 - Remover aresta\n");
    printf("Opção: ");
    scanf("%d", &opcao_aresta);
    
    if (opcao_aresta == 1) {
        graph[origem][destino] = 1;
        graph[destino][origem] = 1;
        printf("Aresta adicionada com sucesso!\n");
    } else if (opcao_aresta == 2) {
        graph[origem][destino] = 0;
        graph[destino][origem] = 0;
        printf("Aresta removida com sucesso!\n");
    } else {
        printf("Opção inválida! Nenhuma alteração foi feita.\n");
    }
}

void calcularGraus()
{
    int grau;
    printf("\nGRAU DOS VÉRTICES\n\n");
    
    for(int i = 0; i < num_vertices; i++)
    {
        grau = 0;
        for(int j = 0; j < num_vertices; j++)
        {
            grau += graph[i][j];
        }
        printf("Vértice %d -> Grau %d\n", i, grau);
    }
}

void listarAdjacencias()
{
    printf("\nLISTA de ADJACÊNCIAS\n");
    
    for(int i = 0; i < num_vertices; i++)
    {
        printf("%d -> ", i);
        int vazio = 1;
        
        for(int j = 0; j < num_vertices; j++)
        {
            if(graph[i][j] == 1)
            {
                printf("%d ", j);
                vazio = 0;
            }
        }
        if(vazio == 1)
        {
            printf("Nenhum");
        }
        printf("\n");
    }
}

int main()
{
    int opcao;
    
    printf("Quantidade de vértices: ");
    scanf("%d", &num_vertices);
    
    if(num_vertices <= 0 || num_vertices > MAX_VERTICES)
    {
        printf("Quantidade inválida!\n");
        return 0;
    }
    
    limparGrafo();
    
    do
    {
        printf("\n=== MENU DO GRAFO ===\n");
        printf("1 - Limpar grafo\n");
        printf("2 - Inserir/remover aresta\n");
        printf("3 - Mostrar matriz\n");
        printf("4 - Mostrar graus\n");
        printf("5 - Mostrar adjacências\n");
        printf("6 - Sair\n");
        printf("Opção: ");
        scanf("%d", &opcao);
        
        switch(opcao)
        {
            case 1:
                limparGrafo();
                break;
            case 2:
                modificaAresta();
                break;
            case 3:
                imprimirMatriz();
                break;
            case 4:
                calcularGraus();
                break;
            case 5:
                listarAdjacencias();
                break;
            case 6:
                printf("\nPrograma encerrado!\n");
                break;
            default:
                printf("Opção inválida!\n");
        }
    } while(opcao != 6);

    return 0;
}

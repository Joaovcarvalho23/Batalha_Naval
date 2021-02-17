#include <stdio.h>
#include <stdlib.h>
#include <time.h>
#include <string.h>

#define TAM_MAX_TABULEIRO 8 //8x8

#define QTD_MAX_EMB_PEQUENAS 1
#define QTD_MAX_EMB_VERTICAL 1
#define QTD_MAX_EMB_SUBINDO_LADEIRA 1 // '/'
#define QTD_MAX_EMB_DESCENDO_LADEIRA 1 // '\'


int main()
{
    char jogador_1, jogador_2;
    char nome_jogador_1[50], nome_jogador_2[50];
    int placar_jogador_1, placar_jogador_2;
    int jogo = 1;
    int vez = 1;

    srand(time(NULL)); 

    printf("\n**BATALHA NAVAL**\n\n");

    //regras
    printf("#REGRAS#");
    printf("\n1. O principal objetivo do jogo é afundar todos os barcos inimigos!;\n");
    printf("\n2. Você deve informar a localização (linha e coluna) para tentar afundar algum barco inimigo;\n");
    printf("\nOBS1: barcos pequenos só ocupam uma posição e mostra o valor (X) quando é acertado;\n");
    printf("\nOBS2: barcos grandes ocupam duas posições, podendo ser horizontal, vertical e diagonal\n");
    
    printf("\n\nDigite o nome do jogador 1: ");
    fgets(nome_jogador_1, 50, stdin);
    printf("\n\nDigite o nome do jogador 2: ");
    fgets(nome_jogador_2, 50, stdin);
    printf("\n\n");

    //montando o jogo
    char area[TAM_MAX_TABULEIRO][TAM_MAX_TABULEIRO];
    int restantes = 7;
    int barco_grande;
    int lin, col;

    //área do jogo
    int area_inimiga[TAM_MAX_TABULEIRO][TAM_MAX_TABULEIRO] =
        {                   
            {0, 0, 0, 0, 0, 0, 0, 0},
            {0, 0, 0, 0, 0, 0, 0, 0}, 
            {0, 0, 0, 0, 0, 0, 0, 0}, 
            {0, 0, 0, 0, 0, 0, 0, 0}, 
            {0, 0, 0, 0, 0, 0, 0, 0}, 
            {0, 0, 0, 0, 0, 0, 0, 0},
            {0, 0, 0, 0, 0, 0, 0, 0},
            {0, 0, 0, 0, 0, 0, 0, 0}
        };

    //desenhando a área do jogo
    for (int lin = 0; lin < TAM_MAX_TABULEIRO; lin++)
    {
        for (int col = 0; col < TAM_MAX_TABULEIRO; col++)
        {
            area[lin][col] = '*';
            printf(" %c ", area[lin][col]);
        }
        printf("\n");
    }

    //Randomização das embarcações pequenas
    for (int a = 0; a < QTD_MAX_EMB_PEQUENAS; a++) 
    {
        int pos_linha, pos_coluna;
        
        do
        {
            pos_linha = rand() % (TAM_MAX_TABULEIRO - 1) + 1;
            pos_coluna = rand() % (TAM_MAX_TABULEIRO - 1) + 1;

        } while (area_inimiga[pos_linha][pos_coluna] != 0);
        area_inimiga[pos_linha][pos_coluna] = 1;
    }

    //Randomização das embarcações verticais
    for (int a = 0; a < QTD_MAX_EMB_VERTICAL; a++)
    {
        int pos_linha, pos_coluna;
        
        do 
        {
            pos_linha = rand() % (TAM_MAX_TABULEIRO - 1);
            pos_coluna = rand() % (TAM_MAX_TABULEIRO - 1) + 1;

        } while (((area_inimiga[pos_linha][pos_coluna] < 1) || (area_inimiga[pos_linha + 1][pos_coluna] < 1)) && (area_inimiga[pos_linha][pos_coluna] != 0));
        area_inimiga[pos_linha][pos_coluna] = 2;
        area_inimiga[pos_linha+1][pos_coluna] = 2;
    }

    //Randomização das embarcações de subida 
    for (int a = 0; a < QTD_MAX_EMB_SUBINDO_LADEIRA; a++) 
    {
        int pos_linha, pos_coluna;
        
        do 
        {
            pos_linha = rand() % (TAM_MAX_TABULEIRO - 2);
            pos_linha += 1;
            pos_coluna = rand() % (TAM_MAX_TABULEIRO - 1);

        } while (((area_inimiga[pos_linha][pos_coluna] < 2) || (area_inimiga[pos_linha - 1][pos_coluna + 1] < 2)) && (area_inimiga[pos_linha][pos_coluna] != 0));
        area_inimiga[pos_linha][pos_coluna] = 3;
        area_inimiga[pos_linha-1][pos_coluna+1] = 3;
    }

    //Randomização das embarcações de descida
    for (int a = 0; a < QTD_MAX_EMB_DESCENDO_LADEIRA; a++) 
    {
        int pos_linha, pos_coluna;
        
        do 
        {
            pos_linha = rand() % (TAM_MAX_TABULEIRO - 1);
            pos_coluna = rand() % (TAM_MAX_TABULEIRO - 1);

        } while (((area_inimiga[pos_linha][pos_coluna] < 3) || (area_inimiga[pos_linha+1][pos_coluna+1] < 3)) && (area_inimiga[pos_linha][pos_coluna] != 0));
        area_inimiga[pos_linha][pos_coluna] = 4;
        area_inimiga[pos_linha+1][pos_coluna+1] = 4;
    }

    for (int i = 0; i < TAM_MAX_TABULEIRO; i++) 
    {
        for (int j = 0; j < TAM_MAX_TABULEIRO; j++) 
        {
            printf(" %i ",area_inimiga[i][j]);
        }
        printf("\n");
    }

    printf("\n");
    printf("\n");
    
    
    while(jogo == 1)
    {
      while(vez == 1)
      {
        while (restantes != 0)
        {
        //tentativas para jogar
        printf("\nJogador %s", nome_jogador_1);
        printf("\nEmbarcações restantes: %i\n", restantes);
        printf("Digite uma linha (0 - 7): ");
        scanf("%i", &lin);
        getchar();
        printf("Agora digite uma coluna (0 - 7): ");
        scanf("%i", &col);
        getchar();

        printf("\n\n");

        //configurando quando acerta e quando erra
        if (lin < TAM_MAX_TABULEIRO && lin >= 0 && col < TAM_MAX_TABULEIRO && col >= 0 && area[lin][col] == '*')
        {
          switch (area_inimiga[lin][col])
          {
           case 0:
                area[lin][col] = ' ';
                printf("Você errou.\n\n");
                break;

           case 1:
                area[lin][col] = 'X';
                restantes--;
                printf("Você acertou o barco pequeno!\n\n");
                break;

           case 2:
                area[lin][col] = 124;
                restantes--;
                if (barco_grande == 3)
                {
                    barco_grande = 0;
                }
                break;

           case 3:
                area[lin][col] = 47;
                restantes--;
                if (barco_grande == 3)
                {
                    barco_grande = 0;
                }
                break;

           case 4:
                area[lin][col] = 92;
                restantes--;
                if (barco_grande == 3)
                {
                    barco_grande = 0;
                }

                else
                {
                    barco_grande += 1;
                }
                printf("Você acertou o barco grande!\n\n");
                break;

           default:
                printf("Você errou\n");
            }
        }

        //desenho da área após acertar ou errar
        for (int lin = 0; lin < TAM_MAX_TABULEIRO; lin++)
        {
            for (int col = 0; col < TAM_MAX_TABULEIRO; col++)
            {
                printf(" %c ", area[lin][col]);
            }
            printf("\n");
        }

        
        }
        vez = 2;
      }
    

      while(vez == 2)
      {
        while (restantes != 0)
        {
        //tentativas para jogar
        printf("\nJogador %s", nome_jogador_2);
        printf("\nEmbarcações restantes: %i\n", restantes);
        printf("Digite uma linha (0 - 7): ");
        scanf("%i", &lin);
        getchar();
        printf("Agora digite uma coluna (0 - 7): ");
        scanf("%i", &col);
        getchar();

        printf("\n\n");

        //configurando quando acerta e quando erra
         if (lin < TAM_MAX_TABULEIRO && lin >= 0 && col < TAM_MAX_TABULEIRO && col >= 0 && area[lin][col] == '*')
         {
            switch (area_inimiga[lin][col])
            {
             case 0:
                  area[lin][col] = ' ';
                  printf("Você errou.\n\n");
                  break;

             case 1:
                  area[lin][col] = 'X';
                  restantes--;
                  printf("Você acertou o barco pequeno!\n\n");
                  break;

             case 2:
                  area[lin][col] = 124;
                  restantes--;
                  if (barco_grande == 3)
                  {
                    barco_grande = 0;
                  }
                  break;

             case 3:
                  area[lin][col] = 47;
                  restantes--;
                  if (barco_grande == 3)
                  {
                    barco_grande = 0;
                  }
                  break;

             case 4:
                  area[lin][col] = 92;
                  restantes--;
                  if (barco_grande == 3)
                  {
                    barco_grande = 0;
                  }

                  else
                  {
                    barco_grande += 1;
                  }
                  printf("Você acertou o barco grande!\n\n");
                  break;

            default:
                printf("Você errou\n");
            }
         }

        //desenho da área após acertar ou errar
         for (int lin = 0; lin < TAM_MAX_TABULEIRO; lin++)
         {
            for (int col = 0; col < TAM_MAX_TABULEIRO; col++)
            {
                printf(" %c ", area[lin][col]);
            }
            printf("\n");
         }
        }
         vez = 1;
      }
      
    
    }
    //final do jogo
        if (restantes == 0)
        {
            printf("**FIM DE JOGO**");
            
            placar_jogador_1 = placar_jogador_1 + 1;
            placar_jogador_2 = placar_jogador_2 + 1;
            
            if(placar_jogador_1 > placar_jogador_2)
            {
              printf("O jogador 1 com o nome de %s ganhou!", nome_jogador_1);
            }

            else if(placar_jogador_1 < placar_jogador_2)
            {
              printf("O jogador 2 com o nome de %s ganhou!", nome_jogador_2);
            }
        }
}

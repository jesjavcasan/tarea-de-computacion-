# tarea-de-computacion-
esta es la tarea realizada por: jesus castro, robert velaz y eduardo jaime para computación l con el profesor Orlando Becerra
este es el codigo fuente del juego


#include <stdio.h>

#include <stdlib.h

#include <time.h

#include <conio.h

#include <windows.h>
 
void wait(int seconds)
{

    clock_t endwait;
    
    endwait = clock() + seconds * CLOCKS_PER_SEC;
    
    while( clock() < endwait ){}
}
 
void imprimir();

void iniciar();
 
int i, j, k, jugador[6][10], oponente[6][10], opcion1, opcion2, puntajejugador = 0, puntajeoponente = 0; 

time_t start,end;

double dif, tiempototal=0;
 

void imprimir()
{  
    printf("\t\t\t\t\t    Tiempo transcurrido = %.1f segundos\n\n", tiempototal);
     
    for(i = 1 ; i <= 5 ; i++) 
    {
        printf("\n\t");
        
		for(j = 1 ; j <= 9 ; j++)
        {
            if(oponente[i][j] == 3){
                
				printf("  #");
            }
            else{
                
				if(oponente[i][j] == 2){
					
                    printf("  X");
                }
                else{
                	
                    printf("  -");
                }
            }                                    
        }
        if(i == 3){
        	
            printf("\tOPONENTE");
        }
        else{
        	
            if(i == 1){
            	
                printf("\t\t\tPuntaje oponente: %d", puntajeoponente);
            }
        }
    }
     
    printf("\n\n\t_____________________________\n\n");
     
    for(i = 1 ; i <= 5 ; i++)
    {
        printf("\n\t");
        for(j = 1 ; j <= 9 ; j++)
        {
            if(jugador[i][j] == 3){
            	
                printf("  #");
            }
            else{
            	
                if(jugador[i][j] == 2){
                	
                    printf("  X");
                }
                else
                {
                    if(jugador[i][j]==1)
                    {
                        printf("  O");
                    }
                    else
                    {
                        printf("  -");
                    }
                }
            }                                    
        }
        if(i == 3)
        {
            printf("\tJUGADOR");
        }
        else
        {
            if(i == 1)
            {
                printf("\t\t\tPuntaje jugador: %d", puntajejugador);
            }
        }
    }
 
    printf("\n\n");  
}
 
void iniciar()
{
         
    for(i = 1 ; i <= 5 ; i++){
    	
        for(j = 1 ; j <= 9 ; j++){
        	
            jugador[i][j]=0;
            oponente[i][j]=0;
        }
    }
     
    printf("\n\n Dame las coordenadas de tus barcos~\n\n");
     
    srand(time(NULL));
    for(k= 1 ; k <= 10; k++) 
    {
        imprimir();
                       
        i=1+rand() % 5;
        j=1+rand() % 9;
        while(oponente[i][j] == 1){
        	
            i = 1 + rand() % 5; j = 1 + rand() % 9;
        }
        oponente[i][j]=1;
                       
        printf("\n\tX%d = ", k);
        scanf("%d", &opcion2);
        while(opcion2 < 1 || opcion2 > 9){
        	
            printf("    Escoje un valor valido ( 1 a 9 )\n\n\tX%d = ", k);
            scanf("%d", &opcion2);
        }
                         
        printf("\n\tY%d = ", k);
        scanf("%d", &opcion1);
        while(opcion1 < 1 || opcion1 > 5){
        	
            printf("\n    Escoje un valor valido ( 1 a 5 )\n\n\tY%d = ", k);
            scanf("%d", &opcion1);
        }
                         
        if(jugador[opcion1][opcion2] == 1)
        {
            printf("\n Ese valor ya existe...");
            getche();
            k=k-1;
        }
        jugador[opcion1][opcion2] = 1;
                       
        system("cls");
                                                         
    }  
     
}
 
main() 
{
    int res, auxiliar, probabilidadcpu, destruidosoponente=0, destruidosjugador=0, ganador;
    float dificultadcpu=0.5;
     
    system("color 1A");
 
    printf("\n\n\t                BATTLESHIP \n");
	
    printf ("                        __________");
    printf ("\n                       /  |      |");
    printf ("\n                      /   |      |");
    printf ("\n                     /    |      |        ");
    printf ("\n                    /     |      |");
    printf ("\n                   /      |      |");
    printf ("\n                  /_______|______|");
    printf ("\n         _________________|_____________");
    printf ("\n        /                              |");
    printf ("\n       /  ººº ººº ººº ººº ººº ººº ººº  |");
    printf ("\n      / ººººº ºººº ºººº ºººº ºººº ºººº |");
    printf ("\n     /_________________________________|");
    printf ("\n\n\n\t           1- JUGAR");
    printf ("\n\t           2- SALIR");
    printf ("\n\n\n\t           DAME TU OPCION: ");
    scanf("%d", &res);
    system("cls");
       
    switch(res){ 
       
       case 1:
       {
           iniciar(); 
           printf("\n\n\n\t\t LISTO(A)?\n\n");
           wait(2);
           printf("\n\t\t YA!!!");
           wait(1);
                             
           do
           {
               time(&start);
               system("cls"); 
                               
               imprimir();
                               
               printf(" ES TU TURNO, DAME LA POSICION PARA ATACAR!\n\n");
               printf("\tX = ");
               scanf("%d", &opcion2);
               while(opcion2 < 1 || opcion2 > 9){
               	
                   printf("\n    ESCOJE UN VALOR VALIDO ( 1 a 9 )\n\n\tX = ");
                   scanf("%d", &opcion2);
               }
                               
               printf("\tY = ");
               scanf("%d", &opcion1);
               while(opcion1 < 1 || opcion1 > 5){
               	
                   printf("\n    ESCOJE UN VALOR VALIDO ( 1 a 5 )\n\n\tY = ");
                   scanf("%d", &opcion1);
               }
                               
               auxiliar=oponente[opcion1][opcion2];
               oponente[opcion1][opcion2]=3;
               system("cls");
               imprimir();
               oponente[opcion1][opcion2]=auxiliar;                          
                               
               if(oponente[opcion1][opcion2] == 1) {
               	
                   oponente[opcion1][opcion2]=2;
                   destruidosoponente=destruidosoponente+1;
                   puntajejugador=puntajejugador+200;
                   printf("\n LE DISTE!!\n\n");
               }
               else
               {
                   printf("\n FALLLASTE...\n\n");
               }
                               
               system("PAUSE");
               system("cls");
               if(destruidosoponente == 10)
               {
                   printf("\n\n\n\n\t\t\t FELICIDADES, GANASTE!!");
                   getche();
               }                                                                
               imprimir();
                               
               printf(" LE TOCA AL OPONENTE!\n\n");
               wait(2);
                               
               dificultadcpu=dificultadcpu+0.1;
                               
               srand(time(NULL));
                               
               probabilidadcpu = rand() % 5;
                               
               if(probabilidadcpu > dificultadcpu)
               {
                   i = 1 + rand() % 5;
                   j = 1 + rand() % 9;
                   while(jugador[i][j]==2)
                   {
                       i = 1 + rand() % 5 ; j = 1 + rand() % 9;
                   }
                   auxiliar = jugador[i][j];
               }
               else
               {
                   while(jugador[i][j]==2 || jugador[i][j]!=1)
                   {
                       i=1+rand()%5; j=1+rand()%9;
                   }
                   auxiliar=jugador[i][j];
               }              
                               
               jugador[i][j] = 3;
               opcion1 = i;
               opcion2 = j;
               system("cls");
               imprimir();
               jugador[opcion1][opcion2] = auxiliar;
                               
               if(jugador[opcion1][opcion2] == 1)
               {
                   printf("\n El oponente ha acertado!!\n\n");
                   jugador[opcion1][opcion2] = 2;
                   destruidosjugador = destruidosjugador + 1;
                   puntajeoponente = puntajeoponente + 200;
               }
               else
               {
                   printf("\n EL OPONENTE FALLO, TE SALVASTE...\n\n");
               }
               if(destruidosjugador == 10)
               {    
                   system("cls");                                                
                   printf("\n\n\n\n\t\t\t JAJAJA, PERDISTE!!");
                   getche();
               }
               system("PAUSE");
               if(destruidosoponente == 10 || destruidosjugador == 10)
               {
                   destruidosoponente = 10 ; destruidosjugador = 10;
               }
               time(&end);
               dif = difftime (end,start);
               tiempototal=tiempototal+dif;
               if(tiempototal > 600)
               {
                   system("cls");
                   printf("\n\n\n\t\t SE ACABO EL TIEMPO... PERDISE :C!!");
                   getche();
               }
           }
           while(destruidosoponente < 10 || destruidosjugador < 10);
       }
                               
    } 
                 
}

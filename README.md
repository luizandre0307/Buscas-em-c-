#include <stdlib.h>
#include <stdio.h>

#define VECTOR_SIZE 1001

int comparacao_bi_recurciva=0;

int busca_linear (int vector[VECTOR_SIZE], int item){
    int i;
    int comparacao_sequencial=0;
	for (i = 1; i < VECTOR_SIZE; i++) {
		comparacao_sequencial++;
        if (vector[i] == item) {
        	//return i;
            return comparacao_sequencial;
        }
    }
    return -1; //numero não encontrado
}

int busca_binaria_recursiva(int vector[VECTOR_SIZE], int begin, int end, int item){
    int i = (begin + end) / 2;
    
	if (begin > end) {
        return -1; //numero não encontrado
    }

    if (vector[i] == item){
	   	comparacao_bi_recurciva++;
		return comparacao_bi_recurciva;
    	
    }
    else {
    	if (item < vector[i]){
			comparacao_bi_recurciva++;
        	return busca_binaria_recursiva(vector, begin, i - 1, item);
    	}
        else {
        	comparacao_bi_recurciva++;
        	return busca_binaria_recursiva(vector, i + 1, end, item);
		}
    }
}

int busca_binaria_interativa(int vector[VECTOR_SIZE], int item){
    int begin = 1;
    int end = VECTOR_SIZE - 1;
	int comparacao_bi_interativa=0;
    while (begin <= end) {  
		comparacao_bi_interativa++;
		int i = (begin + end) / 2;  
		
        if (vector[i] == item) {  
        	return comparacao_bi_interativa;
            break;
			
        }
        if (vector[i] < item) {  
            begin = i + 1;
        } else {  
            end = i - 1;
        }
    }

    return -1; //numero não encontrado
}

int buscaTabelaFrequencia(int vector[VECTOR_SIZE], int item){
	int freq[1001];
	int i;
	for (i = 1; i < VECTOR_SIZE; i++){
		freq[i] = 0;
	}	
	for (i = 1; i < VECTOR_SIZE; i++){
			freq[vector[i]]++;
	}
	for (i = 1; i < VECTOR_SIZE; i++){
		printf("\t\t\t\t a frequencia do numero %d   e %d\n", vector[i], freq[i]);
	}
	return freq[item];
	
}

int main (){
	int vector[VECTOR_SIZE];
	int i;
	for (i = 1; i < VECTOR_SIZE; i++) {
		vector[i] = i;
	}
	int opcao, item;
	
	
    do {
		printf("digite o valor a ser encontrado : ");
		scanf("%d", &item);

        printf("Busca sequencial do numero		%d= %d\n", item, 
                busca_linear(vector, item));

        printf("Busca binaria recursiva do numero	%d= %d\n", item,
                busca_binaria_recursiva(vector, 1, VECTOR_SIZE - 1, item));
                
        comparacao_bi_recurciva = 0;

        printf("Busca binaria interativa do numero	%d= %d\n", item,
                busca_binaria_interativa(vector, item));
                
        printf("Busca tabela frequencia do numero	%d= %d\n", item,
                buscaTabelaFrequencia(vector, item));        

        printf("\n0 - Sair\n1 - Nova Busca\n");
        scanf("%d", &opcao);
    }while (opcao != 0);

    return EXIT_SUCCESS;
}

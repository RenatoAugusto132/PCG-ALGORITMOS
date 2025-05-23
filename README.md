# PCG-ALGORITMOS
escalonamento de tarefas diárias utilizando round robin 

    #include <stdio.h>
    #include <string.h>

    #define quantum 15
    #define MAX 5

    typedef struct {
    char nome[15];
    int restante;
    int concluida;
    } Tarefa;

    void escalonador(Tarefa tarefas[], int n) {
    int total = 0;
    int tarefas_concluidas = 0;

    printf("\nIniciando escalonamento com quantum = %d\n", quantum);
    printf("\n");

    while (tarefas_concluidas < n) {
        for (int i = 0; i < n; i++) {
            if (tarefas[i].concluida)
                continue;

            printf("Executando tarefa: %s\n", tarefas[i].nome);

            if (tarefas[i].restante > quantum) {
                tarefas[i].restante -= quantum;
                total += quantum;
                printf(" %s ainda precisa de %d minutos\n", tarefas[i].nome, tarefas[i].restante);
                printf("\n");
            } else {
                total += tarefas[i].restante;
                printf("-> %s concluído(a) em %d minutos\n", tarefas[i].nome, total);
                printf("\n");
                tarefas[i].restante = 0;
                tarefas[i].concluida = 1;
                tarefas_concluidas++;
            }
        }
    }

    printf("\nTodas as tarefas foram concluidas em %d minutos.\n", total);
    }

    int main() {
    int n;
    Tarefa tarefas[MAX];

    printf("Quantas tarefas deseja adicionar? (maximo %d): ", MAX);
    scanf("%d", &n);

    if (n < 1 || n > MAX) {
        printf("Número inválido de tarefas.\n");
        return 1;
    }

    for (int i = 0; i < n; i++) {
        printf("\nDigite o nome da tarefa %d: ", i + 1);
        scanf("%s", tarefas[i].nome);
        printf("Digite o tempo estimado (em minutos) para a tarefa %s: ", tarefas[i].nome);
        scanf("%d", &tarefas[i].restante);
        tarefas[i].concluida = 0;
    }

    escalonador(tarefas, n);

    return 0;
    }

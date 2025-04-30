# Processos

## Código Fonte x Programa x Processo

### Código Fonte
- Arquivo de texto com instruções escritas em uma linguagem de programação.
- Descreve o que o programa deve fazer.
- Legível para humanos.
- Precisa ser **compilado** ou **interpretado** para se transformar em um programa executável.

### Programa
- Conjunto de instruções que podem ser executadas por um computador.
- Traduzido para linguagem de máquina (binário).
- **Estático**: não muda durante a execução.
- Pode ser executado várias vezes, originando diferentes processos.

#### Analogia:
> O programa é a **receita**, enquanto o processo é a **execução real da receita**.

#### Componentes do Programa
- Código compilado
- Dados estáticos (como variáveis globais)
- Estrutura de controle

#### Partes de um Programa
- Endereço de Hardware
- Endereço de Software
- Espaço de Endereçamento:
  - `PID` (Process ID)
  - `UID` (User ID)
  - Registradores
  - Prioridade
  - Stack (pilha)
  - Heap (memória dinâmica)

---

## Processo

- Uma **instância** de um programa em execução.
- Dinâmico, possui um ciclo de vida.
- Possui estado, espaço de memória, e recursos atribuídos.

### Estados de um Processo
- `New`: processo recém-criado.
- `Ready`: pronto para ser executado.
- `Running`: em execução.
- `Blocked`: aguardando evento ou recurso.
- `Exit`: finalizado.

> Apenas um processo pode estar em **estado "Running"** por CPU.

### Recursos associados a um processo:
- CPU
- Memória
- Arquivos abertos
- Dispositivos de E/S
- Registradores da CPU

---

## Criação de Processos

- Criados por outros processos (`fork`, `spawn`, `exec`).
- Pode ser iniciado pelo próprio sistema operacional durante o boot.
- Exemplo no Linux: o processo `init` ou `systemd` é o "pai de todos".

### Etapas de criação:
1. Alocação de espaço na memória.
2. Atribuição de identificadores (PID, UID).
3. Inicialização de estruturas de dados internas (PCB).
4. Inclusão na fila de processos prontos.

---

## Ciclos de um Processo

### Classificação:
- **CPU-bound**: uso intensivo de processamento.
- **I/O-bound**: espera frequente por dispositivos de entrada/saída.

> O sistema operacional gerencia a alternância entre os dois tipos para otimizar desempenho.

---

## Bloco de Controle de Processo (PCB)

Estrutura que contém:
- PID
- Estado do processo
- Contador de programa
- Registradores
- Informações de escalonamento
- Informações de E/S
- Ponteiros para memória

---

## Planos de Execução

- **Foreground** (primeiro plano):
  - Controlado diretamente pelo usuário (ex: terminal).
- **Background** (segundo plano):
  - Executa tarefas auxiliares ou automáticas.
  - Chamados de **daemons** (Linux) ou **serviços** (Windows).

---

## Término de Processos

### Motivos:
- Execução finalizada com sucesso.
- Erro intencional detectado (ex: divisão por zero).
- Erro inesperado (ex: acesso a área proibida de memória).
- Interrupção externa (comando `kill`, desligamento).

> O sistema operacional libera todos os recursos alocados após o término.

---

## Relação entre Processos

### Linux / UNIX
- Processos possuem hierarquia (pai → filho).
- Agrupados em **grupos de processos** e **sessões**.
- Comando `ps` mostra a árvore de processos.

### Windows
- Não possui hierarquia rígida.
- Todos os processos são tratados de forma independente.

---

## Escalonamento de Processos

- O SO escolhe qual processo será executado a seguir.
- Critérios: prioridade, tempo de espera, tipo (I/O ou CPU-bound).

### Algoritmos comuns:
- FIFO (First In, First Out)
- Round Robin
- Shortest Job First
- Multilevel Queue

---

## Chaveamento de Processos

### Quando ocorre:
- Final de fatia de tempo da CPU (clock interrupt)
- Solicitação de E/S
- Falta de memória
- Chamadas de sistema
- **Trap**:
  - Sinal de interrupção gerado por software para troca de processo.

---

## Troca de Contexto

- Ocorre quando o SO troca o processo em execução.
- Salva o contexto do processo atual (PC, registradores, etc.).
- Restaura o contexto do próximo processo.

> **Overhead**: tempo gasto sem executar código útil.

---

## Retorno de um Processo

- Processo pode retornar:
  - Código de sucesso (`exit 0`)
  - Código de erro (`exit 1`, `exit -1`, etc.)
  - Sinais de falha ou interrupção

> Sistemas operacionais e linguagens usam esses códigos para identificar o que ocorreu na execução.

---

## Papel do Sistema Operacional

- Gerencia e monitora todos os processos ativos.
- Aloca recursos e garante isolamento entre processos.
- Coordena o acesso ao hardware e dispositivos de E/S.
- Armazena informações dos processos em estruturas internas.
- Responsável por segurança, permissões, e estabilidade do sistema.

---

## Comandos úteis (Linux)

```bash
ps aux         # Lista todos os processos
top            # Monitoramento em tempo real
kill PID       # Envia sinal para encerrar processo
nice / renice  # Altera prioridade de um processo
fork()         # Criação de processo filho
exec()         # Substituição de processo

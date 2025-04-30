# Processos

## Código Fonte x Programa x Processo

### Código Fonte
- Arquivo de texto.
- Instruções do que o programa deve fazer.
- Legível para humanos.

### Programa
- Conjunto de instruções em linguagem de máquina (não legível para humanos).
- Pode existir mais de um processo executando o mesmo programa.
- Analogamente, são como **receitas em um restaurante** — estáticas e seguidas.
- Um processo pode chamar outros processos.

#### Partes de um Programa
- Endereço de Hardware.
- Endereço de Software.
- Espaço de Endereçamento:
  - `PID` (Process ID)
  - `UID` (User ID)
  - Registradores
  - Prioridade

### Processo
- Possui diferentes estados: execução, finalizado, pausa, etc.
- Comparável aos **pratos em um restaurante**, que podem estar em preparo, prontos, etc.

---

## Criação de Processos
- O sistema operacional pode iniciar e executar processos automaticamente.
- Outros processos são criados:
  - Durante a inicialização
  - Por chamadas de sistema
  - Por solicitação do usuário

---

## Ciclos de um Processo

- **CPU-bound**: usa intensivamente o processador.
- **I/O-bound**: usa intensivamente operações de entrada e saída (rede, disco, memória, etc).

---

## Bloco de Controle de Processo (PCB - Process Control Block)

### Execução em Diferentes Planos
- **Foreground (Primeiro plano)**:
  - Executa os programas dos usuários.
- **Background (Segundo plano)**:
  - Tarefas do sistema (ex: serviços como SSH, impressão, email).
  - Também chamados de **daemons** (ou "deimons").

---

## Término de um Processo

- Saída normal (voluntária) — sucesso.
- Saída por erro (voluntária) — erro conhecido/esperado.
- Saída por erro (involuntária) — exceções, execução ilegal.
- Cancelamento por outro processo (involuntária) — comando `kill`.

---

## Relacionamento entre Processos

### Linux / UNIX
- Um **pai** pode criar **processos filhos**, que por sua vez podem criar novos processos.
- Forma uma **hierarquia de processos** (grupo de processos).

### Windows
- **Não possui hierarquia de processos**.
- Todos os processos são criados da mesma forma.

> ⚠️ Obs: Se o processo pai morrer, o filho **não necessariamente morre**.

---

## Estados de um Processo

- `New`
- `Ready`
- `Running`
- `Blocked`
- `Exit`

> Apenas um processo pode estar em **"Running"** por vez.

---

## Chaveamento de Processos

Causas que provocam o chaveamento:
- Chamada de sistema
- Interrupção do relógio (tempo de CPU expirado)
- Interrupção de E/S
- Falta de memória (quando há memória virtual)
- **Trap**:
  - Interrupção de software que faz a CPU parar a execução de um processo para iniciar outro.
  - As informações do processo interrompido são salvas na memória para retomada futura.

---

## Troca de Contexto (Context Switch)

- Conjunto de informações que o SO precisa para restaurar a execução de um processo.
- Acontece sempre que um novo processo é selecionado.
- O tempo de troca de contexto é um **overhead** (custo) e depende de **suporte de hardware**.

---

## Retorno de um Processo

- Assim como pratos retornam ao cliente:
  - Pode retornar corretamente,
  - Faltar "ingredientes" (recursos),
  - Ou apresentar falhas (erros).

---

## Sistemas Operacionais e Processos

- Mantêm informações de todos os processos em andamento.
- Usam **registradores** para armazenar:
  - Endereços de hardware
  - Estado de execução
- Evitam retrabalho rastreando os passos já realizados pelas aplicações.
- Funcionam como **despachantes de processos**.

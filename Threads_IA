# Threads

## Definição

- **Processo**: programa em execução que contém um único fluxo de execução.
- **Thread**: programa em execução com múltiplos fluxos de execução.

Existia um Luhg

### Thread:
Um processo pode ter um ou mais threads.

### Paralelismo:

**No SO:**
- (a) Três processos, cada um com uma thread.

**No processo:**
- (b) Um processo com 3 threads.

## Processos:

Em um ambiente multithread, o processo:
- é a unidade de alocação e proteção de recursos.
- tem um espaço de endereçamento virtual que mantém a sua imagem.

Em um processo podem existir uma ou mais threads com:
- Um estado de execução (pronta, em execução, etc.).
- Seu contexto salvo quando não estiver executando.
- Sua pilha de execução.
  - Cada thread está executando uma linha de código diferente.
- Variáveis locais próprias.
- Acesso aos recursos do processo ao qual pertence.

Cada thread possui sua própria pilha de execução.

---

### Processo x Thread:

**Processo pesado**:
- **Informação global**: compartilhada entre todos os threads de um processo.
- **Informação local**: exclusiva para cada thread.

**Registradores | Pilha | Máscara | TSD**  

---

## Vantagens de Threads

- Não existe necessidade de comunicação entre processos.
- Pode-se utilizar vários processadores para um mesmo processo.
- O programa pode ser executado mesmo se parte dele estiver bloqueada.

## Desvantagens de Threads

- Suspender um processo implica em suspender todas as threads desse processo, já que elas compartilham o mesmo espaço de endereçamento.
- O término de um processo implica no término de todas as threads desse processo.
- Desenvolvimento de software é mais complexo.

## Exemplo de 3 Threads

**Editor de Texto**:
1. Teclado.
2. Disco.
3. Renderizar o texto.

---

### Implementação de Thread:

#### Thread em nível de usuário
- **Gerenciamento** pela aplicação:
  - Sem intervenção do SO.
  - O Kernel desconhece a existência das threads.
  - Pode ser usado com bibliotecas para rodar em qualquer SO (que a suporte).
  - Uma chamada de `suspend` bloqueia todas as threads de um processo:
    - O SO pensa que é apenas um processo.
    - Não pode rodar em diferentes processadores.

#### Threads em nível Kernel
- **Gerenciamento das threads** feito pelo kernel.
- Mantém informações de contexto para processo e threads.
- Podem ser executadas em diferentes núcleos.
- O usuário enxerga uma API para threads do kernel.
- No entanto:
  - A transferência de controle entre threads de um mesmo processo requer mudança para o modo kernel.
  - O chaveamento de threads (troca de contexto) é mais barato que a troca de contexto entre processos.

---

## Comunicação Interprocesso

### Comunicação de disputa:
- Dois processos desejam acesso simultâneo à memória compartilhada.

### Deadlock (Impasse):

Situação de impasse:
- Dois ou mais processos, ou threads, em um estado de espera porque um recurso do sistema está travado por outro processo.
- O processo não é capaz de mudar seu estado porque está aguardando recursos de outros processos que também estão esperando.

**Condições necessárias para ocorrer deadlock:**
1. **Não preempção**: recursos já alocados não podem ser tomados à força.
2. **Exclusividade mútua**: cada recurso é alocado a um processo ou está disponível.
3. **Posse e espera**: cada processo pode solicitar um recurso, alocá-lo e ficar bloqueado esperando outro recurso.
4. **Espera circular**: na cadeia circular de dois ou mais processos, um esperando por um recurso bloqueado pelo próximo.

### Tratamento de Deadlocks:
1. **Ignorar totalmente o problema**:
   - Baixa probabilidade de deadlock.
2. **Detecção e recuperação**.
3. **Evitar dinamicamente a ocorrência**:
   - Cuidado ao alocar recursos.
4. **Prevenção**:
   - Negar uma das condições necessárias.

---

### Seção Crítica:
- Seção do código onde se deseja acessar a memória compartilhada.
- Se um processo está na seção crítica, nenhum outro processo deve poder fazer o mesmo.
  - Dois processos não podem ser executados ao mesmo tempo em suas seções críticas.
  - Cada processo deve solicitar permissão para entrar na seção crítica (seção de entrada).
  - Ao terminar a seção crítica, sai-se dela (seção de saída).

---

**Exclusão mútua**: nunca dois processos devem estar na seção crítica ao mesmo tempo.

**Progresso**: Nenhum processo, fora da sua seção crítica, pode bloquear outros processos.

**Espera limitada**: Nenhum processo deve esperar eternamente para entrar na sua seção crítica.

---

## Cenário

1. **Editando um arquivo, o PID tranca o processo para que somente ele possa usar.**
   - Ao tentar usar o arquivo em outro programa, aparece uma mensagem de erro dizendo que ele já está em uso por outro programa.
   - O processo pode ser fechado no outro programa.

2. **Inanição de processos**:
   - Caso um processo precise de algo, mas outros processos estejam utilizando esse recurso, ele ficará em estado de inanição (não poderá continuar).

---

## Como estudar o assunto:

### Sites recomendados:
1. [GeeksforGeeks](https://www.geeksforgeeks.org) - Conteúdos sobre conceitos fundamentais de threads e processos.
2. [TutorialsPoint](https://www.tutorialspoint.com) - Oferece tutoriais abrangentes sobre threads, paralelismo e concorrência.
3. [Stack Overflow](https://stackoverflow.com) - Discussões sobre problemas práticos e soluções de threads em várias linguagens de programação.
4. [Learn-C.org](https://www.learn-c.org) - Focado em linguagens como C, com exemplos de threads e processos.

### Perguntas para prática:
1. O que acontece se um processo cria múltiplos threads e um deles falha? Como o sistema lida com isso?
2. Como podemos evitar deadlocks em sistemas multithreaded? Dê exemplos de estratégias de prevenção.
3. Quais são as diferenças entre gerenciamento de threads em nível de usuário e nível de kernel? Dê exemplos práticos.

### Vídeos recomendados:
1. **[Operating System Concepts: Threads & Processes](https://www.youtube.com/watch?v=2kF6G7zdbtQ)** - Vídeo didático sobre conceitos de processos e threads.
2. **[Introduction to Threads and Concurrency](https://www.youtube.com/watch?v=sQ4j9FKnBdI)** - Uma explicação sobre concorrência e threads no sistema operacional.
3. **[Deadlock in Operating Systems](https://www.youtube.com/watch?v=d57sV5pPqJk)** - Como o deadlock ocorre e formas de tratá-lo.

---

Espero que este conteúdo seja útil para o seu estudo! Se precisar de mais informações ou quiser explorar mais tópicos, me avise.

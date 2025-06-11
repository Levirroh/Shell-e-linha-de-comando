# 🧠 Memória Virtualizada

A memória virtual é uma abstração que permite que cada processo acredite ter acesso exclusivo a um grande espaço de memória contígua, mesmo que o sistema tenha uma quantidade limitada de RAM. Isso é possível graças à paginação e à segmentação, que permitem mapear partes do espaço de endereçamento virtual para diferentes áreas da memória física ou secundária (disco).

## Benefícios

- **Isolamento entre processos**: Um processo não pode acessar a memória de outro sem permissão.
- **Multitarefa eficiente**: Permite a execução de vários processos simultaneamente, mesmo que juntos excedam a capacidade da RAM.
- **Execução de programas maiores que a RAM disponível.**

# 🔄 MMU (Memory Management Unit)

A MMU é o componente de hardware (geralmente dentro da CPU) responsável por converter endereços virtuais em físicos. Essa tradução é essencial para que a CPU possa acessar corretamente os dados na RAM, já que os programas operam apenas com endereços virtuais.

## Estruturas utilizadas

- **Tabela de Páginas**: associa páginas virtuais a molduras físicas.
- **TLB (Translation Lookaside Buffer)**: cache especial que armazena traduções recentes para acelerar o acesso.
- **Registros de controle**: como o CR3 em arquiteturas x86, que aponta para a tabela de páginas atual.

# 📄 Memória Paginada

Na paginação, tanto a memória virtual quanto a física são divididas em blocos de mesmo tamanho:

- **Página**: unidade de memória virtual.
- **Frame (moldura)**: unidade correspondente na memória física.

## Vantagens

- **Redução de fragmentação externa**: por ser alocada em blocos fixos.
- **Facilidade na realocação**: páginas podem ser movidas sem que o processo perceba.

### Exemplo

Se a página tem 4KB e um processo precisa de 16KB, ele usará 4 páginas, que podem estar distribuídas em diferentes locais da RAM.

# ✅ Bit de Validade (Valid Bit)

Cada entrada da tabela de páginas possui um bit de validade, que informa ao sistema se a página está:

- **Presente na RAM (bit = 1)**: pode ser acessada diretamente.
- **Ausente ou inválida (bit = 0)**: o acesso gera um *page fault*.

Esse bit é essencial para detectar acessos ilegais ou ausentes na memória.

# ❗ Page Fault

Um *page fault* ocorre quando a MMU detecta que uma página solicitada por um processo não está na memória física. O sistema operacional, então:

1. Suspende o processo.
2. Carrega a página do disco para a RAM (*page in*).
3. Atualiza a tabela de páginas.
4. Retoma o processo.

Se não houver espaço livre, uma página existente pode ser movida para o disco (*page out*) para abrir espaço.

# 🔃 Page In / Page Out

- **Page In**: geralmente lento, pois envolve acesso ao disco. Ocorre quando uma página ausente é necessária.
- **Page Out**: escrita da página na memória secundária. Pode ser evitada se a página não foi modificada (ver “dirty bit”).

Esse mecanismo permite troca de contexto eficiente, mesmo com pouca RAM disponível.

# 🧭 Políticas de Busca (Page Fetch Policy)

## 1. Por Demanda (*Demand Paging*)

- Mais comum.
- Reduz o uso inicial de RAM.
- Pode gerar *page faults* frequentes no início da execução.

## 2. Antecipada (*Pre-paging*)

- Baseia-se em heurísticas de acesso passado.
- Reduz *page faults* se as previsões forem corretas.
- Pode desperdiçar recursos se páginas não forem usadas.

# 📦 Políticas de Alocação

Determinadas quantas molduras de página um processo pode utilizar:

## 1. Fixa

- Cada processo recebe uma quantidade estática.
- Simples de implementar.
- Pode causar subutilização ou sobrecarga.

## 2. Variável

- Ajuste dinâmico conforme o comportamento do processo.
- Mais eficiente, porém mais complexo.
- Pode usar o conceito de *Working Set* para estimar necessidades.

# 🔁 Políticas de Substituição

Quando a RAM está cheia, é preciso escolher qual página remover. Os critérios incluem:

- **Dirty Bit**: indica se a página foi modificada. Páginas limpas podem ser descartadas sem salvar no disco.
- **Local**: o processo só pode substituir páginas suas.
- **Global**: qualquer página, mesmo de outro processo, pode ser substituída.
- **Páginas do núcleo (Kernel)**: são residentes e não podem ser substituídas, para garantir estabilidade do SO.

# 🔍 Working Set (Modelo de Denning)

O *Working Set* é o conjunto de páginas que um processo utiliza ativamente durante um intervalo de tempo Δ.

## Conceitos de Localidade

- **Temporal**: páginas usadas recentemente tendem a ser usadas de novo em breve.
- **Espacial**: acesso a uma página sugere acesso iminente a páginas próximas.

Esse modelo permite prever quanta memória um processo realmente precisa e pode ser usado para evitar *thrashing* (quando o sistema passa mais tempo trocando páginas do que executando processos).

# ⚙️ Algoritmos de Substituição de Páginas

Cada algoritmo tem vantagens e desvantagens dependendo do padrão de acesso:

- **Ótimo (OPT)**: teórico, serve como benchmark. Impraticável porque exige conhecimento do futuro.
- **FIFO**: simples, mas pode substituir páginas ainda úteis (*anomalia de Belady*).
- **LFU**: remove páginas pouco acessadas, mas páginas antigas que não são mais usadas podem permanecer por muito tempo.
- **LRU**: baseado na localidade temporal, funciona bem na prática, mas pode ser caro de implementar (precisa rastrear ordem de uso).
- **NRU**: usa bits de referência e modificação, classifica páginas em categorias e remove as menos recentemente usadas e não modificadas.

# 📏 Tamanho da Página

A escolha do tamanho da página envolve *trade-offs*:

## Pequenas (ex: 4KB)

- Menor fragmentação interna.
- Mais páginas → mais overhead na tabela de páginas.

## Grandes (ex: 2MB ou 1GB)

- Reduzem a sobrecarga da MMU.
- Aumentam a fragmentação interna (páginas parcialmente usadas).

Sistemas modernos usam páginas de múltiplos tamanhos (ex: *huge pages*) para balancear desempenho e eficiência.

# 🔚 Conclusão

O gerenciamento de memória virtual é uma peça fundamental dos sistemas operacionais modernos. Ele garante que:

- Programas sejam executados com segurança e isolamento.
- A RAM seja utilizada de maneira eficiente.
- O sistema suporte multitarefa intensiva com recursos limitados.

A complexidade desse gerenciamento está escondida dos desenvolvedores e usuários, mas seu impacto é crucial para o desempenho, estabilidade e escalabilidade do sistema.

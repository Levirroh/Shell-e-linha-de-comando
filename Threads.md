Threads:


Definição:

	- Processo: programa e execução que contém um único fuxo de execução.
	- Thread: programa em execução com múltiplos fluxos de execução.

Existia um Luhg

Thread:

	Um um processo pode existir um ou mais processos.



Paralelismo:
No SO:
	a) três processos, cada um com uma threads.
No processo:
	b) um processo com 3 threads.


Processos:

	Em um ambiente multithread, processo:
		- é a unidade de aluçaõcao e proteção de recursos
		- tem um espaço de endereçamento virtual que mantém a asua imagem.

em um processo podem existir uma ou mais threads com:
	- um estado de execução (pronta, em execução,...)
	- seu contexto salvo quando nao estiver executando
	- sua pilha de execução
		- cada thread está executando uma linha de código diferente
	- sua pilha de execução
		- cada thread chama funções independentemente
	- variaveis locais próprias
	- acesso aos recursos do processo ao qual ela pertende.


cada thread possui sua pilha de execução

-- completar
Processo x Thread:

prrocesso pesado:
informação global para todos os threads de um processo:
informação local para cada thread:

registradores | pilha | máscara | TSD
-- fim do completar


vantagens de threads
	- não existe necessidade de comunicação entre processos.
	- pode-se utilizar vários processadores para um mesmo processo.
	- o programa pode ser executado mesmo se parte dele estiver bloqueada.

desvantagens de threads:
	- suspender um rpocesso implica em suspendenr todas as threads 
	  deste processo já que compartulham o mesmo espaço de endereçamento.
	- o término de um processo implica no término de todas as threads desse processo.
	- Desenvolvimento de software é mais complexo.

Exemplo de 3 threads:

Editor de texto:
	1. Teclado.
	2. Disco.
	3. Renderizar o texto.


--completar
Implementação de thread:
	Thread em nível de usuário
		- Gerenciamento pela aplicação 
			- sem intervenção do SO
		- Kernel desconhece existencia dos threads
		- Pode ser usado com bibliotecas para rodar em qualquer SO (que a suporte)
		- Uma chamada de susmtea bloqueia todas as threads de um processo
			- o SO acha que é só um processo.
			- Não pode rodar em diferentes processadores

Threads em nível kernel
	- Gerenciamento das threads feito pelo kernel
	- mantém informações de ´contexto para processo e threas
	- podem ser executadas em diferentes núcleos
	- o usuário enxerga uma API para threads do kernel
	- mas
		- a transferencia de controle entre threads de um mesmo processo requer mudança para modo kernel
		- chaveamento de threads = troca de contexto (no entando mais barata que troca de contexto de processo)
--fim do completar

Comunicação Inter-processo

	Comunicação de disputa:
		- dois processos desejam acesso simultâneo à memória compartilhada.
	
deadlock:
situação de impasse:
	- dois ou mais processos, ou threads em um estado de espera
	- porque um recurso do sistema está trabado por um outro processo
	- que está em espera, aguardando por outro recurso, travado por outro proceso em espera
	- o processo não é capaz de mudar seu estado por aguardar recursos de outros processos em espera


deadlock (impasse):
	- condições necessárias para ocorrer
		- não preempção: recursos já alocados não podem ser tomados à força
		- exclusividade mútua: cada recurso alocado a um processo ou disponível
		- posse-e-espera: cada processo pode solicitar um recurso, alocá-lo e ficar bloqueado, esperando outro recurso
		- espera circular: na cadeia circular de dois ou mais processos, um esprando por um recurso trabalho pelo próximo.

tratamento de deadlocks:
	- ignorar totalmente o problema
		- baixa probabilidade de acontecer o deadlock
	- detecção e recuperação
	- evitar dinamicamente a ocorrência
		- cuidado ao alocar recursos
	- prevenção
		- negar uma das quatro condições necessárias

seção crítica
	- seção do código onde se quer aessar a memória compartilhada
	- se um processo está na seão crítica, nenhum outro processo deve poder fazer o mesmo.
		-  dois processos não podem ser executados, ao memso tempo, em suas seções críticas
		- cada processo deve solicitar permissão para entrar na seção crítica -> seção de entrada
		- ao temrinar seção crítica -> seção de saída
--completar
Exclusão mútua: nunca dois rocessos em uma seção crítica
Progresso: nenhum processo, fora de sua seção crítica, pode bloquear outros processos
espera limitada: nenhum processo deve esperar eternamente para entrar em sua seção crítica


-- fim do completar
cenário

editando um processo, o PID tranca o processo para somente ele usar.
Ao tentar usar ele em outro programa aparece mensagem de erro de que já está em outro programa.
	- Pode ser fechado no outro processo.


Caso um processo precisa de algo mas outros processos estão usando o processo fica em estado de inanição.

--fim
Me forneça cenários e maneiras de estudar o assunto, tanto como sites que possuam o conteúdo tanto 
como perguntas geradas por você mesma. Além disso me passe vídeos altamente recomendados sobre o assunto

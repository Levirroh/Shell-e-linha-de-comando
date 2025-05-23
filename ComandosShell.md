# Comandos no Shell

## Execução de comandos

- `xargs` : para cada linha de saída de um comando ele vai fazer um comando em seguida que pode ser qualquer um.




## Redirecionamento de Saída

- `>`: Envia a saída de um comando para um arquivo ou local especificado (exemplo: `ls / > /tmp/saida.txt`). 
  - **Dica**: Este comando pode ser útil quando você deseja salvar a saída de comandos para análise posterior ou quando precisa gerar logs de execução de scripts.
- `>>`: Funciona igual ao `>`, mas em vez de substituir o conteúdo do arquivo de destino, ele acrescenta ao final.
  - **Dica**: Use `>>` para adicionar saídas de vários comandos em um único arquivo sem perder o que já está lá.
- `2>`: Redireciona a saída de erro do comando (exemplo: `ls bla 2> /tmp/erro.txt`).
  - **Dica**: Essencial para capturar erros e garantir que o sistema de arquivos não seja poluído com mensagens de erro indesejadas.

## Combinação de Comandos

- `|`: Usado para canalizar a saída de um comando diretamente para a entrada de outro.
  - **Dica**: Muito útil quando se deseja realizar operações em cadeia, como filtrar, contar ou ordenar resultados. O uso do `|` pode tornar sua linha de comando muito mais poderosa e eficiente.

## Filtragem de Resultados

- `grep`: Filtra e encontra padrões de texto nos resultados de um comando.
  - `^letra`: Filtra as linhas que começam com a letra especificada.
  - `-v`: Exclui as linhas que contêm o padrão especificado.
  - **Exemplo**: Para encontrar todos os arquivos que começam com "log" em um diretório, use: `ls | grep ^log`.
  - **Dica**: O `grep` é ótimo para encontrar informações específicas em uma grande quantidade de dados. Combine-o com outros comandos, como `ps aux | grep apache` para procurar processos em execução.

## Exibição de Parte do Arquivo

- `head`: Exibe a parte superior de um arquivo (padrão exibe as primeiras 10 linhas).
  - `-n número`: Exibe o número de linhas a partir do topo do arquivo.
  - **Dica**: Use `head` para rapidamente visualizar o começo de arquivos grandes ou logs.
- `tail`: Exibe a parte inferior de um arquivo (padrão exibe as últimas 10 linhas).
  - **Dica**: Ideal para monitoramento de logs em tempo real, especialmente se combinado com a opção `-f` (exemplo: `tail -f /var/log/syslog`).
- `uniq`: Exibe todo o arquivo porém mostra tudo que não repete.

### Exemplo de tail e head:

arquivo data.csv:

Username  |  Identifier | First name | Last name
booker12  |    9012     |   Rachel   |  Booker
grey07    |     2070    |   Laura    |   Grey
johnson81 |     4081    |    Craig   |  Johnson
jenkins46 |     9346    |    Mary    |   Jenkins
smith79   |     5079    |    Jamie   |    Smith

root@vbox:~# cat data.csv | tail -n 2
smith79   |     5079    |    Jamie   |    Smith

`Este possui uma linha em branco`

root@vbox:~# cat data.csv | tail -n 2 | head -n 1
smith79   |     5079    |    Jamie   |    Smith

`Esta foi retirado a linha em branco com o comando head -n 1` 

### Exemplo com o uniq

arquivo:

     2070    
     4081    
     5079    
     5079    
    9012     
     9346    

cat data.csv | cut -d '|' -f2 | sort
     2070    
     4081    
     5079    
    9012     
     9346    
  Identifier 


## Cortando Arquivos

- `cut`: Permite cortar e extrair colunas de texto de um arquivo.
  - `-f (field)`: Define quais colunas (campos) você deseja exibir.
  - `-d`: Define o delimitador que será usado para separar as colunas.
  - **Exemplo**: Para extrair a segunda coluna de um arquivo CSV delimitado por vírgulas, use: `cut -d ',' -f 2 arquivo.csv`.
  - **Dica**: O `cut` é útil quando você precisa extrair ou manipular dados estruturados, como arquivos CSV ou logs com campos delimitados.
 
### Exemplo de cut com -d e -d:

Usando o arquivo data.csv:

Username  |  Identifier | First name | Last name
booker12  |    9012     |   Rachel   |  Booker
grey07    |     2070    |   Laura    |   Grey
johnson81 |     4081    |    Craig   |  Johnson
jenkins46 |     9346    |    Mary    |   Jenkins
smith79   |     5079    |    Jamie   |    Smith

Fica:

cat data.csv | cut -d '|' -f2 
  Identifier 
    9012     
     2070    
     4081    
     9346    
     5079    


Usando o sort no final para aparecer os números em ordem crescente:

cat data.csv | cut -d '|' -f2 | sort
     2070    
     4081    
     5079    
    9012     
     9346    
  Identifier 
  
### Exemplos

- `ls -lha / | grep s`: Lista diretórios que contêm a letra "s" no diretório raiz (`/`).
  - **Dica**: Usar `grep` após comandos como `ls` ou `ps` é uma maneira rápida de buscar por padrões específicos dentro de uma grande quantidade de dados.

## Comandos Comuns

- `cat`: Exibe o conteúdo completo de um arquivo no terminal.
  - **Dica**: Combine com `more` ou `less` para ler arquivos longos sem sobrecarregar a tela. Exemplo: `cat arquivo.txt | less`.
- `tac`: Exibe o conteúdo de um arquivo ao contrário, linha por linha.
  - **Dica**: Útil para visualizar logs ou arquivos grandes de baixo para cima, por exemplo, quando você quer ver as entradas mais recentes primeiro.
- `pwd`: Mostra o caminho do diretório atual.
  - **Dica**: Use frequentemente para ter certeza de que você está no diretório correto ao navegar por arquivos e pastas.
- `nano`: Editor de texto no terminal, simples e eficaz para editar arquivos.
  - **Dica**: Use `nano` para edições rápidas, mas para tarefas mais complexas, um editor como `vim` ou `emacs` pode ser mais eficiente.

## Diretórios Importantes

- `/etc/motd`: Arquivo que exibe a mensagem de boas-vindas ao iniciar a máquina virtual (VM).
  - **Dica**: Você pode editar esse arquivo para personalizar a mensagem que será exibida para todos os usuários ao acessar a máquina, o que pode ser útil para incluir informações importantes ou notificações.

# Comandos Gerais

## Instalações de Pacotes

- `apt install`: Sincroniza a lista de pacotes disponíveis para instalação com os repositórios configurados no arquivo `/etc/apt
- `apt install curl`: O comando apt install curl serve para instalar a ferramenta curl no seu sistema. Ele é uma ferramenta de linha de comando que permite transferir dados utilizando diversos protocolos de rede, como HTTP, HTTPS, FTP, entre outros.
    - Juntamente este link irá inserir no arquivo mencionado tudo que está no link: "curl https://support.staffbase.com/hc/en-us/          article_attachments/360009197031/username.csv > data.csv"



## Atualização de Pacotes

- `apt update`: Sincroniza a lista de pacotes disponíveis para instalação com os repositórios configurados no arquivo `/etc/apt

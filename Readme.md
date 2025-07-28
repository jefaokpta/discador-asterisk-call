## Discador Simples para Asterisk

Este repositório acompanha um tutorial em vídeo que ensina a **automatizar chamadas** no Asterisk usando o recurso de arquivos `.call`. Com ele, você pode originar ligações, conectá-las a atendentes ou reproduzir áudios informativos de forma simples e eficaz.

-----

### Como Funciona

A automação é feita através de um arquivo com a extensão **`.call`**, que contém todas as informações da chamada a ser executada. Ao mover este arquivo para o diretório `/var/spool/asterisk/outgoing`, o Asterisk o processa imediatamente.

-----

### Estrutura do Arquivo `.call`

O arquivo `.call` é um arquivo de texto simples com uma série de parâmetros que definem o comportamento da chamada. Veja um exemplo:

```
Channel: SIP/9100
Callerid: Boris <123456789>
MaxRetries: 5
RetryTime: 5
WaitTime: 10

;; Executar qualquer contexto
Context: default
Extension: 1234
Priority: 1

;; Executar alguma aplicação
Application: Playback
Data: hello-world

```

-----

### Parâmetros Principais

A seguir, a descrição dos parâmetros mais comuns que você pode utilizar:

#### Parâmetros do Originador da Chamada

  * **`Channel`**: Define o canal de saída que o Asterisk utilizará para originar a chamada. Exemplo: `DAHDI/1122334455` ou `SIP/9100`.
  * **`CallerID`**: Define o nome (`${CALLERID(name)}`) e o número (`${CALLERID(num)}`) que aparecerão para o destino da chamada. Exemplo: `Boris <123456789>`.
  * **`MaxRetries`**: O número máximo de tentativas de chamada. Se for `0`, o Asterisk tentará apenas uma vez.
  * **`RetryTime`**: O intervalo, em segundos, entre as tentativas de chamada. O valor padrão é 300 segundos.
  * **`WaitTime`**: O tempo, em segundos, que o Asterisk aguardará o atendimento da chamada em cada tentativa. O valor padrão é 45 segundos.
  * **`Account`**: O código da conta de billing associado à chamada. Exemplo: `22`.

#### Parâmetros de Destino da Chamada

Após a chamada ser atendida, você pode direcioná-la para um destino ou executar uma aplicação.

##### Opção 1: Conectar a um Atendente

  * **`Context`**: O contexto do dialplan por onde a chamada será processada.
  * **`Extension`**: O número de destino da chamada dentro do contexto.
  * **`Priority`**: A prioridade com que a extensão será processada no contexto.

##### Opção 2: Executar uma Aplicação

  * **`Application`**: O nome da aplicação do Asterisk a ser executada. Exemplo: `Playback`.
  * **`Data`**: Os dados da aplicação. Para o `Playback`, é o nome do arquivo de áudio. Exemplo: `tt-monkeys`.

#### Variáveis de Canal

  * **`Set`**: Permite definir uma variável de canal para ser utilizada no processamento da chamada. Exemplo: `CDR(userfield)=CALLBACK`.

-----

### Assista ao Tutorial

Para ver esses conceitos em ação, assista ao vídeo tutorial e aprenda a criar seu próprio discador simples\!
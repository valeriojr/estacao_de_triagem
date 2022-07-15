Universidade Federal de Alagoas - UFAL

Instituto de Computação - IC

Engenharia de Computação

Automação Industrial 2021.2

Prof.: João Raphael Souza Martins

Aluno: Valério Nogueira Rodrigues Júnior

# Estação de triagem

Simulação de uma estação de triagem como projeto final da disciplina de Automação Industrial, utilizando FactoryIO e TIA Portal v17

![Funcionamento do sistema](https://github.com/valeriojr/estacao_de_triagem/blob/61a1977e4b2de3b6a5f5ca568538b6fb4a768f37/EstacaoDeTriagem.gif)

## Descrição do problema

O problema consiste em automatizar uma estação de triagem para separar objetos. Os objetos são transportados através de esteiras, passando por um sensor ótico que identifica o tipo do objeto. Em seguida o percurso é impedido pelo separador correspondente, que faz com que o objeto caia na rampa desejada e incremente seu contador.

## Esquemático

![Esquemático do projeto](/esquematico.jpg)

## Tabelas de endereçamento
A tabela de endereçamento do projeto foi construída com base nas entradas e saídas presentes na cena do *FactoryIO*. A seguir é apresentada a tabela com o nome da *tag*, seu tipo e o endereço lógico, obtida utilizando a ferramenta de exportação do TIA Portal
| Name | Data Type | Logical Address |
| --- | --- | --- |
| At Exit | Bool | %I0.0 |
| Start | Bool | %I0.1 |
| Stop | Bool | %I0.3 |
| Vision Sensor | DInt | %ID30 |
| Ramp | DInt | %MD0 |
| Entry Conveyor | Bool | %Q0.0 |
| Exit Conveyor | Bool | %Q0.2 |
| Sorter 1 Turn | Bool | %Q0.3 |
| Sorter 1 Belt | Bool | %Q0.4 |
| Sorter 2 Turn | Bool | %Q0.5 |
| Sorter 2 Belt | Bool | %Q0.6 |
| Sorter 3 Turn | Bool | %Q0.7 |
| Sorter 3 Belt | Bool | %Q1.0 |
| On | Bool | %Q1.1 |
| Emitter | Bool | %Q1.4 |
| Counter 1 | DInt | %QD30 |
| Counter 2 | DInt | %QD34 |
| Counter 3 | DInt | %QD38 |

Para ver a tabela completa, clique [aqui](https://docs.google.com/spreadsheets/d/164uqqT6c53RvLH8Ako69DZUV4Dy293bLTqGDGNpTXPA/edit?usp=sharing).

## Descrições lógicas
| Nome | Descrição |
| --- | --- |
| At Exit | Sensor que indica a passagem de objetos nas rampas (Normalmente fechado) |
| Start | Botão que inicia o processo |
| Stop | Botão que para o processo |
| Vision Sensor | Sensor ótico que detecta e reconhece o tipo de objeto |
| Ramp | Variável de memória que armazena o número da rampa que o objeto atual deve cair (-1 caso não haja um objeto atual) |
| Entry Conveyor | Esteira onde os objetos são depositados e levados até o sensor de visão |
| Exit Conveyor | Esteira que leva os objetos até a entrada da rampa que eles devem ser separados |
| Sorter 1 Turn | Separador da primeira rampa, da direita para a esquerda |
| Sorter 1 Belt | Correia do separador 1 |
| Sorter 2 Turn | Separador da rampa do meio |
| Sorter 2 Belt | Correia do separador 2 |
| Sorter 3 Turn | Separador da última rampa, da direita para a esquerda |
| Sorter 3 Belt | Correia do separador 3 |
| On | Variável que indica que o sistema está ligado, utilizada para ligar os componentes e selar o botão *Start* |
| Emitter | Deposita os objetos na esteira de entrada |
| Counter 1 | Display de 7 segmentos que representa quantos objetos caíram na rampa 1 |
| Counter 2 | Display de 7 segmentos que representa quantos objetos caíram na rampa 2 |
| Counter 3 | Display de 7 segmentos que representa quantos objetos caíram na rampa 3 |

## Tabelas verdade

A seguir são apresentadas as tabelas verdade utilizadas

| Start | Stop | On | On (Saída) |
| --- | --- | --- | --- |
| F | F | F | F |
| F | F | V | F |
| F | V | F | F |
| F | V | V | V |
| V | F | F | F |
| V | F | V | F |
| V | V | F | V |
| V | V | V | V |

| On | Emitter (Saída) | Entry Conveyor (Saída) | Exit Conveyor (Saída) |
| --- | --- | --- | --- |
| V | V | V | V |
| F | F | F | F |

| On | Sorter1 Turn | Sorter1 Belt (Saída) |
| --- | --- | --- |
| F | F | F |
| F | V | F |
| V | F | F |
| V | V | V |

| On | Sorter2 Turn | Sorter2 Belt (Saída) |
| --- | --- | --- |
| F | F | F |
| F | V | F |
| V | F | F |
| V | V | V |

| On | Sorter3 Turn | Sorter3 Belt (Saída) |
| --- | --- | --- |
| F | F | F |
| F | V | F |
| V | F | F |
| V | V | V |


## Programação em Ladder

O código em Ladder foi dividido em 5 redes, sendo elas:

### Integração com *FactoryIO*

Bloco que faz a integração entre os dois *softwares*. Disponível no *template* o projeto disponibilizado pelo *FactoryIO*, não deve ser alterado.

![Integração com *FactoryIO*](/ladder_network1.png) 

### Liga/Desliga

Rede que cuida da parte da ligação e desligamento do sistema. Ativa as esteiras principais e as esteiras dos separadores quando necessário.

![Liga/Desliga](/ladder_network2.png)

### Classificação do objeto

Realiza a identificação do objeto através de um sensor ótico. A leitura do sensor é um inteiro != 0 quando um objeto é detectado. Guarda o tipo na variável `Ramp` (leitura do sensor mód. 3)

![Classificação do objeto](/ladder_network3.png)

### Separadores

Ativa os separador correspondente quando o tipo do objeto é identificado e assim o mantém por 1 segundo depois que o sensor de saída detecta que um objeto está "entrou" em uma das 3 rampas, para garantir que ele caia.

![Separadores](/ladder_network4.png)

### Contadores

Incrementa o contador da rampa correspondente toda vez que o objeto passa por ela e "esquece" o tipo do objeto atual (reativa a esteira de entrada, fazendo com que o sensor ótico detecte um novo objeto).

![Contadores](/ladder_network5.png)

## Resultado
![![Apresentação do projeto](https://img.youtube.com/vi/0x-oRdty2iY/0.jpg)](https://www.youtube.com/watch?v=0x-oRdty2iY)

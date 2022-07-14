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

## Programação em Ladder

## Resultado
![![Apresentação do projeto](https://img.youtube.com/vi/0x-oRdty2iY/0.jpg)](https://www.youtube.com/watch?v=0x-oRdty2iY)

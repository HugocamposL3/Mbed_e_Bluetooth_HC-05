# Bluetooth HC-05 com a Placa NUCLEO STM-32

## Objetivo:

- Ligar e desligar três leds comandados por dados enviados via bluetooth HC-05 e a placa NUCLEO-F103RB.

## Introdução:

Neste tutorial será apresentado como controlar três leds com bluetooth HC-05 e também como criar um aplicativo para que esse controle seja feito com o smartphone.

### Programando com mBed:

Para programar a placa NUCLEO, será utilizado o compilador online chamado mBed, é necessário fazer o login no site do fornecedor [link](https://os.mbed.com/) e logo após abrir o compilador online para começar o seu código, nesse tutorial o autor entende que o leitor já tem o básico para programar na plataforma online mBed, então por isso ele não vai colocar o passo a passo para isso. 

### Escrevendo o Código:

Nesse código não é utilizado funções complexas, o microntrolador só vai receber o caracter enviado para o bluetooth e fazer o que foi programado em poucas linhas. Primeiramente, import a biblioteca padrão do mBed.

```javascript
#include "mbed.h"
```
Logo após declare os pinos de saida do microcontrolador, nos quais irão ligar os leds.

```javascript
DigitalOut led1 (D10);
DigitalOut led2 (D9);
DigitalOut led3 (D8);
``` 
Agora declare as portas que serão utilzadas para comunicação TX,RX entre o Bluetooth e a placa NUCLEO, nesse caso é utilizado as portas PB10 E PB11.

```javascript
Serial bt (PB_10, PB_11); 
```
Dando inicio ao programa principal, declarando uma variavel tipo **char** e iniciando o baud rate do bluetooth em 9600.

```javascript
int main(void)
{
    char ch;
    bt.baud(9600);
    bt.printf("Código Carregado\r\n");
```
E por fim o loop principal, que é aonde o microcontrolador vai receber o carácter enviado pelo o aplicativo do celular para o bluetooth HC-05, cada letra enviada é um 
comando que o microcontrolar irá fazer.

```javascript
while(1)
    {
        if(bt.readable())
        {
            ch = bt.putc(bt.getc());
            if (ch == 'A')
            {
                led1 = 1;
                wait_ms(200);
            }
            else if (ch == 'B')
            {
                led1 = 0;
                wait_ms(200);
            }
            else if (ch == 'C')
            {
                led2 = 1;
                wait_ms(200);
            }
            else if (ch == 'D')
            {
                led2 = 0;
                wait_ms(200);
            }  
            else if (ch == 'E')
            {
                led3 = 1;
                wait_ms(200);
            }  
            else if (ch == 'F')
            {
                led3 = 0;
                wait_ms(200);
            }     
        }
    }
}
``` 
Primeiro o código verifica se o bluetooth está operando, se sim, o código vai gravar na variavel **ch** o dado que foi enviado para o bluetooth e logo após é
uma sequência de **else if** que irão ligar ou desligar os leds. 

## Esquemático das ligações:

Essas são os componentes utilizados nesse projeto:

- 1 Bluetooth HC-05.
- 1 Placa NUCLEO-f103RB.
- 3 Leds.
- 3 Resistores de 270Ohm ou parecido.
- 1 Protoboard.

O circuito do projeto:

<a href="https://imgur.com/MN3owUH"><img src="https://imgur.com/MN3owUH.jpg" title="source: imgur.com" /></a>

- Pino RX do Bluetooth será ligado no pino PB_10 da NUCLEO.
- Pino TX do Bluetooth será ligado no pino PB_11 da NUCLEO.
- Para alimentar o Bluetooth foi utilizado a saída 3.3V da NUCLEO.
- Os leds serão ligados nos D10, D9 e D8 da NUCLEO
- O GND é o mesmo para o circuito todo, foi utilizado o GND da NUCLEO.

## Aplicativo desse Projeto:

O aplicativo desse projeto, está anexado no juntos com os outros arquivos e poderá ser exportado para o site do **KODULAR** [link](https://www.kodular.io/). 
Ele tem o desgner da imagem abaixo e já está programado para enviar os caracteres que foram incluidos no código do mBed.

<a href="https://imgur.com/7NILrWE"><img src="https://imgur.com/7NILrWE.jpg" title="source: imgur.com" /></a>

Este aplicativo foi projetado para um celular com a tela que tem uma resolução de 2400x1080, se caso a tela do celular for diferente dessa, pode ser que
o aplicativo fique um pouco distorcido. 

# Conclusão:

Pronto o projeto foi finalizado e está pronto para ser testado, o aplicativo é bem simples de utilizar e a ligação também não é dificil. Se tiver qualquer erro
ou não ter entendido algum passo desse tutorial entre em contato com o autor via E-mail, para tirar dúvidas.


# Autor:
- Hugo Campos
- E-mail: camposhugo029@gmail.com
- Data: 11/03/2021










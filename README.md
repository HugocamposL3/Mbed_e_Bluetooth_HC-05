# Utilizando o Bluetooth HC-05 com a Placa Núcleo STM-32

## Objetivo:

- Ligar e desligar três leds comandados por dados enviados via bluetooth HC-05 e a placa Núcleo-F103RB.

## Introdução:

Neste tutorial será apresentado como controlar três leds com bluetooth HC-05 e também como criar um aplicativo para que esse controle seja feito com o smartphone.

### Programando com MBED:

Para programar a placa Nucleo, será utilizado o compilador online chamado MBED, é necessário fazer o login no site do fornecedor [link](https://os.mbed.com/) e logo após abrir o compilador online para começar o seu código, nesse tutorial o autor entende que o leitor já tem o básico para programar na plataforma online MBED, então por isso ele não vai colocar o passo a passo para isso. 

### Escrevendo o Código:

Nesse código não é utilizado funções complexas, o microntrolador só vai receber o caracter enviado para o bluetooth e fazer o que foi programado em poucas linhas. Primeiramente, import a biblioteca padrão do MBED.

```javascript
#include "mbed.h"
```
Logo após declare os pinos de saida do microcontrolador, nos quais irão ligar os leds.

```javascript
DigitalOut led1 (D10);
DigitalOut led2 (D9);
DigitalOut led3 (D8);
``` 
Agora declare as portas que serão utilzadas para comunicação TX,RX entre o Bluetooth e a placa Núcleo, nesse caso é utilizado as portas PB10 E PB11.

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






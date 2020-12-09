# Programa-de-controle-para-uma-bomba-de-piscina
Um controlador para temporizar o funcionamento de uma bomba de piscina.

#include "ssd.h"
#include "pwm.h"
#include "config.h"
#include "lcd.h"


void main(void) {
    unsigned int i, j;
    unsigned int contseg, contmin;
    
    ssdInit();
    pwmInit();
    pwmSet(50);
    lcdInit();

    lcdData('L');
    lcdData('i');
    lcdData('g');
    lcdData('a');
    lcdData('d');
    lcdData('o');
    
    
    for (;;) {

        
        contseg++;
        contmin++;
        if (((contseg / 1000) % 10) == 6) {
            contseg = 0;
            contmin += 4000;
        }
       
        
        pwmSet(50);

        ssdDigit(((contseg / 100) % 10), 3); //1s
        ssdDigit(((contseg / 1000) % 10), 2); //10s 
        ssdDigit(((contmin / 10000) % 10), 1);
        ssdDigit(((contmin / 100000) % 10), 0); //1000s
        ssdUpdate();

    }

}



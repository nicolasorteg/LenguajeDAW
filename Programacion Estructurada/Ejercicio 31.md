### Simular el mecanismo de devolución de monedas de una máquina expendedora. El programa pregunta una cantidad de dinero en euros (ej. 3,47 €) y calcula la cantidad mínima de monedas necesarias para devolverla (ej. 1 de 2€, 1 de 1€, 2 de 20cts, etc.)

```bash

Main {

    decimal dinero;
    int moneda2Euros;
    int moneda1Euro;
    int moneda50Centimos;
    int moneda20Centimos;
    int moneda10Centimos;
    int moneda5Centimos;
    int moneda2Centimos;
    int moneda1Centimo;
    bool isNegativo = false; // bandera

    writeLine("Simulación de Devolución de Monedas.");

    do {

        writeLine("¿Qué cantidad desea?: ");
        dinero = (decimal) readLine(); // 14.89

        if (dinero<= 0.0) {
            
            writeLine("El valor debe ser superior a 0.0")
            isNegativo = true;

        } else {

            isNegativo = false;
        }

    } while (isNegativo); // no se repetirá ya que 14.89 > 0.0 y por lo tanto isNegativo = false

    while (dinero >= 2.0) { // 7 entradas
        dinero -= 2.0;
        moneda2Euros += 1;
    }

    while (dinero >= 1.0) { // 0 entradas
        dinero -= 1.0;
        moneda1Euro += 1;
    }

    while (dinero >= 0.50) { // 1 entrada
        dinero -= 0.50;
        moneda50Centimos += 1;
    }

    while (dinero >= 0.20) { // 1 entrada
        dinero -= 0.20;
        moneda20Centimos += 1;
    }

    while (dinero >= 0.10) { // 1 entrada
        dinero -= 0.10;
        moneda10Centimos += 1;
    }

    while (dinero >= 0.05) { // 1 entrada
        dinero -= 0.05;
        moneda5Centimos += 1;
    }

    while (dinero >= 0.02) { // 2 entradas
        dinero -= 0.02;
        moneda2Centimos += 1;
    } 

    while (dinero >= 0.01) { // 0 entradas
        dinero -= 0.01;
        moneda1Centimo += 1;
    }

    int monedasTotales = moneda2Euros + moneda1Euro + moneda50Centimos + moneda20Centimos + moneda10Centimos + moneda5Centimos + moneda2Centimos + moneda1Centimo; // 12

    writeLine("Monedas de 2€ usadas: " + moneda2Euros); // 7
    writeLine("Monedas de 1€ usadas: " + moneda1Euro); // 0
    writeLine("Monedas de 50 céntimos usadas: " + moneda50Centimos); // 1
    writeLine("Monedas de 20 céntimos usadas: " + moneda20Centimos); // 1
    writeLine("Monedas de 10 céntimos usadas: " + moneda10Centimos); // 1
    writeLine("Monedas de 5 céntimos usadas: " + moneda5Centimos); // 1
    writeLine("Monedas de 2 céntimos usadas: " + moneda2Centimos); // 2
    writeLine("Monedas de 1 céntimo usadas: " + moneda1Centimo); // 0
    writeLine("El mínimo número de monedas posible para esa cantidad es: " + monedasTotales); // 12
}





```
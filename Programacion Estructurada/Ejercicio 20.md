### Dados dos números enteros, calcular el cociente y el resto de su división mediante la técnica de restas sucesivas (utilizando un bucle mientras).

``` bash
Main {

    int dividendo;
    int divisor;
    int cociente = 0;
    int resto = 0;
    bool isNegativo = false;

    writeLine("Algoritmo de Restas Sucesivas");

    do {
        
        writeLine("Introduce el Dividendo: ");
        dividendo = (int) readLine();
        writeLine("Introduce el Divisor: ");
        divisor = (int) readLine();

        if (dividendo < 0 || divisor <= 0) {

            writeLine("Entrada de datos inválida. Por favor, introduzca valores enteros positivos.");

            isNegativo = true;

        } else {

            while (dividendo >= divisor) {

                dividendo -= divisor;

                cociente += 1;

            }

            resto = dividendo;

        }

    } while (isNegativo);

    writeLine("Cociente = " + cociente);
    writeLine("Resto = " + resto);
}
```

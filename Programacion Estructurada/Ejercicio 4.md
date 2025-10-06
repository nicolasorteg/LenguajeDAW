### Diseñar un algoritmo que calcule la media de tres números que se piden al usuario. El resultado se debe mostrar con decimales.

``` bash
Main {

    decimal num1;
    decimal num2;
    decimal num3;
    decimal media;
    bool isNegativo = false;

    writeLine("Media de Tres Números");

    // bucles indefinidos do-while para que el menú se muestre al menos una vez (1-N)
    do {
        do {

        writeLine("Introduce el primer número: ");
        num1 = (decimal) readLine();
        writeLine("Introduce el segundo número: ");
        num2 = (decimal) readLine();
        writeLine("Introduce el tercer número: ");
        num3 = (decimal) readLine();

        if (num1 <= 0 || num2 <= 0 || num3 <= 0) {

            writeLine("Datos no válidos. Por favor, introduzca un valores superiores a 0.0");
            isNegativo = true;

        } else {

            isNegativo = false;

        }

    } while (isNegativo);

    media = (num1 + num2 + num3) / 3;

    writeLine("La media de los datos introducidos es: " + media);

    writeLine("¿Desea volver al inicio del programa?: (y/n)");
    string opcion = readLine();

    } while (opcion == "y" || opcion == "yes" || opcion == "Y"); 

    writeLine("Fin del programa.");
}
```
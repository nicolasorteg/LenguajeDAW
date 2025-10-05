### Calcular y mostrar el área y la circunferencia de un círculo, dado el radio introducido por el usuario.

``` bash
Main {

    // declaración de variables
    int radio;
    decimal area;
    decimal circunferencia;
    decimal pi = 3.1415926535;
    bool isNegativo = false

    writeLine("Cálculo de Círculo");

    do {

        writeLine("Introduce el radio (cm): "); // 10
        radio = (int)readLine();

        if (radio <= 0) {

            writeLine("El número debe ser superior a 0.")
            isNegativo = true;

        } else {

            isNegativo = false;

        }

    } while (isNegativo); // no repetirá ya que 10 > 0

    circunferencia = 2 * pi * radio; // 62.83185307
    area = pi * radio * radio; // 314.15926535

    writeLine("Según el radio dado, el círculo tendrá:");
    writeLine("Circunferencia: " + circunferencia);
    writeLine("Área: " + area);

    writeLine("Fin del programa");
}
```
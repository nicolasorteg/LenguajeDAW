### Calcular y mostrar la superficie y el perímetro de un rectángulo cuyos datos (largo y ancho) se piden por teclado.

``` bash
Main {

    int largo;
    int ancho;
    int perimetro;
    int superficie;
    bool entradaInvalida = false; // bandera

    writeLine("Cálculo de Área de Rectángulo");

    // aplicamos un bucle para asegurar la entrada de datos, el programa no comenzará con los cálculos hasta que estos sean válidos
    do {

        entradaInvalidad = false // siempre empezamos reiniciando la variable a false hasta que se introduzcan datos

        writeLine("¿Cuánto mide de largo (cm)?: ");
        largo = (int)readLine();
        writeLine("¿Cuánto mide de ancho (cm)?: ");
        ancho = (int)readLine();

        if (largo <= 0 || ancho <= 0) {

            writeLine("Entrada de datos fallida. Por favor, introduzca valores por encima de 0.");
            entradaInvalida = true; // asignamos true ya que la entrada es invalida y nos servirá como bandera

        } else {

            writeLine("Largo: " + largo);
            writeLine("Ancho: " + ancho);
        }

    } while (entradaInvalida) // mientras la entrada sea invalida, sigue pidiendo los datos
    
    // solo se accede a estos cálculos con datos válidos
    perimetro = largo * 2 + ancho * 2;
    superficie = largo * ancho;

    // muestra por pantalla
    writeLine("Según estas medidas, el rectángulo dado:")
    writeLine("Perímetro = " + perimetro);
    writeLine("Superficie = " + superficie);

    writeLine("Fin del programa.")
}
```
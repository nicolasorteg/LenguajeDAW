### Calcular y mostrar la superficie y el perímetro de un cuadrado cuyo lado se pide por teclado.

```bash
Main {

    //declaración de variables
    int superficie;
    int perimetro;
    int lado;

    // condicional para cuidar la entrada de datos
    do {

        writeLine("Introduce la medida de un lado en centímetros: ");
        lado = (int)readLine();

        if (lado >= 1) {

            perimetro = lado * 4;
            superficie = lado * lado;
            writeLine("Perímetro: " + perimetro + ". Superficie: " + superficie + ".");

        } else {

            writeLine("El lado no puede ser inferior a 1cm.")
        }

  } while (lado < 1);

   writeLine("Fin del programa.");
}
```
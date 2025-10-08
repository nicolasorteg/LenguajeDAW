### Implementar una simulación básica de una máquina tragaperras (tres valores aleatorios entre 0 y 9). Gestionar el saldo, las pérdidas y las ganancias. El juego termina si el saldo llega a 0 o si el usuario decide no continuar.

``` bash
Main {

    // declaración de variables.
    decimal saldo;
    decimal saldoApostado;
    decimal saldoAñadido;
    int opcionMenu;
    int numeroAleatorio1;
    int numeroAleatorio2;
    int numeroAleatorio3;
    bool isNegativo;
    bool isSaldoAñadidoNegativo;

    writeLine("Simulación de Máquina Tragaperras");
    

    do {

        writeLine("Introduce el saldo inicial: "); // 1
        saldo = (decimal)readLine(); // 1.0

        if (saldo < 0.50) { // no entra

            writeLine("Saldo inferior a 0.50€. Por favor, introduzca un valor superior o igual a la apuesta mínima.");
            isNegativo = true;

        } else { // entra

            writeLine("Saldo inicial: " + saldo + "€"); // Saldo inicial: 1.0€
            isNegativo = false;

        }

    } while (isNegativo); // 0 repeticiones, solo la obligada


    do {

        writeLine("-----------------------------------------------------------");
        writeLine("Introduzca el número de la opción que desee llevar acabo:");
        writeLine("1. Tirar de la tragaperras.");
        writeLine("2. Añadir saldo.");
        writeLine("3. Salir.");
        opcionMenu = (int)readLine(); // 1

        switch (opcionMenu) {

            case 1:

                do { 

                    writeLine("¿Cuando dinero quiere apostar a esta tirada?: "); // 1
                    saldoApostado = (decimal)readLine(); // 1.0

                    if (saldoApostado < 0.50 || saldoApostado > saldo) { // 0 entradas

                        writeLine("Entrada de datos inválida. Recuerde que la apuesta mínima es de 0.50€ y la máxima es su saldo.");

                    } else {

                        saldo -= saldoApostado; // saldo = 0.0

                        numeroAleatorio1 = Math.random(1, 9); // 2
                        numeroAleatorio2 = Math.random(1, 9); // 3
                        numeroAleatorio3 = Math.random(1, 9); // 7

                        if (numeroAleatorio1 == numeroAleatorio2 == numeroAleatorio3) { // no entrada

                            saldo += 2 * saldoApostado;
                            writeLine(numeroAleatorio1 + " " + numeroAleatorio2 + " " + numeroAleatorio3 + ". ENHORABUENA!!" );
                            writeLine("Tu saldo tras esta victoria es: " + saldo);

                        } else if ((numeroAleatorio1 == numeroAleatorio2 != numeroAleatorio3) || (numeroAleatorio1 != numeroAleatorio2 == numeroAleatorio3) || (numeroAleatorio1 == numeroAleatorio3 != numeroAleatorio2)) { // no entrada

                            saldo += saldoApostado;
                            writeLine(numeroAleatorio1 + " " + numeroAleatorio2 + " " + numeroAleatorio3 + ". Dinero apostado devuelto." );
                            writeLine("Tu saldo es de: " + saldo);

                        } else {  // entra

                            writeLine(numeroAleatorio1 + " " + numeroAleatorio2 + " " + numeroAleatorio3 + ". Más suerte la próxima." );
                            writeLine("Tu saldo es de: " + saldo + "€"); // 0.0

                        }
                    } 
                
                } while (saldoApostado < 0.50 || saldoApostado > saldo); // 0 repeticiones, solo la obligada
                

                break;
            
            case 2: // no entra

                do {

                    writeLine("¿Cuánto quieres añadir?: ");
                    saldoAñadido = (decimal)readLine();

                    if (saldoAñadido < 0.0) {

                        writeLine("No se acepta dinero negativo.");
                        isSaldoAñadidoNegativo = true;

                    } else {

                        saldo += saldoAñadido;
                        writeLine("Saldo final: " + saldo);
                        isSaldoAñadidoNegativo = false;

                    }

                } while (isSaldoAñadidoNegativo);
                
                break;

            case 3: // no entra

                writeLine("Ha sido un placer.");

                break;

            default:

                writeLine("Opción no válida.");

                break;

        }

    } while (opcionMenu != 3 && saldo >= 0.5); // true && false = false

    writeLine("Fin del programa. Saldo final: " + saldo);
}
```
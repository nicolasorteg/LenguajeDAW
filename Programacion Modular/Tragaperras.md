### Implementar una simulación de una máquina tragaperras. 

``` bash

/* este programa aún no gestiona las entradas de datos con 'try catch'
   por lo que si se introduce texto donde espera números el programa fallará 
*/

using Math; // importamos la librería math

Main {

    decimal saldo;

    bool isSaldoValido = true;


    writeLine("Bienvenido a la Máquina Tragaperras");

    do {

        writeLine("¿Con cuánto saldo deseas iniciar? (€): ");
        saldo = (decimal)readLine();

        isSaldoValido = isSuperiorA0(saldo);

        if (!isSaldoValido) {
            writeLine("Error. La cantidad mínima para participar son 0.01€. Inténtelo de nuevo."); 
        }

    } while (!isSaldoValido); // se repite hasta que la funcion isValido indique el el saldo introducido es apto para jugar

    ejecutarMenu(ref saldo); // comienza la simulación

    writeLine("Ha sido un placer 😉"); // fin del programa

}



procedure ejecutarMenu(ref decimal saldo) {

    int opcionElegida = 0; // inicializada a 0 para garantizar la 1a entrada al 'do-while'


    do {

        writeLine("----------------------");
        writeLine("Elija una opción:");
        writeLine("1.- Tirar de la tragaperras.");
        writeLine("2.- Gestionar saldo.");
        writeLine("3.- Ver premios.");
        writeLine("4.- Salir.");
        writeLine("Opción elegida = ");
        opcionElegida = (int)readLine();

        switch (opcionElegida) {

            case 1:
                tirarTragaperras(ref saldo); // tiramos de la tragaperras, e independientemente de lo que pase volverá a imprimir el menú al acabar la tirada
                break;
            
            case 2:
                gestionarSaldo(ref saldo); // añadimos, retiramos o simplemente vemos el salario, y vuelve a imprimir el menú
                break;

            case 3:
                imprimirListaPremios(); // imprime los premios de las posibles convinaciones y vuelve a mostrar el menú
                break;

            case 4:
                writeLine("Ha sido un placer."); // sale
                break;

            default:
                writeLine("Opción no válida. Introduzca una opción de las 4 posibles.");
                break;

        }

    } while (opcionElegida != 4); // se repite hasta que se indica la 4a opción, salir del programa.
}



procedure tirarTragaperras (ref decimal saldo) {

    decimal saldoApostado; // importante almacenarlo para poder modificarlo en base a la tirada
    bool isSaldoValido;


    writeLine("¿Cuánto saldo desea apostar en la tirada?: ");
    saldoApostado = (decimal)readLine(); // fallo si se introduce texto

    // llamada a la funcion que verifica que el saldo no sea negativo ni 0 (L41)
    isSaldoValido = isSuperiorA0(saldoApostado);

    if (!isSaldoValido || (saldoApostado > saldo)) { // si entra aquí no llevará acabo la tirada y volverá directamente a ejecutarMenu

        writeLine("El saldo apostado no puede ser superior al saldo ni inferior a 0.01€ (apuesta mínima).");


    } else { // solo entra aquí si el saldo apostado es válido

        // restamos el saldo apostado, después en base al resultado se devolverá X cantidad o se quedará igual
        saldo -= saldoApostado; 

        // generamos la tirada
        int numeroAleatorio1 = Math.random(0, 9);
        int numeroAleatorio2 = Math.random(0, 9);
        int numeroAleatorio3 = Math.random(0, 9);


        // lo que va a continuacion se podria meter en una funcion llamada calcularPremio a la que se le pasasen los numeros de la tirada

        // caso 777
        if ((numeroAleatorio1 == numeroAleatorio2) && (numeroAleatorio1 == numeroAleatorio3) && (numeroAleatorio1 == 7)) {

            saldo += 10 * saldoApostado;
            writeLine("JACKPOT!!");
            writeLine("La tragaperras muestra: " + numeroAleatorio1 + " " + numeroAleatorio2 + " " + numeroAleatorio3);
            writeLine("Saldo actual: " + saldo + "€");

        // caso 3 iguales pero no son 7
        } else if ((numeroAleatorio1 == numeroAleatorio2) && (numeroAleatorio1 == numeroAleatorio3) && (numeroAleatorio1 != 7)) {

            saldo += 3 * saldoApostado;
            writeLine("VICTORIA!!");
            writeLine("La tragaperras muestra: " + numeroAleatorio1 + " " + numeroAleatorio2 + " " + numeroAleatorio3);
            writeLine("Saldo actual: " + saldo + "€");

        // caso n1 = n2 != n3, n2 = n3 != n1 y n1 = n3 != n2. 2 números iguales
        } else if ((numeroAleatorio1 == numeroAleatorio2) && (numeroAleatorio1 != numeroAleatorio3) || 
                   (numeroAleatorio2 == numeroAleatorio3) && (numeroAleatorio1 != numeroAleatorio2) ||
                   (numeroAleatorio1 == numeroAleatorio3) && (numeroAleatorio2 != numeroAleatorio1) ) {

            saldo += 1.5 * saldoApostado;
            writeLine("SALVADO!!");
            writeLine("La tragaperras muestra: " + numeroAleatorio1 + " " + numeroAleatorio2 + " " + numeroAleatorio3);
            writeLine("Saldo actual: " + saldo + "€");

        // caso ninguno igual        
        } else {

            writeLine("MALA SUERTE!!");
            writeLine("La tragaperras muestra: " + numeroAleatorio1 + " " + numeroAleatorio2 + " " + numeroAleatorio3);
            writeLine("Saldo actual: " + saldo + "€");
        }
    }

}



function gestionarSaldo (ref decimal saldo) {

    int opcionElegida = 0; // inicializada a 0 para garantizar la 1a entrada al 'do-while'
    decimal saldoIntroducido;
    bool isSaldoIntroducidoInvalido = false; // un saldo no introducido no puede ser invalido

    writeLine("Saldo actual = " + saldo + "€");
    writeLine("¿Qué desea hacer?");
    writeLine("1.- Añadir saldo.");
    writeLine("2.- Retirar saldo.");
    writeLine("3.- Volver al menú.");
    writeLine("Opción elegida = ");
    opcionElegida = (int)readLine();

    switch (opcionElegida) {
        
        case 1:

            writeLine("Saldo a añadir: ");
            saldoIntroducido = (decimal)readLine();

            // verificacion de que se introduzca al menos 1
            isSaldoIntroducidoInvalido = isNegativo(saldoIntroducido);

            // validacion de que se vaya a añadir al menos 1 céntimo
            if (isSaldoIntroducidoInvalido) {
                writeLine("No se puede introducir un saldo negativo.");
            } else {
                saldo += saldoIntroducido; // sumamos el saldo a sumar al saldo actual
            }
            break;

        case 2: 
            writeLine("Saldo a retirar: ");
            saldoIntroducido = (decimal)readLine();

            isSaldoIntroducidoInvalido = isNegativo(saldoIntroducido);

            // validación de que no se retire dinero negativo ni más de lo que se tiene
            if (isSaldoIntroducidoInvalido) {
                
                writeLine("Error. No se puede introducir un saldo negativo.");

            } else if (saldoIntroducido > saldo){

                writeLine("Error. No puedes retirar más de lo que tienes.");

            } else {

                saldo -= saldoIntroducido;
            }
            break;

        case 3: 

            writeLine("Volviendo al menú...");
            break;
        
        default:

            writeLine("Error. Opción no válida");
            break;
    }
}



procedure imprimirListaPremios {

    writeLine("Posibles premios:");
    writeLine("- Si no coincide ningún número pierdes el dinero apostado.");
    writeLine("- Si sólo coinciden 2 números, sean cuales sean recuperas un x1.5 de lo apostado.");
    writeLine("- Si coinciden los 3 números recuperas un x3 de lo apostado excepto si los números que coinciden son 777.");
    writeLine("- Si coinciden  7 7 7 recuperas un x10 de lo apostado."); // jackpot
}




// funcion para verificar que el saldo no sea 0 o negativo
// usamos early return para salir directamente de la funcion en caso de que el saldo no sea valido
function bool isSuperiorA0(decimal saldo) {

    if (saldo <= 0.0) {
        return false; 
    }
    return true;
}

// funcion para verificar que el número no sea negativo
// usamos early return para salir directamente de la funcion en caso de que el número no sea valido
function bool isNegativo(decimal num) {

    if (num < 0.0) {
        return true; 
    }
    return false;
}
```
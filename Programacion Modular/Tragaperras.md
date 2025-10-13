### Implementar una simulación de una máquina tragaperras. 

``` bash
Main {

    decimal saldo;

    bool isSaldoValido = true;


    writeLine("Bienvenido a la Máquina Tragaperras");

    do {

        writeLine("¿Con cuánto saldo deseas iniciar? (€): ");
        saldo = (decimal)readLine();

        isSaldoValido = verificarSaldo(saldo);

        if (!isSaldoValido) {
            writeLine("ERROR. La cantidad mínima para participar son 0.01€. Inténtelo de nuevo."); 
        }

    } while (!isSaldoValido);

    imprimirMenu();


}


function bool verificarSaldo(decimal saldo) {

    if (saldo <= 0.0) {
        return false; 
    }
    return true;
}

procedure imrimirListaPremios {

    writeLine("Posibles premios:");
    writeLine("- Si no coincide ningún número pierdes el dinero apostado.");
    writeLine("- Si sólo coinciden 2 números, sean cuales sean recuperas un x1.5 de lo apostado.");
    writeLine("- Si coinciden los 3 números recuperas un x3 de lo apostado excepto si los números que coinciden son 777.");
    writeLine("- Si coinciden  7 7 7 recuperas un x10 de lo apostado.");
}



```
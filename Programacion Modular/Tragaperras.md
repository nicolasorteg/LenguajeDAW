### Implementar una simulación básica de una máquina tragaperras. 

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



```
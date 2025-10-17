``` bash

using Math; // importamos la librería math

const int PIEDRA = 1;
const int PAPEL = 2;
const int TIJERA = 4;

Main {

    string participante;

    writeLine("Bienvenido a la simulación de Piedra, Papel o Tijera!! ");
    
    writeLine("Nombre del participante: ");
    participante = readLine(); // no es necesario el casting explícito ya que readLine lee y pasa a un string

    writeLine("Un placer " + participante);

    ejecutarMenu(participante);
}

procedure ejecutarMenu(string participante) {

    int opcionElegida = 0;

    do {
        writeLine("------------------------");
        writeLine("Elija una opción " + participante ":");
        writeLine("1.- Empezar la partida.");
        writeLine("2.- Enfrentarse al Jefe Final.");
        writeLine("3.- Probabilidades.");
        writeLine("4.- Salir.")
        opcionElegida = (int)readLine();

        switch (opcionElegida) {

            case 1:
                simularRonda(participante);
                break;

            case 2:
                simularJefe(participante);
                break;

            case 3:
                mostrarProbabilidades();
                break;

            case 4:
                writeLine("Ha sido un placer " + participante + " 😉");
                break;

            default:
                writeLine("❌ERROR❌ Opción introducida no válida. Por favor, introduce una opción del 1-4.");
                break;

        } 

    } while (opcion != 4);
}


procedure simularRonda(string participante) {

    int opcionElegida;
    int opcionOrdenador;
    int puntuacionParticipante;
    int puntuacionOrdenador;
    int ganador;

    writeLine("------------------");
    writeLine("Comienza la ronda.");



    writeLine("1 = Piedra");
    writeLine("2 = Papel");
    writeLine("3 = Tijera");
    writeLine("Opción elegida: ");
    opcionElegida = (int)readLine();

    opcionOrdenador = Math.random(1, 3);

    ganador = verificarResultado(opcionElegida, opcionOrdenador, puntuacionParticipante, puntuacionOrdenador);


}

function int verificarResultado(int opcionElegida, int opcionOrdenador, int puntuacionParticipante, puntuacionOrdenador) {


    switch()

}












procedure mostrarProbabilidades {

    writeLine("------------------------");
    writeLine("PROBABILIDADES PARTIDA NORMAL");
    writeLine("Probabilidades de victoria: 33%");
    writeLine("Probabilidades de empate: 33%");
    writeLine("Probabilidades de perder: 33%");
    writeLine("------------------------");
    writeLine("PROBABILIDADES JEFE");
    writeLine("Probabilidades de victoria: 33%");
    writeLine("Probabilidades de empate: 0%");
    writeLine("Probabilidades de perder: 66%");

}
```
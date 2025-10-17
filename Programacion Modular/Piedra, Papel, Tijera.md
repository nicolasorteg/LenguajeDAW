``` bash

using Math; // importamos la librería math

Main {

    string participante;

    writeLine("Bienvenido a la simulación de Piedra, Papel o Tijera!! ");
    
    writeLine("Nombre del participante: ");
    participante = readLine();

    writeLine("Un placer " + participante);

    ejecutarMenu(participante);
}


procedure ejecutarMenu(string participante) {

    int victorias = 0; // la sesion empieza con 0 victorias
    int opcionElegida = 0;

    do {
        writeLine("------------------------");
        writeLine("Elija una opción " + participante + ":");
        writeLine("1.- Empezar la partida.");
        writeLine("2.- Enfrentarse al Jefe Final.");
        writeLine("3.- Probabilidades.");
        writeLine("4.- Salir.");
        opcionElegida = (int)readLine();

        switch (opcionElegida) {

            case 1:
                simularRonda(participante, ref victorias);
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

    } while (opcionElegida != 4);
}


procedure simularRonda(string participante, ref int victorias) {

    int opcionElegida;
    int opcionOrdenador;
    int puntuacionParticipante = 0;
    int puntuacionOrdenador = 0;

    writeLine("------------------");
    writeLine("Comienza la ronda.");


    do {
        writeLine("-----------");
        writeLine("1 = Piedra");
        writeLine("2 = Papel");
        writeLine("3 = Tijera");
        writeLine("Opción elegida: ");
        opcionElegida = (int)readLine();

        opcionOrdenador = Math.random(1, 3);

        verificarResultado(opcionElegida, opcionOrdenador, ref puntuacionParticipante, ref puntuacionOrdenador);

    } while ((puntuacionParticipante < 2) && (puntuacionOrdenador < 2)); // al mejor de 3 (primero que gane 2)

    if (puntuacionParticipante > puntuacionOrdenador) {

        victorias += 1;
        writeLine("ENHORABUENA 😀 Has ganado. +1 Victoria");
        writeLine("Victorias totales: " + victorias);

    } else {

        writeLine("Mala suerte 😔 Más suerte la próxima vez!");
        writeLine("Victorias totales: " + victorias);
    }
}


procedure verificarResultado(int opcionElegida, int opcionOrdenador, ref int puntuacionParticipante, ref int puntuacionOrdenador) {

    
    const int PIEDRA = 1;
    const int PAPEL = 2;
    const int TIJERA = 3;


    switch(opcionElegida) {

        case 1: // usuario Piedra
            
            if (opcionOrdenador == PIEDRA) {

                writeLine("Sacaste Piedra...");
                writeLine("El ordenador saca... PIEDRA! Puntuaciones:");
                writeLine("Marcador actual -> Jugador: " + puntuacionParticipante + " | Ordenador: " + puntuacionOrdenador);

            } else if (opcionOrdenador == PAPEL) {

                puntuacionOrdenador += 1;

                writeLine("Sacaste Piedra...");
                writeLine("El ordenador saca... PAPEL! Puntuaciones:");
                writeLine("Marcador actual -> Jugador: " + puntuacionParticipante + " | Ordenador: " + puntuacionOrdenador);
                
            } else if (opcionOrdenador == TIJERA) {

                puntuacionParticipante += 1;

                writeLine("Sacaste Piedra...");
                writeLine("El ordenador saca... TIJERAS! Puntuaciones:");
                writeLine("Marcador actual -> Jugador: " + puntuacionParticipante + " | Ordenador: " + puntuacionOrdenador);
                
            } 

            break;


        case 2: // usuario Papel
        
            if (opcionOrdenador == PIEDRA) {

                puntuacionParticipante += 1;

                writeLine("Sacaste Papel...");
                writeLine("El ordenador saca... PIEDRA! Puntuaciones:");
                writeLine("Marcador actual -> Jugador: " + puntuacionParticipante + " | Ordenador: " + puntuacionOrdenador);
                
            } else if (opcionOrdenador == PAPEL) {

                writeLine("Sacaste Papel...");
                writeLine("El ordenador saca... PAPEL! Puntuaciones:");
                writeLine("Marcador actual -> Jugador: " + puntuacionParticipante + " | Ordenador: " + puntuacionOrdenador);
                
            } else if (opcionOrdenador == TIJERA) {

                puntuacionOrdenador += 1;

                writeLine("Sacaste Papel...");
                writeLine("El ordenador saca... TIJERAS! Puntuaciones:");
                writeLine("Marcador actual -> Jugador: " + puntuacionParticipante + " | Ordenador: " + puntuacionOrdenador);
                
            } 
            break;


        case 3: // usuario Tijera

            if (opcionOrdenador == PIEDRA) {

                puntuacionOrdenador += 1;

                writeLine("Sacaste Tijera...");
                writeLine("El ordenador saca... PIEDRA! Puntuaciones:");
                writeLine("Marcador actual -> Jugador: " + puntuacionParticipante + " | Ordenador: " + puntuacionOrdenador);

            } else if (opcionOrdenador == PAPEL) {

                puntuacionParticipante += 1;

                writeLine("Sacaste Tijera...");
                writeLine("El ordenador saca... PAPEL! Puntuaciones:");
                writeLine("Marcador actual -> Jugador: " + puntuacionParticipante + " | Ordenador: " + puntuacionOrdenador);

            } else if (opcionOrdenador == TIJERA) {

                writeLine("Sacaste Tijera...");
                writeLine("El ordenador saca... TIJERAS! Puntuaciones:");
                writeLine("Marcador actual -> Jugador: " + puntuacionParticipante + " | Ordenador: " + puntuacionOrdenador);

            } 
            break;

        default: // usuario cualquier otro numero
        
            writeLine("❌ERROR❌ Opción introducida no válida. Por favor, introduce una opción del 1-3.");
            break;
    }
}












procedure mostrarProbabilidades() {

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
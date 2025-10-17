``` bash

using Math; // importamos la librería math

const int OPCION_SALIR = 4; // se almacena en una constante para que si en futuras actualizaciones 
                            // se implementan mas opciones, solo haya que tocar aquí

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
        writeLine(OPCION_SALIR + ".- Salir.");
        
        try {
            opcionElegida = (int)readLine();

            switch (opcionElegida) {

                case 1:
                    simularRonda(participante, ref victorias);
                    break;

                case 2:
                    simularJefe(participante, ref victorias);
                    break;

                case 3:
                    mostrarProbabilidades(victorias);
                    break;

                case OPCION_SALIR:
                    writeLine("Ha sido un placer " + participante + " 😉");
                    break;

                default:
                    writeLine("❌ERROR❌ Opción introducida no válida. Por favor, introduce una opción de las " + OPCION_SALIR + " posibles.");
                    break;

            } 
        } catch (Exception e) {

            writeLine("❌ Error de formato. Debe introducir un número entero. Volviendo al menú...");
            opcionElegida = 0; // fuerza la repetición del bucle
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

        try {
            opcionOrdenador = Math.random(1, 3);

            verificarResultado(opcionElegida, opcionOrdenador, ref puntuacionParticipante, ref puntuacionOrdenador);

        } catch (Exception e) {

            writeLine("❌ Error de formato. Debe introducir un número entero 1-3. Volviendo a la elección de figura...");
        }


    } while ((puntuacionParticipante < 2) && (puntuacionOrdenador < 2)); // al mejor de 3 (primero que gane 2)

    if (puntuacionParticipante > puntuacionOrdenador) {

        victorias += 1;
        writeLine("ENHORABUENA " + participante + " 😀 Has ganado. +1 Victoria");
        writeLine("Victorias totales: " + victorias);

    } else {

        writeLine("Mala suerte " + participante + " 😔 Más suerte la próxima vez!");
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



procedure simularJefe(string participante, ref int victorias) {

    int opcionElegida;
    int opcionOrdenador;
    int puntuacionParticipante = 0;
    int puntuacionOrdenador = 0;
    

    if (victorias < 5) {

        writeLine("Aún no estás preparado para esta batalla. Sigue entrenando hasta obtener 5 victorias.");

    } else {

        writeLine("Bienvenido a la Batalla Final. Espero que te hayas preparado bien " + participante + ", esto no va a ser tan fácil...");
        writeLine("Comienza la partida");

        do {
            writeLine("-----------");
            writeLine("1 = Piedra");
            writeLine("2 = Papel");
            writeLine("3 = Tijera");
            writeLine("Opción elegida: ");
            opcionElegida = (int)readLine();

            try {
                opcionOrdenador = generarRespuestaJefe(opcionElegida);

                verificarResultado(opcionElegida, opcionOrdenador, ref puntuacionParticipante, ref puntuacionOrdenador);

            } catch (Exception e) {

                writeLine("❌ Error de formato. Debe introducir un número entero 1-3. Volviendo a la elección de figura...");

            }

        } while ((puntuacionParticipante < 3) && (puntuacionOrdenador < 3)); // al mejor de 5 (primero que gane 3)

        if (puntuacionParticipante > puntuacionOrdenador) {

            writeLine("ENHORABUENA!! Has logrado vencer el Jefe de este Reino. Toma este merecido premio -> 👑");

        } else {

            victorias -= 2;
            writeLine("PERDISTE!! Lamentablemente, el jefe no solo te ha ganado, sino que además se ha quedado con 2 de tus victorias...");

            writeLine("Victorias tras la derrota -> " + victorias);
        }
    }

}


function int generarRespuestaJefe(int opcionElegida) {

    int opcionOrdenador;

    if (opcionElegida == 1) { // usuario Piedra

        opcionOrdenador = Math.random(1, 3);

        switch (opcionOrdenador) { // si es Piedra, 66% de sacar Papel (return 2) y 33% de Tijera
            case 1:
            case 2:

                return 2;

            case 3:

                return 3;
        }

    } else if(opcionElegida == 2) { // si es Papel, 66% de sacar Tijera y 33% de Piedra

        opcionOrdenador = Math.random(1, 3);

        switch (opcionOrdenador) {
            case 1:

                return 1;

            case 2:
            case 3:

                return 3;
        }

    } else if (opcionElegida == 3) { // si es Tijera, 66% de sacar Piedra y 33% de Papel

        opcionOrdenador = Math.random(1, 3);

        switch (opcionOrdenador) {

            case 1:
            case 3:
                return 1;
                break;

            case 2:
                return 3;
                break;
        }

    } 
    return 0;
}





procedure mostrarProbabilidades(int victorias) {

    writeLine("------------------------");
    writeLine("PROBABILIDADES PARTIDA NORMAL");
    writeLine("Probabilidades de victoria: 33%");
    writeLine("Probabilidades de empate: 33%");
    writeLine("Probabilidades de perder: 33%");
    writeLine("------------------------");
    writeLine("PROBABILIDADES JEFE");

    if (victorias < 5) {

        writeLine("Aún no estás listo... Vuelve cuando tengas al menos 5 victorias.");

    } else {

        writeLine("Probabilidades de victoria: 33%");
        writeLine("Probabilidades de empate: 0%");
        writeLine("Probabilidades de perder: 66%");
    }
}
```
``` bash

// importamos la librería math
using Math; 


// constantes para el menú principal, imprescinble para la sostenibilidad del código, ya que si se añaden más opciones de esta forma será más sencillo modificarlo
const int OPCION_MENU_RONDA = 1;
const int OPCION_MENU_JEFE = 2;
const int OPCION_MENU_PROBABILIDADES = 3;
const int OPCION_MENU_SALIR = 4; 

// constantes para identificar las figuras usuadas por el usuario, muy útil para mejorar la legibilidad del código
const int PIEDRA = 1;
const int PAPEL = 2;
const int TIJERA = 3;

Main {

    string participante;

    writeLine("👋 Bienvenido a la simulación de Piedra, Papel o Tijera!! ");
    
    writeLine("Nombre del participante: ");
    participante = readLine();

    writeLine("Un placer " + participante + " 😊");

    ejecutarMenu(participante); // comienza la simulación

    writeLine("Fin del programa.");
}

/*
Se encarga de imprimir el menu por pantalla que contine toda la simulacion
Se le pasa el nombre del participante
*/
procedure ejecutarMenu(string participante) {

    int victorias = 0; // la sesion empieza con 0 victorias
    int opcionElegida = 0; // inicializamos a 0 para garantizar la primera entrada al bucle


    do {
        writeLine("------------------------");
        writeLine("Elija una opción " + participante + ":");
        writeLine(OPCION_MENU_RONDA + ".- 👾 Empezar la partida.");
        writeLine(OPCION_MENU_JEFE + ".- 😈 Enfrentarse al Jefe Final.");
        writeLine(OPCION_MENU_PROBABILIDADES + ".- 🤷‍♀️ Probabilidades.");
        writeLine(OPCION_MENU_SALIR + ".- 😔 Salir.");
        
        // llamamos a la funcion que valida que lo que se introduzca es un entero, de no serlo se repite la pregunta hasta que lo sea
        opcionElegida = leerEntero("Opción elegida: "); 

        switch (opcionElegida) {

            case OPCION_MENU_RONDA: // introduce 1
                simularPartida(participante, ref victorias); // comienza la simulacion de la partida normal
                break;

            case OPCION_MENU_JEFE: // introduce 2
                simularJefe(participante, ref victorias); // comienza la simulacion de la partida contra el jefe
                break;

            case OPCION_MENU_PROBABILIDADES: // introduce 3
                mostrarProbabilidades(victorias); // muestra las probabilidades de ambos tipos de partidas
                break;

            case OPCION_MENU_SALIR: // introduce 4
                writeLine("Ha sido un placer " + participante + " 😉"); // imprime despedida y se sale del bucle, FIN DEL PROGRAMA
                break;

            default: // si se introduce un num que no esté entre las opciones
                writeLine("❌ Opción introducida no válida. Por favor, introduce una opción de las " + OPCION_MENU_SALIR + " posibles."); 
                break;

        } 

        
    } while (opcionElegida != OPCION_MENU_SALIR); // el menu se repite hasta que no se introduzca la opcion salir, en esta version es la 4
}


/*
Esta función se encarga de simular la partida normal.
Se le pasa el nombre del participante y el número de victorias por referencia. Esto último es importante para que se guarde bien en caso de que gane.
*/
procedure simularPartida(string participante, ref int victorias) {

    // variables requeridas para la simulacion
    int opcionElegida;
    int opcionOrdenador;
    int puntuacionParticipante = 0; // inicializada para garantizar 
    int puntuacionOrdenador = 0;    // el comienzo 0-0

    writeLine("------------------");
    writeLine("Bienvenido a la zona de juego...");
    writeLine("⚔ Comienza la partida ⚔");


    do {
        writeLine("-----------");
        writeLine(PIEDRA + " = Piedra");
        writeLine(PAPEL + " = Papel");
        writeLine(TIJERA + " = Tijera");

        opcionElegida = leerEntero("Opción elegida: "); // llama a leerEntero que valida que la opcion introducida sea un entero

        if (opcionElegida >= 1 && opcionElegida <= 3) { // si se introduce algo del 1-3
            
            opcionOrdenador = Math.random(1, 3); // cada vez que pasa una ronda, el usuario elije otra figura y el ordenador genera otra

            // se llama a la funcion que, en base al numero introducido y al numero generado, suma la puntuacion a uno o a otro
            verificarResultado(opcionElegida, opcionOrdenador, ref puntuacionParticipante, ref puntuacionOrdenador); 
            
        } else { // si se introduce un valor que no este entre 1-3
            
            writeLine("❌ Opción introducida no válida. Por favor, introduce una opción del 1-3.");
        }


    } while ((puntuacionParticipante < 2) && (puntuacionOrdenador < 2)); // al mejor de 3 (primero que gane 2)

    if (puntuacionParticipante > puntuacionOrdenador) { // en caso de que gane el usuario

        victorias += 1; // victorias vino pasada por referencia, muy imporante
        writeLine("ENHORABUENA " + participante + " 😀 Has ganado. +1 Victoria");
        writeLine("Victorias totales: " + victorias);

    } else { // no se pone la condicion (puntuacionParticipante < puntuacionOrdenador) ya que es la única opcion que queda, y el = es imposible

        writeLine("Mala suerte " + participante + " 😔 Más suerte la próxima vez!");
        writeLine("Victorias totales: " + victorias); // no modificadas
    }
}


/*
Esta función se encarga de simular la partida contra el Jefe.
Se le pasa el nombre del participante y el número de victorias por referencia. Esto último es importante para que se guarde bien en caso de perder la partida.
*/
procedure simularJefe(string participante, ref int victorias) {

    // variables requeridas para la simulacion
    int opcionElegida;
    int opcionOrdenador;
    int puntuacionParticipante = 0;
    int puntuacionOrdenador = 0;
    

    if (victorias < 5) { // si no tiene al menos 5 victorias (>=) no puedes acceder a la pelea

        writeLine("Aún no estás preparado para esta batalla. Sigue entrenando hasta obtener 5 victorias.");
        writeLine("Mucha suerte, la necesitarás 😬");

    } else { // toda la simulacion va aqui dentro para garantizar que solo pueda entrar con 5 victorias en partidas normales

        writeLine("Bienvenido a la Batalla Final 😈. Espero que te hayas preparado bien " + participante + ", esto no va a ser tan fácil...");
        writeLine("⚔ Comienza la Batalla Final ⚔");

        do {
            writeLine("-----------");
            writeLine("1 = Piedra");
            writeLine("2 = Papel");
            writeLine("3 = Tijera");

            // mismo tipo de validación que en simularPartida
            opcionElegida = leerEntero("Opción elegida: ");

            if (opcionElegida >= 1 && opcionElegida <= 3) {
                
                // esta vez necesitamos una funcion que genere la figura del ordenador en base a lo que escriba el usuario
                opcionOrdenador = generarRespuestaJefe(opcionElegida); 
                verificarResultado(opcionElegida, opcionOrdenador, ref puntuacionParticipante, ref puntuacionOrdenador);

            } else { // si no pasa la validacion de leerEntero o si no se introduce un valor del 1-3

                writeLine("❌ Opción introducida no válida. Debe ser 1, 2 o 3.");
            }

        } while ((puntuacionParticipante < 3) && (puntuacionOrdenador < 3)); // al mejor de 5 (primero que gane 3)

        if (puntuacionParticipante > puntuacionOrdenador) {

            writeLine("ENHORABUENA!! Has logrado vencer el Jefe de este Reino. Toma este merecido premio -> 👑");

        } else {

            victorias -= 2; // pasada por referencia, importante
            writeLine("PERDISTE!! Lamentablemente, el jefe no solo te ha ganado, sino que además se ha quedado con 2 de tus victorias 😖");

            writeLine("Victorias tras la derrota -> " + victorias);
        }
    }

}


/*
Esta función se encarga de, en base a la opcion elegida por el usuario, generar la figura del Jefe. 
Esto se hace asi para garantizar las probabilidades especificadas en mostrarProbabilidades.
Se le pasa la opcion que elije el usuario.
*/
function int generarRespuestaJefe(int opcionElegida) {

    int opcionOrdenador;

    if (opcionElegida == PIEDRA) { // usuario Piedra

        opcionOrdenador = Math.random(1, 3);

        switch (opcionOrdenador) { // si es Piedra, 66% de sacar Papel (return 2) y 33% de Tijera
            case PIEDRA:
            case PAPEL:

                return PAPEL;
                break;

            case TIJERA:

                return TIJERA;
                break;
        }

    } else if(opcionElegida == PAPEL) { // si es Papel, 66% de sacar Tijera y 33% de Piedra

        opcionOrdenador = Math.random(1, 3);

        switch (opcionOrdenador) {
            case PIEDRA:

                return PIEDRA;
                break;

            case PAPEL: 
            case TIJERA:

                return TIJERA;
                break;
        }

    } else if (opcionElegida == TIJERA) { // si es Tijera, 66% de sacar Piedra y 33% de Papel

        opcionOrdenador = Math.random(1, 3);

        switch (opcionOrdenador) {

            case PIEDRA:
            case TIJERA:
                return PIEDRA;
                break;

            case PAPEL:
                return PAPEL;
                break;
        }

    } 
    return 0; // nunca devolvera 0 ya que como se lleva acabo antes una doble validacion, si se llega a este punto, opcionElegida siempre sera 1,2 o 3
}


/*
Muesta las probabilidades que tiene el usuario de ganar al ordenador en cada ronda
Se le pasa el numero de victorias para garantizar que solo puede acceder a las probabilidades de la pelea final si la tiene desbloqueada
*/
procedure mostrarProbabilidades(int victorias) {

    writeLine("------------------------");
    writeLine("👾 PROBABILIDADES PARTIDA NORMAL");
    writeLine("- Probabilidades de victoria: 33%");
    writeLine("- Probabilidades de empate: 33%");
    writeLine("- Probabilidades de perder: 33%");
    writeLine("------------------------");
    writeLine("😈 PROBABILIDADES JEFE");

    if (victorias < 5) {

        writeLine("Aún no estás listo... Vuelve cuando tengas al menos 5 victorias.");

    } else {

        writeLine("- Probabilidades de victoria: 33%");
        writeLine("- Probabilidades de empate: 0%");
        writeLine("- Probabilidades de perder: 66%");
    }
}


/*
Procedimiento vital, se encarga de revisar las opciones elegidas por el usuario y el ordenador, y en base a eso, suma a la puntuacion de uno u otro.
Se le pasan las opciones elegidas por ambos y las puntuaciones por REFERENCIA, muy importante para que se registren los cambios
*/
procedure verificarResultado(int opcionElegida, int opcionOrdenador, ref int puntuacionParticipante, ref int puntuacionOrdenador) {


    switch(opcionElegida) {

        case PIEDRA: // usuario Piedra
            if (opcionOrdenador == PIEDRA) { // empate, no hay sumas en las puntuaciones
                mostrarMarcador("Piedra", "PIEDRA", puntuacionParticipante, puntuacionOrdenador); // declarada justo debajo de esta funcion

            } else if (opcionOrdenador == PAPEL) { // gana ordenador
                puntuacionOrdenador += 1;
                mostrarMarcador("Piedra", "PAPEL", puntuacionParticipante, puntuacionOrdenador);

            } else if (opcionOrdenador == TIJERA) { // gana usuario
                puntuacionParticipante += 1;
                mostrarMarcador("Piedra", "TIJERAS", puntuacionParticipante, puntuacionOrdenador);
            }
            break;


        case PAPEL: // usuario Papel
            if (opcionOrdenador == PIEDRA) { // gana usuario
                puntuacionParticipante += 1;
                mostrarMarcador("Papel", "PIEDRA", puntuacionParticipante, puntuacionOrdenador);

            } else if (opcionOrdenador == PAPEL) { // empate, no hay sumas en las puntuaciones
                mostrarMarcador("Papel", "PAPEL", puntuacionParticipante, puntuacionOrdenador);

            } else if (opcionOrdenador == TIJERA) { // gana ordenador
                puntuacionOrdenador += 1;
                mostrarMarcador("Papel", "TIJERAS", puntuacionParticipante, puntuacionOrdenador);
            }
            break;


        case TIJERA: // usuario Tijera
            if (opcionOrdenador == PIEDRA) { // gana ordenador
                puntuacionOrdenador += 1;
                mostrarMarcador("Tijera", "PIEDRA", puntuacionParticipante, puntuacionOrdenador);

            } else if (opcionOrdenador == PAPEL) { // gana usuario
                puntuacionParticipante += 1;
                mostrarMarcador("Tijera", "PAPEL", puntuacionParticipante, puntuacionOrdenador);

            } else if (opcionOrdenador == TIJERA) { // empate, no hay sumas en las puntuaciones
                mostrarMarcador("Tijera", "TIJERAS", puntuacionParticipante, puntuacionOrdenador);
            }
            break;

        default: // usuario cualquier otro numero
        
            writeLine("❌ERROR❌ Opción introducida no válida. Por favor, introduce una opción del 1-3.");
            break;
    }
}

/*
Para no hacer verificarResultado tan grande, se crea este procedimiento que simplemente imprime como va la partida
Se le pasan los datos que necesita imprimir. Como no va a modificar ninguno no se usa el paso por referencia
*/
procedure mostrarMarcador(string jugadaUsuario, string jugadaOrdenador, int puntosUsuario, int puntosOrdenador) {
    writeLine("Sacaste " + jugadaUsuario + "...");
    writeLine("El ordenador saca... " + jugadaOrdenador + "!");
    writeLine("Marcador actual -> Jugador: " + puntosUsuario + " | Ordenador: " + puntosOrdenador);
}

/*
Se encarga de verificar que un numero introducido por teclado sea un numero entero mediante un try-catch
Se le pasa el mensaje donde el usuario escribe el numero.
*/
function int leerEntero(string mensaje) {

    int valorLeido = 0;
    bool isFormatoCorrecto = false; //flag

    do {
        writeLine(mensaje);
        try {
            valorLeido = (int)readLine(); 
            isFormatoCorrecto = true;
        } catch (Exception e) {
            writeLine("❌ Error de formato. Debe introducir un número entero. Inténtelo de nuevo.");
        }
    } while (!isFormatoCorrecto);

    return valorLeido; // devuelve el valor leido, no lo hace hasta que sea valido
}
```
### Determinar si un número entero introducido por teclado es primo, utilizando un bucle controlado por un indicador (bandera o flag)

``` bash 
Main {
    
    int num;
    bool isNegativo = false;
    bool isPrimo = true;

    writeLine("Comprobación de Número Primo.");

    do {

        writeLine("Introduce un número: "); // 5
        num = (int)readLine();

        if (num <= 1) { // 0 entradas

            writeLine("Por definición, para que un número pueda ser primo debe ser mayor que 2. Introduzca un número mayor o igual a 2.")
            isPrimo = false;
            isNegativo = true;

        } else {

            int i = 2;
            while (i * i <= num && isPrimo) { // 1 entradas

                if (num % i == 0) { // 0 entradas

                    isPrimo = false;

                }

                i += 1;

            }
        }

        if (isPrimo) {

            writeLine("El número " + num + " es primo"); // resultado esperado

        } else {

            writeLine("El número " + num + " no es primo");
            
        }
    } while (isNegativo); // 1 entrada
}
```

### Explicación

Para que un número sea primo debe ser divisible **solo** entre 1 y si mismo, en el momento en el que es divisible entre cualquier otro número deja de ser primo. 
Teniendo en cuenta esta definición, necesitamos un algoritmo que revise que el número introducido no sea divisible por ningún número **a partir del 2**. 
¿Por qúe a partir del 2? Porque todos los números positivos son divisibles entre 1.
Entonces, para llevar a cabo este algoritmo hacemos uso de un bucle indefinido ya que no sabemos cuando vamos a acabar, en este caso while y no do-while ya que no queremos que el programa entre 1-N veces, queremos que revise siempre antes de entrar al bucle. 

Entonces lo importante, ¿por qué la condición del while? Bien, para esto tenemos que partir de la base de que si nosotros queremos dividir un num A entre un num B por ejemplo, este num B deberá ser **inferior o igual a la mitad** del num A. Si nosotros tenemos un 16, el numero máximo que tiene opciones de poder dar un cociente entero es el 8. Esto no quiere decir que todos los numeros inferiores o iguales a la mitad vayan a dar un cociente entero, significa que son posibles candidatos. 

Por esto, lo que hace este algoritmo es verificar que el doble de un número no sea mayor al número dado. La mejor manera de ver esto es poniendo ejemplos:

num = 5, que va a pasar aquí: while (2 * 2 <= 5) esto claramente es verdadero. Una vez entra en el bucle, revisa si la division de 5/2 es entera, y al no serlo no entra en el condicional y se incrementa en 1 la i. Vuelve a revisar al condición del bucle: while (3 * 3 <= 5) esto claramente es falso, por lo que se sale del bucle, pero al ser isPrimo true por defecto, al salir y revisar si es Primo o no dará como resultado true, lo esperado. 

Ahora pongamos un ejemplo de un numero no primo, el 6. En este caso hará la primera entrada y como 6%2 = 0, isPrimo tomará el valor de false, y al intentar volver a entrar como hay un operador AND (&&) que obliga a que isPrimo sea true, este no podrá volver a entrar e imprimirá directamente que no es primo. 
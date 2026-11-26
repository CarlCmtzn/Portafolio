---
layout: default
title: Práctica 2
parent: Tareas
grand_parent: Fundamentos de Programación Y Laboratorio
nav_order: 8
---

# Cálculo de Promedio, Nota Máxima, Nota Mínima y Histograma

```python
#include <stdio.h>
#include <stdlib.h>

//===================================================================//
//                        VALIDACION RANGO                           //
/*
    Parametros:
    min: valor minimo permitido.
    max: valor maximo permitido.

    Proposito:
    Solicitar un numero entero y validar que se encuentre
    dentro del rango especificado.

    La funcion:
    - Verifica que la entrada sea numerica.
    - Verifica que el valor este dentro del rango.
    - Solicita nuevamente el dato en caso de error.

    Retorno:
    Devuelve un numero entero valido dentro del rango.
*/
int ValidarRango(int min, int max)
{
    int n;
    int valido;
    do
    {
        valido = scanf("%d", &n);
        while(getchar() != '\n');
        if(valido != 1 || n < min || n > max)
        {
            printf("Valor Invalido.\n");
        }
    }
    while(valido != 1 || n < min || n > max);
    return n;
}
//===================================================================//

//===================================================================//
//                         CALIFICACIONES                            //
/*
    Parametros:
    calificaciones: arreglo donde se almacenaran las calificaciones.
    n: cantidad de alumnos registrados.

    Proposito:
    Solicitar y almacenar las calificaciones de todos
    los alumnos.

    Cada calificacion:
    - Debe encontrarse entre 0 y 60.
    - Es validada antes de almacenarse.

    Tipo void:
    La funcion no devuelve ningun valor porque modifica
    directamente el arreglo recibido como parametro.
*/
void llenarCalificaciones(int calificaciones[], int n)
{
    int i;
    for(i = 0; i < n; i++)
    {
        printf("Calificacion %d (0-60): ", i + 1);
        calificaciones[i] = ValidarRango(0, 60);
    }
}
//===================================================================//

//===================================================================//
//                       NOTA MAXIMA                                 //
/*
    Parametros:
    calificaciones: arreglo que almacena todas las calificaciones.
    n: cantidad total de alumnos registrados.

    Proposito:
    Recorrer el arreglo de calificaciones para encontrar
    la nota más alta obtenida por los alumnos.

    Retorno:
    Devuelve la calificacion maxima encontrada.
*/
int obtenerMaximo(int calificaciones[], int n)
{
    int max = calificaciones[0];
    int i;
    for(i = 1; i < n; i++)
    {
        if(calificaciones[i] > max)
        {
            max = calificaciones[i];
        }
    }
    return max;
}
//===================================================================//

//===================================================================//
//                       NOTA MINIMA                                 //
/*
    Parametros:
    calificaciones: arreglo que almacena todas las calificaciones.
    n: cantidad total de alumnos registrados.

    Proposito:
    Recorrer el arreglo de calificaciones para encontrar
    la nota más alta obtenida por los alumnos.

    Retorno:
    Devuelve la calificacion minima encontrada.
*/
int obtenerMinimo(int calificaciones[], int n)
{
    int min = calificaciones[0];
    int i;
    for(i = 1; i < n; i++)
    {
        if(calificaciones[i] < min)
        {
            min = calificaciones[i];
        }
    }
    return min;
}
//===================================================================//

//===================================================================//
//                           PROMEDIO                                //
/*
    Parametros:
    calificaciones: arreglo que contiene las calificaciones.
    n: cantidad total de alumnos.

    Proposito:
    Calcular el promedio general de las calificaciones.

    Retorno:
    Devuelve el promedio en formato flotante.
*/
float obtenerPromedio(int calificaciones[], int n)
{
    int suma = 0;
    int i;
    for(i = 0; i < n; i++)
    {
        suma += calificaciones[i];
    }
    return (float)suma / n;
}
//===================================================================//


//===================================================================//
//                           HISTOGRAMA                              //
/*
    Parametros:
    calificaciones: arreglo que almacena las notas de los alumnos.
    n: cantidad total de alumnos.

    Proposito:
    Generar e imprimir un histograma que represente la
    distribucion de las calificaciones por rangos.

    Rangos utilizados:
    notas[0] = 0 - 9
    notas[1] = 10 - 19
    notas[2] = 20 - 29
    notas[3] = 30 - 39
    notas[4] = 40 - 49
    notas[5] = 50 - 59
    notas[6] = 60

    Tipo void:
    La funcion no devuelve valores, solamente
    muestra el histograma en pantalla.
*/
void mostrarHistograma(int calificaciones[], int n)
{
    int notas[7] = {0};
    int i, fila, columna, maxn;
    for(i = 0; i < n; i++)
    {
        notas[calificaciones[i] / 10]++;
    }
    maxn = notas[0];
    for(i = 1; i < 7; i++)
    {
        if(notas[i] > maxn)
        {
            maxn = notas[i];
        }
    }
    for(fila = maxn; fila >= 1; fila--)
    {
        printf("%d >", fila);
        for(columna = 0; columna < 7; columna++)
        {
            if(notas[columna] >= fila)
            {
                printf("####### ");
            }
            else
            {
                printf("        ");
            }
        }
        printf("\n");
    }
    printf("  +-------+-------+-------+-------+-------+-------+-------+\n");
    printf("     0-9    10-19   20-29   30-39   40-49   50-59    60 \n");
}
//===================================================================//

//===================================================================//
//                         FUNCION PRINCIPAL                         //
/*
    Funcion: main

    Proposito:
    Controlar la ejecucion general del programa.

    Desde esta funcion:
    - Se muestra el nombre del autor.
    - Se despliega el menu principal.
    - Se capturan las calificaciones.
    - Se muestran los resultados solicitados.
    - Se administra la memoria dinamica del arreglo.

    El programa permanece en ejecucion hasta que
    el usuario selecciona la opcion de salir.
*/
int main()
{
    int opcion = 0;
    // BANDERA
    int datosCapturados = 0;
    //
    int *calificaciones = NULL;
    int n = 0, max, min;
    float promedio;
    int contador = 0, i;

    printf("Carlos Ruben Salinas Cuamatzin\n");
    printf("Presione ENTER para continuar");
    getchar();

    do
    {
        printf("\n");
        printf("========== MENU ==========\n");
        printf("1. Llenar calificaciones\n");
        printf("2. Nota maxima\n");
        printf("3. Nota minima\n");
        printf("4. Promedio\n");
        printf("5. Histograma\n");
        printf("6. Salir\n");
        printf("Opcion: ");

        opcion = ValidarRango(1, 6);

        switch(opcion)
        {
            case 1:
                printf("Cantidad de alumnos: ");
                n = ValidarRango(1, 50);
                //Libera la memoria de la vriable calificaciones en caso de
                //volverla a usar, solo si ya tenia datos antes.
                if(calificaciones != NULL)
                {
                    free(calificaciones);
                }
                //malloc es para la assignacion dinamica de memoria,
                //usado para el relleno del arreglo
                calificaciones = malloc(n * sizeof(int));
                if(calificaciones == NULL)
                {
                    printf("Error al reservar memoria.\n");
                    return 1;
                }
                llenarCalificaciones(calificaciones, n);
                //IMPORTANTE, datosCapturados es la "bandera", la cual,
                //hara que puedas usar las demas opciones (2-5).
                datosCapturados = 1;
            break;

            case 2:
                //si datosCapturados es 0, no te dejara acceder a esta opcion
                if(datosCapturados)
                {
                    //El contador incrementara siempre que 
                    //la calificacion maxima (previamente guardada con la funcion obtenerMaximo()) se repita
                    contador = 0;   
                    max = obtenerMaximo(calificaciones, n);
                    for(i = 0; i < n; i++)
                    {
                        if(calificaciones[i] == max)
                        {
                            contador++;
                        }
                    }
                    printf("Nota maxima: %d\n", max);
                    printf("Alumnos con esa nota: %d\n", contador);
                }
                else
                {
                    printf("Primero capture las calificaciones.\n");
                }
            break;

            case 3:
                //si datosCapturados es 0, no te dejara acceder a esta opcion
                if(datosCapturados)
                {
                    //El contador incrementara siempre que 
                    //la calificacion minimo (previamente guardada con la funcion obtenerMinimo()) se repita
                    contador = 0;
                    min = obtenerMinimo(calificaciones, n);
                    for(i = 0; i < n; i++)
                    {
                        if(calificaciones[i] == min)
                        {
                            contador++;
                        }
                    }
                    printf("Nota minima: %d\n", min);
                    printf("Alumnos con esa nota: %d\n", contador);
                }
                else
                {
                    printf("Primero capture las calificaciones.\n");
                }
            break;

            case 4:
                //si datosCapturados es 0, no te dejara acceder a esta opcion
                if(datosCapturados)
                {
                    promedio = obtenerPromedio(calificaciones, n);
                    printf("Promedio: %.2f\n", promedio);
                }
                else
                {
                    printf("Primero capture las calificaciones.\n");
                }
            break;

            case 5:
                //si datosCapturados es 0, no te dejara acceder a esta opcion
                if(datosCapturados)
                {
                    mostrarHistograma(calificaciones, n);
                }
                else
                {
                    printf("Primero capture las calificaciones.\n");
                }
            break;

            case 6:
                printf("Saliendo...\n");
            break;
        }

    }
    while(opcion != 6);

    //Cuando acaba el programa se libera la memoria
    if(calificaciones != NULL)
    {
        free(calificaciones);
    }

    return 0;
}
//===================================================================//
```


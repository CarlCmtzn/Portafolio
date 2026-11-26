---
layout: default
title: Recursion y Combinatoria
parent: Tareas
grand_parent: Lógica Matemática y Matemáticas Discretas
nav_order: 8
---

# Recursion y Combinatoria

```python
# =========================================================
# FACTORIAL
# =========================================================

def factorial(n):
    # El factorial solo está definido para enteros no negativos
    if n < 0:
        raise ValueError("El factorial no está definido para negativos")

    # Caso base
    if n == 0 or n == 1:
        return 1

    # Llamada recursiva
    return n * factorial(n - 1)


# =========================================================
# PERMUTACIONES
# =========================================================

def dfs_permutaciones(lista):
    resultado = []
    dfs_perm([], lista, resultado)
    return resultado


def dfs_perm(actual, restantes, resultado):
    # Si no quedan elementos, la permutación está completa
    if len(restantes) == 0:
        resultado.append(actual)
        return

    # Intentar colocar cada elemento en la siguiente posición
    for i in range(len(restantes)):
        siguiente = restantes[i]

        # Lista sin el elemento seleccionado
        nuevo_resto = restantes[:i] + restantes[i + 1:]

        # Continuar construyendo la permutación
        dfs_perm(actual + [siguiente], nuevo_resto, resultado)


# =========================================================
# COMBINACIONES
# =========================================================

def dfs_combinaciones(lista, r):
    resultado = []
    dfs_comb([], 0, lista, r, resultado)
    return resultado


def dfs_comb(actual, inicio, lista, r, resultado):
    # Si ya elegimos r elementos, guardamos la combinación
    if len(actual) == r:
        resultado.append(actual)
        return

    # Solo avanzar, nunca regresar a elementos anteriores
    for i in range(inicio, len(lista)):
        dfs_comb(actual + [lista[i]], i + 1, lista, r, resultado)
```

# Prueba 1
```python
# =========================================================
# PRUEBAS 1
# =========================================================

print("Factorial de 5:")
print(factorial(5))


print("\nPermutaciones de [1, 2, 3]:")

permutaciones = dfs_permutaciones([1, 2, 3])

for permutacion in permutaciones:
    print(permutacion)


print("\nCombinaciones de [1, 2, 3] tomando 2:")

combinaciones = dfs_combinaciones([1, 2, 3], 2)

for combinacion in combinaciones:
    print(combinacion)
```

![Gráfica de concentración]({{ '/assets/img/Logica/prueba1.png' | relative_url }})

# Prueba 2
```python
# =========================================================
# PRUEBA 2
# =========================================================

print("Factorial de 9:")
print(factorial(9))


print("\nPermutaciones de [1, 2, 3, 4]:")

permutaciones = dfs_permutaciones([1, 2, 3, 4])

for permutacion in permutaciones:
    print(permutacion)


print("\nCombinaciones de [4, 6, 8, 10] tomando 3:")

combinaciones = dfs_combinaciones([4, 6, 8, 10], 3)

for combinacion in combinaciones:
    print(combinacion)
```



![Gráfica de concentración]({{ '/assets/img/Logica/prueba2.png' | relative_url }})


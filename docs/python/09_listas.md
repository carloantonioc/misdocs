# Listas en Python

Las listas son una estructura de datos en Python que permiten almacenar una colección de elementos ordenados y mutables. Las listas se definen utilizando corchetes `[]` y los elementos se separan por comas.

```python
frutas = ["manzana", "naranja", "kiwi"]
print(frutas)  # ['manzana', 'naranja', 'kiwi']
```

## Acceso a los elementos

Podemos acceder a los elementos de una lista utilizando índices, donde el primer elemento tiene un índice de 0.

```python
print(frutas[0])  # manzana
print(frutas[1])  # naranja
print(frutas[2])  # kiwi
```

## Tipos de datos

Las listas también pueden contener elementos de diferentes tipos de datos, como números, cadenas de texto, booleanos, etc.

```python
mi_lista = [1, "hola", True, 3.14]
print(mi_lista)  # [1, 'hola', True, 3.14]
```

## Modificación de elementos

Podemos modificar los elementos de una lista asignando un nuevo valor a un índice específico.

```python
frutas[1] = "pera"
print(frutas)  # ['manzana', 'pera', 'kiwi']
```

## Métodos comunes

Las listas también tienen varios métodos incorporados que nos permiten realizar operaciones comunes, como agregar elementos, eliminar elementos, ordenar la lista, etc.

```python
frutas.append("plátano")  # Agrega un elemento al final de la lista
print(frutas)  # ['manzana', 'pera', 'kiwi', 'plátano']

frutas.remove("pera")  # Elimina un elemento de la lista
print(frutas)  # ['manzana', 'kiwi', 'plátano']

frutas.sort()  # Ordena la lista alfabéticamente
print(frutas)  # ['kiwi', 'manzana', 'plátano']
```

## Longitud de la lista

También podemos usar la función `len()` para obtener la longitud de una lista, es decir, el número de elementos que contiene.

```python
print(len(frutas))  # 3
```

## Listas anidadas

Las listas también pueden contener otras listas, lo que se conoce como listas anidadas.

```python
matriz = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
print(matriz)      # [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
print(matriz[0])   # [1, 2, 3]
print(matriz[0][1])# 2
```

> **En resumen:** Las listas son una estructura de datos muy versátil en Python que nos permiten almacenar y manipular colecciones de elementos de manera eficiente.

## Operador `in`

Podemos usar el operador `in` para verificar si un elemento está presente en una lista.

```python
if "manzana" in frutas:
    print("La manzana está en la lista de frutas.")
```

## Operador `del`

Podemos usar el operador `del` para eliminar un elemento de una lista por su índice.

```python
del frutas[0]  # Elimina el primer elemento de la lista
print(frutas)  # ['kiwi', 'plátano']
```

## Referencia de Métodos

A continuación se describen los métodos más utilizados para listas:

- **`append()`**: Agrega un elemento al final de la lista.
- **`remove()`**: Elimina la primera aparición de un elemento específico de la lista.
- **`sort()`**: Ordena los elementos de la lista en orden alfabético o numérico.
- **`reverse()`**: Invierte el orden de los elementos en la lista.
- **`index()`**: Devuelve el índice de la primera aparición de un elemento específico en la lista.
- **`count()`**: Devuelve el número de veces que un elemento específico aparece en la lista.
- **`extend()`**: Agrega los elementos de otra lista al final de la lista actual.
- **`clear()`**: Elimina todos los elementos de la lista, dejándola vacía.
- **`pop()`**: Elimina y devuelve el último elemento de la lista o el elemento en un índice específico.

## Ejemplo Práctico

Ejemplo de uso de algunos métodos de listas:

```python
numeros = [3, 1, 4, 1, 5]

numeros.append(9)  # Agrega el número 9 al final de la lista
print(numeros)  # [3, 1, 4, 1, 5, 9]

numeros.remove(1)  # Elimina la primera aparición del número 1
print(numeros)  # [3, 4, 1, 5, 9]

numeros.sort()  # Ordena la lista de números
print(numeros)  # [1, 3, 4, 5, 9]

numeros.reverse()  # Invierte el orden de la lista
print(numeros)  # [9, 5, 4, 3, 1]

print(numeros.index(4))  # Devuelve el índice del número 4 (2)
print(numeros.count(1))  # Devuelve el número de veces que el número 1 aparece (1)

otra_lista = [2, 6]
numeros.extend(otra_lista)  # Agrega los elementos de otra_lista al final de numeros
print(numeros)  # [9, 5, 4, 3, 1, 2, 6]

numeros.clear()  # Elimina todos los elementos de la lista dejándola vacía
print(numeros)  # []
```
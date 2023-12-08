## Aritmética de punteros:

![[Algoritmos y Programación II/Punteros/Untitled.png|Untitled]]

![[Algoritmos y Programación II/Punteros/Untitled 1.png|Untitled]]

## **Múltiple Indirecciones:**

![[Algoritmos y Programación II/Punteros/Untitled 2.png|Untitled]]

![[Algoritmos y Programación II/Punteros/Untitled 3.png|Untitled]]

## Puntero comodín: void*

Es un puntero genérico que puede apuntar a cualquier cosa.

Este puntero no puede ser desreferenciado, no se le pueden aplicar las reglas de aritmética de punteros y puede ser convertido a cualquier tipo de dato sin una conversión explícita.

```c
int main(){
	int a = 10;
	char b = 'x';

	void* p = &a;  //El puntero a void guarda la dirección del entero 'a'
	p = &b;        //El puntero a void guarda la dirección del caracter 'b'
	
	return 0;
}
```

## Puntero a función:

### Declarar punteros a función:

Si tenemos la función

```c
char obtener_letra (int numero, bool chequeo);
```

Un puntero a esta función sería

```c
char(*puntero_obtener_letra)(int, bool);
puntero_obtener_letra = obtener_letra;         //asignación
```

O también

```c
char (*puntero_obtener_letra)(int, bool) = obtener_letra;   //inicialización
```

### Recibir puntero a función por parámetro:

Lo haremos de esta maner:

```c
void mostrar_letra (int repeticiones, char (*puntero_obtener_letras)(int, bool));
```

### Invocar una función si tengo el puntero de la misma:

```c
char mi_letra = puntero_a_letra(180, true);
```
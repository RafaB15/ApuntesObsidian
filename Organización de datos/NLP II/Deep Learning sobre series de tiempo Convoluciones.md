# Convoluciones:

![[Organización de datos/NLP II/Deep Learning sobre series de tiempo Convoluciones/Untitled.png|Untitled]]

# Convolución discreta

![[Organización de datos/NLP II/Deep Learning sobre series de tiempo Convoluciones/Untitled 1.png|Untitled]]

# Convoluciones en 1D

![[Organización de datos/NLP II/Deep Learning sobre series de tiempo Convoluciones/Untitled 2.png|Untitled]]

![[Organización de datos/NLP II/Deep Learning sobre series de tiempo Convoluciones/Untitled 3.png|Untitled]]

# Hiperparámetros

## Kernel Size

![[Organización de datos/NLP II/Deep Learning sobre series de tiempo Convoluciones/Untitled 4.png|Untitled]]

![[Organización de datos/NLP II/Deep Learning sobre series de tiempo Convoluciones/Untitled 5.png|Untitled]]

![[Organización de datos/NLP II/Deep Learning sobre series de tiempo Convoluciones/Untitled 6.png|Untitled]]

## Stride

![[Organización de datos/NLP II/Deep Learning sobre series de tiempo Convoluciones/Untitled 7.png|Untitled]]

![[Organización de datos/NLP II/Deep Learning sobre series de tiempo Convoluciones/Untitled 8.png|Untitled]]

![[Organización de datos/NLP II/Deep Learning sobre series de tiempo Convoluciones/Untitled 9.png|Untitled]]

# Stride de 1 y Kernel de 2

![[Organización de datos/NLP II/Deep Learning sobre series de tiempo Convoluciones/Untitled 10.png|Untitled]]

## Dilatación de 1 y Kernel size 2

![[Organización de datos/NLP II/Deep Learning sobre series de tiempo Convoluciones/Untitled 11.png|Untitled]]

## ¿Qué hacer con al salida?

Podemos volverla a convulsionar

![[Organización de datos/NLP II/Deep Learning sobre series de tiempo Convoluciones/Untitled 12.png|Untitled]]

Hacer pooling

![[Organización de datos/NLP II/Deep Learning sobre series de tiempo Convoluciones/Untitled 13.png|Untitled]]

![[Organización de datos/NLP II/Deep Learning sobre series de tiempo Convoluciones/Untitled 14.png|Untitled]]

![[Organización de datos/NLP II/Deep Learning sobre series de tiempo Convoluciones/Untitled 15.png|Untitled]]

# Conclusiones:

- Las convoluciones no usan recurrencia para avanzar por sobre la serie de tiempo.
- Las convoluciones son más rápidas que las RNNs.
- Podemos regular el kernel size para elegir cuantos instantes de tiempo ve la convolución.
- Usar stride nos permite acortar el largo de la salida.
- Usar dilatación nos permite ver los instantes de tiempo de forma intercalada.
- El pooling resume la secuencia de salida de las CNNs.
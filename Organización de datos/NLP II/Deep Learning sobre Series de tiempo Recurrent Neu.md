# Deep Learning:

![[Organización de datos/NLP II/Deep Learning sobre Series de tiempo Recurrent Neu/Untitled.png|Untitled]]

![[Organización de datos/NLP II/Deep Learning sobre Series de tiempo Recurrent Neu/Untitled 1.png|Untitled]]

$$
n_1 = h(\sum_{i=1}^6 w_i^{n_1} * f_i)
$$

$$
O=\sum_{i=1}^5 n_i *w_1^{O}
$$

$$
\vec{\theta} = (w_1^{n_1},w_2^{n_1},...,w_6^{n_5},w_1^{O},...)
$$

Función de costo

$$
J(\vec{\theta}) = \frac{1}{N}\sum^N_{i=1}(y-\hat y)^2
$$

![[Organización de datos/NLP II/Deep Learning sobre Series de tiempo Recurrent Neu/Untitled 2.png|Untitled]]

![[Organización de datos/NLP II/Deep Learning sobre Series de tiempo Recurrent Neu/Untitled 3.png|Untitled]]

![[Organización de datos/NLP II/Deep Learning sobre Series de tiempo Recurrent Neu/Untitled 4.png|Untitled]]

![[Organización de datos/NLP II/Deep Learning sobre Series de tiempo Recurrent Neu/Untitled 5.png|Untitled]]

![[Organización de datos/NLP II/Deep Learning sobre Series de tiempo Recurrent Neu/Untitled 6.png|Untitled]]

![[Organización de datos/NLP II/Deep Learning sobre Series de tiempo Recurrent Neu/Untitled 7.png|Untitled]]

![[Organización de datos/NLP II/Deep Learning sobre Series de tiempo Recurrent Neu/Untitled 8.png|Untitled]]

En lugar de crear nosotros los features para el pasado queremos que la red neuronallos descubra, ¿Cómo podemos hacer eso?

# Recurrent Neural Networks

![[Organización de datos/NLP II/Deep Learning sobre Series de tiempo Recurrent Neu/Untitled 9.png|Untitled]]

![[Organización de datos/NLP II/Deep Learning sobre Series de tiempo Recurrent Neu/Untitled 10.png|Untitled]]

![[Organización de datos/NLP II/Deep Learning sobre Series de tiempo Recurrent Neu/Untitled 11.png|Untitled]]

## RNNs y gradientes

![[Organización de datos/NLP II/Deep Learning sobre Series de tiempo Recurrent Neu/Untitled 12.png|Untitled]]

![[Organización de datos/NLP II/Deep Learning sobre Series de tiempo Recurrent Neu/Untitled 13.png|Untitled]]

## Long short-term memory

![[Organización de datos/NLP II/Deep Learning sobre Series de tiempo Recurrent Neu/Untitled 14.png|Untitled]]

## Gru

![[Organización de datos/NLP II/Deep Learning sobre Series de tiempo Recurrent Neu/Untitled 15.png|Untitled]]

## Múltiples RNNs

![[Organización de datos/NLP II/Deep Learning sobre Series de tiempo Recurrent Neu/Untitled 16.png|Untitled]]

## Stacked RNN:

![[Organización de datos/NLP II/Deep Learning sobre Series de tiempo Recurrent Neu/Untitled 17.png|Untitled]]

## Configuraciones de RNNs

![[Organización de datos/NLP II/Deep Learning sobre Series de tiempo Recurrent Neu/Untitled 18.png|Untitled]]

# Conclusiones:

- Las RNNs sirven para inferir features de forma automática sobre series de tiempo.
- Las RNNs clásicas tienen problemas para retener secuencias largas y problemas con sus gradientes (exploding y vanishing gradients).
- Las LSTMs es una versión más rápida de la LSTM.
- Podemos formar distintas arquitecturas con distintas configuraciones de RNNs.
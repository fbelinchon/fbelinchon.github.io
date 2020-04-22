# Modelo simple

## Objetivo.
El objetivo del artículo es entender como se define un modelo de apredizaje. Nos centraremos 
en la definición de modelos de redes neuronales sencillas para entender los mecanismos básicos.
Las redes neuronales se denominan **deep learning** porque se basan en arquitecturas de varios niveles que se
conectan de forma encadenada hasta producir el resultado final.

## Configuración básica


El modelo más básico de red neuronal es el perceptrón. Está definido por una neurona que acepta una entrada con varios parámetros y produce una salida. Idealmente la salida es 0 o 1. Para calcular el resultado final se multiplica cada entrada por un peso que nos indica el aporte de esa entrada al resultado final.

 Al sumatorio de todas esas operaciones se le compara con un valor constante para devolver un 1 si el sumatorio es mayor que ese valor o un 0  en caso contrario. Si nos damos cuenta tenemos los mismo elementos que describimos en el árticulo anterior.
- Una entrada de datos.
- Una matriz (en este caso un vector) de pesos.
- Un parámetro de ajuste para indicar el umbral del cero que denominamos bias y que se añade a la multiplicación de ,los valores anteriores.
- El resultado de nuestro modelo. En este caso concreto sería 0 o 1.

Este modelo lo podemos representar matemáticamente como:

$\hat{y}=W*x + b$

![mnist](/images/Perceptron.svg)
> Imagen perceptrón con cinco entradas tomada de Wikipedia

Para ajustar la salida de un perceptrón que sería de 0 o 1 podemos indicar que el valor será un 1 si el resultado es positivo y cero en caso contrario.

El perceptrón es un modelo muy simple donde solamente tenemos una neurona y una sola capa. Como veremos más adelante las redes neuronales constan de cientos de neuronas en cada capa y de varias capas que se encadenan unas a otras. Es decir, la salida de una capa es la entrada a la siguiente.

### Multiplicación de matrices

El ejemplo del perceptron se define matemáticamente como una multiplicación de vectores. Al multiplicar el vector entrada $\vec{x}$ por el vector $\vec{w}$ de los pesos tenemos las operaciones de multiplicación que hemos definido.

$$
\left[\begin{array}{ccc}x_1& x_2 & x_3\end{array}\right] \left[\begin{array}{ccc}w_1 \\ w_2 \\ w_3\end{array}\right] = x_1*w_1+x_2*w_2+x_3*w_3
$$

Si queremos añadir más neuronas a nuestro modelo necesitamos tratar con multiplicaciones de matrices. Imaginemos que se añade una nueva neurona. Tendrá el mismo número de entradas pero tendremos dos resultados de nuestro modelo, uno por cada neurona. Cada nueva columna de nuestra matriz de pesos representa una neurona con sus correspondietnes pesos que se aplican a cada entrada. Si lo expresamos como operaciones de matrices trandríamos lo siguiente.


$$
\left[\begin{array}{ccc}x_1& x_2 & x_3\end{array}\right] \left[\begin{array}{ccc}w_{1n1}&w_{1n2} \\ w_{2n1} & w_{2n2}\\ w_{3n1} & w_{3n2}\end{array}\right] = \begin{cases} x_1*w_{1n1}+x_{2}*w_{2n1}+x_3*w_{3n1} \\ x_1*w_{1n2}+x_{2}*w_{2n2}+x_3*w_{3n2}\end{cases}
$$

Hemos numerado los índices de los pesos de forma que el primer elemento es el orden del peso y el segundo la neurona. Por ejemplo $w_{3n2}$ sería el peso que se aplica a la tercera entrada perteneciente a la segunda neurona. Normalmente en matrices se habla de filas y columnas (en ese orden). A partir de ahora utilizaremos esa nomenclatura donde el primer valor (fila) es el orden del peso y el segundo (columna) es la neurona, $w_{32}$ (es el tercer parámetro de la segunda neurona)

Es importante tener claro unos conceptos básicos de multiplicación de matrices.
- Para multiplicar dos matrices necesitamos que el número de columnas de la primera matriz sea igual al número de filas de la segunda matriz. Tiene sentido porque el número de parámetros de entrada tiene que ser igual al número de pesos que tiene cada neurona.
- La matriz resultado tendrá el mismo número de filas que la primera matriz y el mismo número de columnas de la segunda. También concuerda con lo que hemos explicado. Si tenemos como entrada un vector $\vec{x} = \left[\begin{array}{ccc}x_1& x_2 & x_3\end{array}\right]$ (1 fila y 3 columnas) y nuestro modelo tiene dos neuronas (3 filas y 2 columnas) el resultado tendría una fila y dos columnas, una columnas para el resultado de cada neurona. Simplificando, el resultado de nuestro modelo sería igual al número de registros de entrada (en nuestro ejemplo uno) y tantas columnas como neuronas tenemos $X(1,3) * W(3,2) = R(1,2)$
  
Para aclarar un poco más el tema podemos poner un ejemplo donde como entrada tenemos dos registros y nuestro modelo tiene 3 neuronas. X(2,3) * W(3,3) = R(2,3)

$$
\left[\begin{array}{ccc}x_{11}& x_{12} & x_{13} \\ x_{21}& x_{22} & x_{23}\end{array}\right] * \left[\begin{array}{ccc}w_{11}&w_{12} & w_{13} \\ w_{21} & w_{22} & w_{23}\\ w_{31} & w_{32}& w_{33}\end{array}\right] = \left[\begin{array}{ccc} r_{11}  & r_{12} & r_{13}\\ r_{21}  & r_{22} & r_{23}\end{array}\right]
$$

$$ 
r_{11} = x_{11}*w_{11} + x_{12}*w_{21} + x_{13}*w_{31}
$$

$$
r_{12} = x_{11}*w_{12} + x_{12}*w_{22} + x_{13}*w_{32}
$$

$$
r_{13} = x_{11}*w_{13} + x_{12}*w_{23} + x_{13}*w_{33}
$$

$$
r_{21} = x_{21}*w_{11} + x_{22}*w_{22} + x_{23}*w_{31}
$$

$$
r_{22} = x_{21}*w_{12} + x_{22}*w_{22} + x_{23}*w_{32}
$$

$$
r_{23} = x_{21}*w_{13} + x_{22}*w_{23} + x_{23}*w_{33}
$$


La primera fila del resultado es el valor de cada una de las tres neuronas para el primer registro de entrada. La segunda fila corresponde a los valores de cada neurona para el segundo registro.

Conocer las dimensiones de la salida de nuestro modelo es esencial para poder incorporar más niveles a nuestro modelo.

# README P1 Robótica Móvil

## 1. Introducción

El objetivo de esta prática es diseñar un algoritmo para una aspiradora de baja gama. Se pide que recorra una estancia sin acceder al mapa, solo con la información del bumper y/o del laser.

## 2. Notas

Inicialmente importamos todas las librerías que se van a necesitar. Después declaramos las funciones que vamos a necesitar. La función forward sirve para que avance hacia delante, y para asegurar que no queda ninguna velocidad angular restante de un estado anterior se pone específicamente a 0. La segunda función que tenemos es backward, que sirve para que el robot vaya hacia detras, y ponemos la velocidad angular a 0 por el mismo motivo que en la función forward.

Después tenemos las funciones turn_right y turn_left que sirven para que el robot gire a la derecha o a la izquierda. Especificamos también que la velocidad linear sea 0, en caso de que quede restante de un estado anterior.

A continuación tenemos control_cycle que es la máquina de estados. Declaramos state_, turn_ltime, turn_rtime como globales. Después se recoge información del bumper. El primer estado que tenemos es FORWARD, con el que vamos a empezar. En este estado haremos que se ejecute forward mientras no detecte choque, en caso de que detecte un choque se cambiará de estado a BACKWARD.

En el estado Backward tenemos 3 posibilidades. En caso de que el choque sea frontal se ejecuta la función backward hasta que se deje de detectar el choque, cuando se deja de detectar girará a la izquierda. En caso de que el choque sea en el lado izquierdo girará hacia la derecha. En caso de que el choque se haya detectado un choque a la derecha girará a la izquierda duramte un determinado tiempo.

Después tenemos un bucle infinito while True que ejecutará continuamente la máquina de estados.

## 3. Dificultades

El problema más difícil que se ha encontrado son los ángulos. Inicialmente la idea era que cuando se chocara girara 90 grados aproximadamente, pero debido a la inexactitud pues no ha sido posible. Primero el robot no paraba de girar, a veces interrumpía para volver a avanzar pero no le era posible. Se implementaron trazas y se observó que los angulos de un momento a otro saltaban de 2 a 14 grados y era imposible saber con exactitud hasta cuando debía girar. Para solucionar esto se implementó un tiempo determinado de giro.

El segundo problema que se ha tenido ha sido con variables gobales y locales, que ha habido pequeñas confusiones debido a que el error aparecía en otros sitios que no era el propio programa. Se solucionó declarando state_ turn_ltime y turn_rtime en control_cycle como globales y dándoles un valor inicial 0 al principio.

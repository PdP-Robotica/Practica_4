# Practica_4

## Integrantes:
- Luis Fernando Duarte Reséndiz.
  
-  Mauricio Alberto Gómez Arroyo.

- Diego Brandon Guzmán Sierra.

- Bryan Hiadim Vera Hernández.

## Introducción 

El uso de brazos robóticos ha convertido en un componente esencial para la optimización de la eficiencia y la productividad dentro de diferentes entornos industriales. Su capacidad de asumir tareas repetitivas y de alta precisión, ha permitido su integración dentro de diversas áreas. Dentro de la presente práctica se demostrará la capacidad del robot Epson para la realizar una secuencia de movimientos programados con el software Epson RC+ 7.0, permitiendo apilar una serie de 4 fusibles de manera precisa. Requiriendo un nivel elevado de exactitud para garantizar la estabilidad de la de la pila y evitar su colapso.

## Instrucciones

### 1.- Inciar la conexión

Se debe establecer conexión por medio de USB con el equipo que se utilizará para progrmar el brazo, de igual manera, dentro del software es importante determinar el tipo de conexión como se muestra a continuación

![image](https://github.com/user-attachments/assets/03a31c7e-03fe-4469-a717-ff48916fb041)

### 2.- Grabar las posiciones 

Una vez establecida la conexión con el equipo, se debe inicializar los motores del brazo para comenzar con su movimiento.

![Captura de pantalla 2024-09-25 213637](https://github.com/user-attachments/assets/a223a487-b385-4466-9a5f-3bc34b535f0e)

Posteriormente debemos de seleccionar un dispensador de fusibles, de aquí es de donde tomaremos los fusibles para apilarlos. Una vez seleccionado se puede comenzar con el grabado de posiciones. Dentro de la pestaña "Jog & Teach" seleccionamos el tipo de movimiento "World", el cual permite un movimiento cartesiano dentro de 3 ejes (x,y,z).

![Captura de pantalla 2024-09-25 220042](https://github.com/user-attachments/assets/5d5ef3c8-8a82-4715-b81f-cc08363b3b78)

Ahora bien, colocamos el brazo sobre el dispensador de fusibles seleccionado como se muestra en la imagen.

<img src="https://github.com/user-attachments/assets/65d19469-e183-4299-a14f-e24e5ea6bbbb" alt="agarrar" height="200" style="display: block; margin: auto;">

Obteniendo las siguientes coordenadas:
![Captura de pantalla 2024-09-25 221602](https://github.com/user-attachments/assets/26d7fdbf-bec4-469d-972c-daca8415874c)

Dentro de la pestaña "Teach Points" se almacena esa posición con el nombre "Arriba", esto para poder programar la secuencia de movimeintos más adelante.
![Captura de pantalla 2024-09-25 222036](https://github.com/user-attachments/assets/57783c5c-e592-47f9-a529-233e6a242c0b)

Posteriormente, se bajó el brazo para que quedara exactamente en la posición del fusible como se muestra a continuación:

<img src="https://github.com/user-attachments/assets/82d72990-4a4a-43cf-af28-cc2760f01e46" alt="agarrado" height="200" style="display: block; margin: auto;">

Para ello, solo se realizaron modificaciones en el eje z estando en la posición "Arriba", donde se obtuvieron las siguientes coordenadas:
![Captura de pantalla 2024-09-25 223401](https://github.com/user-attachments/assets/d9216ddd-53fa-4a5b-83b6-994eae3a0ee1)

A dicha posición se le denominó "Agarrar"
![Captura de pantalla 2024-09-25 223537](https://github.com/user-attachments/assets/ad0d1077-9d46-4027-b19f-bb1eb02d640b)

Finalemente, la última posición necesaria es el lugar donde se apilarán los fusibles. Siendo en las siguientes coordenadas:
![Captura de pantalla 2024-09-25 223816](https://github.com/user-attachments/assets/d97dcabb-4f2a-4b7d-9579-8fdbe9847331)

A esta posición se le nombró "Soltar"
![Captura de pantalla 2024-09-25 223858](https://github.com/user-attachments/assets/06c50482-27f6-400a-8cd8-dce1688098d0)

### 3.- Generar código

Una vez grabadas las posiciones a utilizar se procede con la programación del código en el archivo "Main.prg". Donde se generó el siguiente código

```spel
Function main
On 2
Home
Integer i
Integer f
f = 10.5
For i = 0 To 3
	Go Arriba
	Move Agarrar
	Off 2
	Move Arriba
	Home
	Go Soltar +Z(i * f)
	On 2
	Home
	
Next

Fend
```
Los comando más importantes utilizados en el programa son: 
<table style="width: 100%; border-collapse: collapse;">
  <thead>
    <tr>
      <th style="border: 1px solid #ddd; padding: 8px; text-align: left; background-color: #f2f2f2;">Comando</th>
      <th style="border: 1px solid #ddd; padding: 8px; text-align: left; background-color: #f2f2f2;">Descripción</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="border: 1px solid #ddd; padding: 8px;">'On'</td>
      <td style="border: 1px solid #ddd; padding: 8px;">Permite abrir la pinza</td>
    </tr>
    <tr>
      <td style="border: 1px solid #ddd; padding: 8px;">'Off'</td>
      <td style="border: 1px solid #ddd; padding: 8px;">Permite cerrar la pinza</td>
    </tr>
    <tr>
      <td style="border: 1px solid #ddd; padding: 8px;">'Integer'</td>
      <td style="border: 1px solid #ddd; padding: 8px;">Permite declarar una variable como entero</td>
    </tr>
    <td style="border: 1px solid #ddd; padding: 8px;">'Go'</td>
      <td style="border: 1px solid #ddd; padding: 8px;">Permite ir a una posición con una trayectoria curva</td>
    </tr>
  </tr>
    <td style="border: 1px solid #ddd; padding: 8px;">'Move'</td>
      <td style="border: 1px solid #ddd; padding: 8px;">Permite ir a una posición con una trayectoria recta</td>
    </tr>
  </tbody>
</table>

Ahora bien, el código realiza los siguiente pasos:

1.- Abrir la pinza: Incia con la apertura de la pinza para evitar colisiones al momento de tomar el fusible

2.- Ir a la posición Home: Esto asegura que el movimiento inicia en la posición Home (Posición establecida en prácticas anteriores)

3.- Declarar variable: Declara dos variables que van a permitir la generación de un ciclo for

4.- Generar ciclo for: Es necesario el uso de un ciclo for, como se va a tomar el fusible de la misma posición las 4 veces, es necesario repetir las acciones. Este ciclo inicia con la variable "i" en 0 y termina cuando esta obtiene un valor de 3, resultando en las 4 iteraciones necesarias para apilar 4 fusibles.

Dentro del ciclo for se ejecuta lo siguiente:

1.- Ir a la posición "Arriba": Posiciona el brazo encima del dispensador de fusibles

2.- Ir a la posición "Agarrar": Baja el brazo para poder tomar el fusible con la pinza. **Nota: Se utiliza el comando Move para realizar una trayectoria completamente recta y evitar colisiones al momento de sujetar el fusible**

3.- Cierra la pinza

4.- Vuelve a la posición "Arriba": Posiciona de nuevo el brazo en la parte superior, para poder extraer el fusible del dispensador

5.- Ir a la posición "Home": Posiciona el brazo en "Home" para evitar colisiones al momento de soltar el fusible

6.- Ir a la posición "Soltar": Manda el brazo a la posición donde se soltarán los fusibles. Dentro de esta posición es necesario ajustar el eje Z. Dado que los fusibles se apilarán, se debe tener en cuenta la altura del fusible anterior para determinar la posición del siguiente. Para esto, utilizamos la variable 'f', que se declaró anteriormente con un valor de 10.5 mm (1.05 cm), aproximadamente el ancho de un fusible. Este valor se multiplica por 'i', que indica cuántos fusibles ya se han colocado. De esta manera, se pueden apilar los cuatro fusibles, considerando la variación en sus alturas.

7.- Regresar a la posición "Home": Una vez soltado el fusible regresa a la posición "Home" para repetir el proceso.

## Ejecución

Una vez terminado el código, se compila y carga al brazo para su ejecución.


# Práctica 4

## Integrantes:
- Luis Fernando Duarte Reséndiz.
  
-  Mauricio Alberto Gómez Arroyo.

- Diego Brandon Guzmán Sierra.

- Bryan Hiadim Vera Hernández.

## Introducción.

El uso de brazos robóticos se ha convertido en un componente esencial para la optimización de la eficiencia y la productividad dentro de diferentes entornos industriales. Su capacidad de asumir tareas repetitivas y de alta precisión, ha permitido su integración dentro de diversas áreas. Dentro de la presente práctica se demostrará la capacidad del robot Epson para la realizar una secuencia de movimientos programados con el software Epson RC+ 7.0, permitiendo apilar una serie de 4 fusibles de manera precisa. Requiriendo un nivel elevado de exactitud para garantizar la estabilidad de la de la pila y evitar su colapso.

## Instrucciones.

### 1.- Inciar la conexión.

Se debe establecer conexión por medio de USB con el equipo que se utilizará para programar el brazo, de igual manera, dentro del software es importante determinar el tipo de conexión como se muestra a continuación:

![image](https://github.com/user-attachments/assets/03a31c7e-03fe-4469-a717-ff48916fb041)

### 2.- Grabar las posiciones.

Una vez establecida la conexión con el equipo, se debe inicializar los motores del brazo para comenzar con su movimiento.

![Captura de pantalla 2024-09-25 213637](https://github.com/user-attachments/assets/a223a487-b385-4466-9a5f-3bc34b535f0e)

Posteriormente, se debe de seleccionar un dispensador de fusibles (de aquí es de donde se tomarán los fusibles para apilarlos). Una vez seleccionado se puede comenzar con el grabado de posiciones. Dentro de la pestaña "Jog & Teach" se configura el tipo de movimiento como "World", el cual permite un movimiento cartesiano dentro de 3 ejes (x,y,z).

![Captura de pantalla 2024-09-25 220042](https://github.com/user-attachments/assets/5d5ef3c8-8a82-4715-b81f-cc08363b3b78)

Ahora bien, colocamos el brazo sobre el dispensador de fusibles seleccionado como se muestra en la imagen:

<img src="https://github.com/user-attachments/assets/65d19469-e183-4299-a14f-e24e5ea6bbbb" alt="agarrar" height="250">

Obteniendo las siguientes coordenadas:

![Captura de pantalla 2024-09-25 221602](https://github.com/user-attachments/assets/26d7fdbf-bec4-469d-972c-daca8415874c)

Dentro de la pestaña "Teach Points" se almacena esa posición con el nombre "Arriba", esto para poder programar la secuencia de movimeintos más adelante.

![Captura de pantalla 2024-09-25 222036](https://github.com/user-attachments/assets/57783c5c-e592-47f9-a529-233e6a242c0b)

Posteriormente, se bajó el brazo para que quedara exactamente en la posición del fusible como se muestra a continuación:

<img src="https://github.com/user-attachments/assets/82d72990-4a4a-43cf-af28-cc2760f01e46" alt="agarrado" height="250">

Para ello, solo se realizaron modificaciones en el eje z estando en la posición "Arriba", donde se obtuvieron las siguientes coordenadas:

![Captura de pantalla 2024-09-25 223401](https://github.com/user-attachments/assets/d9216ddd-53fa-4a5b-83b6-994eae3a0ee1)

A dicha posición se le denominó "Agarrar".

![Captura de pantalla 2024-09-25 223537](https://github.com/user-attachments/assets/ad0d1077-9d46-4027-b19f-bb1eb02d640b)

Finalemente, la última posición necesaria es el lugar donde se apilarán los fusibles. Siendo en las siguientes coordenadas:

![Captura de pantalla 2024-09-25 223816](https://github.com/user-attachments/assets/d97dcabb-4f2a-4b7d-9579-8fdbe9847331)

A esta posición se le nombró "Soltar".

![Captura de pantalla 2024-09-25 223858](https://github.com/user-attachments/assets/06c50482-27f6-400a-8cd8-dce1688098d0)

### 3.- Generar código.

Una vez grabadas las posiciones a utilizar se procede con la programación del código en el archivo "Main.prg". Donde se generó el siguiente código:

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

1.- Abrir la pinza: Incia con la apertura de la pinza para evitar colisiones al momento de tomar el fusible.

2.- Ir a la posición Home: Esto asegura que el movimiento inicia en la posición Home (Posición establecida en prácticas anteriores).

3.- Declarar variables: Declara dos variables que van a permitir la generación de un ciclo for y el aumento de la altura.

4.- Generar ciclo for: Es necesario el uso de un ciclo for puesto que se va a tomar el fusible de la misma posición las 4 veces, es necesario repetir las acciones. Este ciclo inicia con la variable "i" en 0 y termina cuando esta obtiene un valor de 3, resultando en las 4 iteraciones necesarias para apilar 4 fusibles.

Dentro del ciclo for se ejecuta lo siguiente:

1.- Ir a la posición "Arriba": Posiciona el brazo encima del dispensador de fusibles

2.- Ir a la posición "Agarrar": Baja el brazo para poder tomar el fusible con la pinza. 

**Nota: Se utiliza el comando Move para realizar una trayectoria completamente recta y evitar colisiones al momento de sujetar el fusible.**

3.- Cierra la pinza.

4.- Vuelve a la posición "Arriba": Posiciona de nuevo el brazo en la parte superior, para poder extraer el fusible del dispensador.

5.- Ir a la posición "Home": Posiciona el brazo en "Home" para evitar colisiones al momento de soltar el fusible.

6.- Ir a la posición "Soltar": Manda el brazo a la posición donde se soltarán los fusibles. Dentro de esta posición es necesario ajustar el eje Z. Dado que los fusibles se apilarán, se debe tener en cuenta la altura del fusible anterior para determinar la posición del siguiente. Para esto, utilizamos la variable 'f', que se declaró anteriormente con un valor de 10.5 mm (1.05 cm), aproximadamente el ancho de un fusible. Este valor se multiplica por 'i', que indica cuántos fusibles ya se han colocado. De esta manera, se pueden apilar los cuatro fusibles, considerando la variación en sus alturas.

7.- Regresar a la posición "Home": Una vez soltado el fusible regresa a la posición "Home" para repetir el proceso.

## Ejecución

Una vez terminado el código, se compila y carga al brazo para su ejecución obteniendo el siguiente resultado:

https://github.com/user-attachments/assets/129f6279-a942-4b1e-9d03-f1bfc3109abd

## Conclusiones
- Luis Fernando Duarte Reséndiz.

La automatización mediante brazos robóticos no solo mejora la eficiencia, sino que también permite la adaptación de procesos a las características específicas de los objetos manipulados. En el caso del dispensador de fusibles, ajustar la posición en función de la altura de los fusibles demuestra cómo la robótica puede ser integrada de manera flexible en diversas aplicaciones industriales, facilitando un futuro más innovador en la manufactura.

- Mauricio Alberto Gómez Arroyo.

La implementación de brazos robóticos en procesos de apilación, como se vio en esta práctica, demuestra cómo la automatización puede mejorar significativamente la precisión y la eficiencia en entornos industriales. La capacidad de programar movimientos exactos reduce el riesgo de errores y optimiza el tiempo de producción, lo que resulta en una operación más segura y efectiva.

- Diego Brandon Guzmán Sierra.

La correcta calibración de las posiciones en la automatización es fundamental para asegurar que los procesos se realicen de manera efectiva. La atención a detalles como la altura de los objetos a apilar no solo garantiza un funcionamiento adecuado, sino que también previene problemas potenciales, como la inestabilidad de la carga. Esto resalta la necesidad de una planificación cuidadosa en la programación de sistemas robóticos.
  
- Bryan Hiadim Vera Hernández.

La utilización de variables en la programación de brazos robóticos demuestra cómo la personalización de procesos puede optimizar el rendimiento. Ajustar los parámetros para adaptarse a las características específicas de los objetos a manipular permite mejorar la eficiencia y la precisión. Este enfoque refuerza la idea de que la automatización debe ser flexible y adaptable para enfrentar los desafíos de diferentes entornos industriales.

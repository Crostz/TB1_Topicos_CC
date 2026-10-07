
# Descripción del proyecto

Sistema que resuelve un puzzle Futoshiki a partir de una fotografía.
Se aplica OpenCV y YOLO para leer el tablero, OR-Tools CP-SAT para resolverlo y la solución se dibuja sobre la foto original.

Enlace herramienta desplegada: https://fushiki.vercel.app/

## ¿Qué es Futoshiki?

Un Futoshiki es un juego de lógica que consiste en una cuadrícula de N×N donde hay que colocar los números del 1 al N sin repetirlos en ninguna fila ni columna, respetando los signos de desigualdad (`<`, `>`) dibujados entre celdas contiguas y los dígitos que ya vienen impresos.

## Fases del proyecto
* Visión: Detecta la grilla, corrige la perspectiva, lee los dígitos con YOLO y los signos (regla geométrica) y genera un JSON con el estado inicial. Para este modulo se utiliza OpenCV y Ultralytics YOLO.
* Razonamiento: Modela el puzzle como un problema de restricciones, lo resuelve y comprueba si la solución es única. Las herramientas aplicadas son OR-Tools y CP-SAT 
* Visualización: Escribe la solución sobre la foto original y la muestra en una página web. Para esto se utiliza las herramientas OpenCV y Gradio.

## Fuente de datos
Dataset propio de 68 imágenes capturadas con cámara de puzzles Futoshiki, de las 68 imágenes se hicieron 4839 recortes (71 recortes por imagen aproximadamente) distribuidos de la siguiente manera:
* Vacíos 3265 recortes (Celdas sin dígito y huecos sin signo, es decir, con tinta < 0.02)
* Dígitos	792	recortes (Celdas con contenido)
* Signos 782 recortes (< 165, > 221, ^ 203, v 193)

Utilizamos el modelo de `yolo11n-cls.pt`, preentrenado con ImageNet, y le hacemos fine-tuning con los dígitos nuevos.

# Ejemplo para utilizar la herramienta

## 1. Capturar problema con cámara
A continuación está un ejemplo del input que espera el programa.

![Foto1](/Read_me_img/Ejercicio.jpg)

## 2. Solucinar el problema con la herramienta
1. Se ingresa al enlace del desplegable
2. Se sube la imagen del problema a la herramienta
3. Automáticamente se resuelve el problema indentificado.

![Foto2](/Read_me_img/ProgramaSolver.png)

# Limitaciones
* La detección necesita que se vea la grilla completa y que el número de celdas sea un cuadrado perfecto de al menos 9.
* El modelo solo reconoce los dígitos con los que fue entrenado.
* Los signos se leen con una regla geométrica, sin aprendizaje automático.
* La comprobación de unicidad no tiene límite de tiempo explícito, por lo que en tableros grandes podría tardar.
* `share=True` publica la aplicación con un enlace temporal por lo que no se deben subir fotos con información sensible.

## Autores 
* Nicole Yessenia Vasquez Tinco - U202322884
* Alessandro Daniel Bravo Castillo - U202224501
* Alessandro Elías Hesse Pulache - U202318347


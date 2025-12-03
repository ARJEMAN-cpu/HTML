# **Llamémosla una superficie de dibuja(s)**  
El elemento canvas de HTML5 se define como un "lienzo de mapa de bits dependiente de la resolución que puede utilizarse para renderizar gráficos, gráficos de juegos u otras imágenes visuales sobre la marcha". Es un área rectangular en la página donde se puede dibujar utilizando JavaScript  
Inicialmente, un elemento canvas no tiene contenido ni borde propio, por lo que no se ve nada. La sintaxis básica incluye la definición de ancho y alto, y opcionalmente un id para acceder a él en el DOM (Document Object Model). Se pueden tener múltiples elementos canvas en una misma página, y cada uno mantiene su propio estado  
# **Contexto de Dibujo y Coordenadas**  
Todo canvas comienza en blanco. Para empezar a dibujar, es necesario obtener el contexto de dibujo. Esto se hace llamando al método getContext() sobre el elemento canvas, al cual se le debe pasar obligatoriamente la cadena "2d". El contexto de dibujo es donde se definen todos los métodos y propiedades de dibujo  
El canvas utiliza una cuadrícula bidimensional donde la coordenada (0, 0) se encuentra en la esquina superior izquierda del canvas. Los valores del eje X aumentan hacia la derecha y los valores del eje Y aumentan hacia la parte inferior  
Una técnica importante para el dibujo preciso es el desplazamiento de coordenadas: para dibujar una línea de un solo píxel de ancho, es necesario desplazar las coordenadas en 0.5 perpendicularmente a la dirección de la línea  
Si se desea borrar el contenido de un canvas y restablecer las propiedades de su contexto de dibujo a sus valores predeterminados, se puede simplemente reestablecer su propiedad width o height a su valor actual  
# **Dibujo de Formas y Rutas**  
El contexto de dibujo proporciona propiedades y métodos específicos para dibujar:  
• Rectángulos: Los métodos incluyen fillRect(x, y, width, height) para dibujar un rectángulo relleno y strokeRect(x, y, width, height) para dibujar solo los bordes (el trazo).  
• Limpieza: clearRect(x, y, width, height) borra los píxeles en el área rectangular especificada.  
• Estilos: Las propiedades fillStyle y strokeStyle controlan el estilo del relleno y del trazo, respectivamente. Estos pueden ser un color CSS, un patrón o un gradiente.  
**El proceso de dibujo se explica a menudo con la metáfora del "lápiz" y la "tinta":**  
1. "Lápiz" (Definición de Ruta): Al igual que un boceto, las rutas no son visibles hasta que se trazan. Los métodos de "lápiz" para líneas rectas incluyen moveTo(x, y) (mueve el lápiz al punto de partida) y lineTo(x, y) (dibuja una línea al punto final). Para dibujar un círculo (que es un arco completo), se utiliza el método arc(). Para comenzar una nueva ruta, se utiliza context.beginPath()  
2. "Tinta" (Dibujo Final): Para hacer permanente lo dibujado, se usan métodos de "tinta" como stroke() (traza el camino con el strokeStyle actual) o fill() (rellena la forma).  
Se puede dibujar texto en un canvas utilizando el método fillText(). A diferencia del texto en el resto de la página web, el texto en el canvas no tiene box model, lo que significa que las técnicas de diseño CSS como floats, márgenes y padding no están disponibles.  
**Los atributos disponibles en el contexto de dibujo para el texto incluyen:**  
• font: Puede ser cualquier regla de fuente CSS (estilo, variante, peso, tamaño, etc.).  
• textAlign: Controla la alineación horizontal (start, end, left, right, center).  
• textBaseline: Controla dónde se dibuja el texto en relación con el punto de partida (valores posibles incluyen top, middle, alphabetic, bottom).  
# **Gradientes**  
Un gradiente es una transición suave de dos o más colores. El contexto soporta dos tipos:  
1. createLinearGradient(x0, y0, x1, y1): Pinta a lo largo de una línea.  
2. createRadialGradient(x0, y0, r0, x1, y1, r1): Pinta a lo largo de un cono entre dos círculos definidos.  
Para definir los colores, se usa el método addColorStop() en el objeto gradiente, especificando una posición entre 0 y 1. Para usar el gradiente, se asigna el objeto gradiente a la propiedad fillStyle antes de dibujar una forma.  
# **Imágenes**  
El método drawImage() permite dibujar una imagen en un canvas. Este método acepta tres, cinco o nueve argumentos para especificar la imagen fuente, y las coordenadas y dimensiones de destino (incluyendo escalado y recorte).  
La imagen puede ser un elemento img existente o un objeto Image() creado con JavaScript. Es fundamental asegurarse de que la imagen esté completamente cargada antes de intentar dibujarla en el canvas, a menudo esperando el evento window.onload o Image.onload.  
# **Interacción y Compatibilidad**  
Para que el canvas responda a la interacción del usuario, se pueden añadir event listeners, como un listener para el evento click. La función de manejo de eventos recibe un objeto MouseEvent  
**El proceso para determinar dónde hizo clic el usuario implica varios pasos:**  
1. Obtener las coordenadas x e y relativas al documento.  
2. Convertir estas coordenadas a coordenadas relativas al canvas (ajustando por gCanvasElement.offsetLeft y gCanvasElement.offsetTop).  
3. Usar estas coordenadas relativas al canvas para la lógica específica de la aplicación.
Soporte de Navegadores (Internet Explorer)  
Internet Explorer 9 (IE9) es la primera versión que soporta nativamente la API de canvas. Las versiones anteriores de Internet Explorer (IE7 y IE8) requieren el uso de la biblioteca de terceros ExplorerCanvas (excanvas.js).  
ExplorerCanvas es una biblioteca JavaScript que implementa la API de canvas en IE usando la tecnología propietaria VML de Microsoft. Se incluye en la sección head de la página usando comentarios condicionales <!--[if lt IE 9]>) para que solo IE lo descargue y ejecute, mejorando la velocidad de carga en otros navegadores.  
**Sin embargo, ExplorerCanvas tiene varias limitaciones:**  
• Solo soporta gradientes lineales; los gradientes radiales no son compatibles.  
• Es notablemente más lento que la implementación nativa.  
• Puede ocurrir una condición de carrera si se intenta usar la interfaz faux-canvas inmediatamente. La solución más sencilla es diferir toda la manipulación del canvas hasta después de que se dispare el evento onload.  
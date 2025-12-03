# **DETECCION DE CARACTERISTICAS HTML5**  
El texto proporcionado explica en detalle cómo la detección de características de HTML5 es crucial, ya que HTML5 es una colección de características individuales (como canvas, video, geolocalización, etc.), y no una única entidad. Por lo tanto, en lugar de detectar el soporte de "HTML5" en general, se debe detectar el soporte para funciones específicas.  
# **Técnicas de Detección de Características de HTML5**   
El proceso se basa en examinar el Modelo de Objeto de Documento (DOM) para ver qué propiedades y métodos están presentes en el navegador.  

# 1. **Comprobar Propiedad en Objeto Global (Técnica #1)**  
Esta es la técnica más sencilla. Consiste en verificar la existencia de una propiedad concreta dentro de un objeto global del DOM (como window o navigator).  
# 2. **Crear Elemento y Comprobar Propiedad/Método (Técnica #2)**  
Esta técnica implica crear un elemento DOM ficticio en memoria y luego examinarlo para ver si tiene una propiedad o método específico que solo existe si la característica es compatible.  
# 3. **Crear Elemento, Llamar a Método y Comprobar Valor Devuelto (Técnica #3)**  
Esta técnica se utiliza cuando el soporte no es binario (sí/no), sino que requiere una verificación más detallada, como en los formatos de vídeo.  
# 4. **Crear Elemento, Establecer y Comprobar el Valor de Propiedad (Técnica #4)**  
Esta técnica se utiliza para detectar soporte para nuevos tipos de input. Se establece el atributo type a un nuevo valor de HTML5 y se comprueba si el navegador lo mantuvo (lo soporta) o si volvió al valor predeterminado "text" (no lo soporta).  
# **Modernizr: La Biblioteca de Detección**  
Modernizr es una biblioteca de JavaScript de código abierto (licencia MIT) que automatiza la detección de características de HTML5 y CSS3.  
Funcionamiento: Se incluye el script en el head de la página. Al ejecutarse, crea un objeto global llamado Modernizr con propiedades booleanas para cada característica que detecta (p. ej., Modernizr.canvas será true o false).  
if (Modernizr.canvas) {  

  // Usar la API Canvas nativa  

} else {  

  // Usar una solución alternativa (polyfill)  

}  
Detección Específica (Ej. Tipos de Entrada): Para tipos de entrada, crea un sub-objeto llamado Modernizr.inputtypes, donde cada tipo se comprueba individualmente (p. ej., Modernizr.inputtypes.date).
# **Almacenamiento local**  
El almacenamiento en HTML5 permite que los sitios web almacenen información en tu ordenador y la recuperen más tarde. El concepto es similar al de las cookies, pero está diseñado para mayores cantidades de información. Las cookies son limitadas en tamaño, y tu navegador las envía de vuelta al servidor web cada vez que solicita una nueva página (lo que requiere tiempo extra y un valioso ancho de banda). El almacenamiento en HTML5 permanece en tu ordenador, y los sitios web pueden acceder a él con JavaScript una vez cargada la página.  
# **Web Workers**  
Los Web Workers proporcionan una forma estándar para que los navegadores ejecuten JavaScript en segundo plano. Con los web workers, puedes generar varios "hilos" que se ejecutan todos al mismo tiempo, más o menos. (Piensa en cómo tu ordenador puede ejecutar varias aplicaciones a la vez y ya estás casi en el camino.) Estos "hilos en segundo plano" pueden realizar cálculos matemáticos complejos, hacer peticiones de red o acceder a almacenamiento local mientras la página web principal responde al usuario que se desplaza, hace clic o escribe.  
# **Aplicaciones web offline**  
Las aplicaciones web offline comienzan como aplicaciones web online, el servidor web le indica a tu navegador qué archivos necesita para funcionar offline. Estos archivos pueden ser cualquier cosa — HTML, JavaScript, imágenes, incluso vídeosUna vez que tu navegador descarga todos los archivos necesarios, puedes volver a visitar la web aunque no estés conectado a Internet. Tu navegador notará que estás desconectado y usará los archivos que ya ha descargado. Cuando vuelvas a conectarte, cualquier cambio que hayas hecho podrá subirse al servidor web remoto.  

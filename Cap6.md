# **Concepto y Métodos de Geolocalización**  
La geolocalización se define como el arte de determinar dónde se encuentra usted en el mundo y, opcionalmente, compartir esa información con personas de confianza. Existen múltiples métodos para determinar la ubicación física, incluyendo el uso de la dirección IP, la conexión de red inalámbrica, la torre celular a la que está conectado el teléfono, o el hardware GPS dedicado que calcula la latitud y longitud a partir de satélites.  
El sistema de coordenadas geográficas utilizado por los atributos del API de geolocalización es el World Geodetic System (2d) [WGS84], un sistema centrado en la Tierra.  
# **El API de Geolocalización y Privacidad**  
El API de geolocalización permite a los sitios web de confianza obtener la latitud y longitud del usuario a través de JavaScript, lo que les permite realizar funciones conscientes de la ubicación, como mostrar la ubicación en un mapa o encontrar negocios locales.  
La privacidad es una preocupación obvia. El API establece explícitamente que los agentes de usuario no deben enviar información de ubicación a sitios web sin el permiso expreso del usuario. Compartir la ubicación es siempre un proceso opt-in.  
Cuando un sitio web llama a la función para obtener la ubicación, el navegador (como Mozilla Firefox) presenta una barra de información (infobar). Este cuadro de diálogo informa al usuario qué sitio web solicita la ubicación y le permite:  
1. Elegir compartir la ubicación.  
2. Elegir no compartir la ubicación.  
3. Pedirle al navegador que recuerde la elección para ese sitio web.  
Esta barra de información es incondicional (el sitio web no puede evitarla) y bloqueante, lo que significa que el sitio web no puede determinar la ubicación mientras espera la respuesta del usuario.  
# **Uso del API: Obtención de Posición**  
El API se centra en una nueva propiedad del objeto global navigator: navigator.geolocation. La forma más simple de obtener la ubicación es utilizando la función getCurrentPosition():  
**navigator.geolocation.getCurrentPosition(show_map);**  
1. Función de Devolución de Llamada (Callback) Exitosa La función getCurrentPosition() regresa inmediatamente, pero la información de ubicación solo estará disponible cuando se llame a la función callback de éxito. Esta función se llama con un único parámetro, un objeto que contiene las propiedades coords y timestamp.  
• El objeto coords contiene la latitud y la longitud de la ubicación física.  
• Las únicas propiedades de posición garantizadas son coords.latitude, coords.longitude y coords.accuracy. Otras propiedades como altitude, heading (dirección) y speed pueden ser null.  
2. Opciones de Posición (PositionOptions) La función getCurrentPosition() tiene un tercer argumento opcional, el objeto PositionOptions, que permite configurar  
3. Precisión de la Ubicación En dispositivos móviles populares (como iPhone y Android), se admiten dos métodos de ubicación:  
• Triangulación de torres celulares: Es rápida y no requiere GPS dedicado, pero solo proporciona una idea aproximada (desde una cuadra hasta un kilómetro).  
• Hardware GPS dedicado: Puede determinar la ubicación con una precisión de pocos metros, pero el chip GPS consume mucha energía y hay un retraso inicial mientras se conecta a los satélites.  

Es posible que la llamada a getCurrentPosition() falle si se establece enableHighAccuracy:true, pero tenga éxito si se usa enableHighAccuracy:false.  

4. Monitoreo Continuo (watchPosition) Si se necesita la ubicación de forma continua, se utiliza watchPosition(). Esta función tiene la misma estructura que getCurrentPosition() pero llama a la función callback cada vez que cambia la ubicación del usuario. El dispositivo determina el intervalo óptimo de sondeo. La función watchPosition() devuelve un número que se utiliza con el método clearWatch() para detener el seguimiento de la ubicación.  
# **Manejo de Errores**  
Si ocurre un problema, se llama a la función callback de manejo de errores, que es el segundo argumento de getCurrentPosition():  
navigator.geolocation.getCurrentPosition( show_map, handle_error)  
# **Compatibilidad y Librerías de Envoltura (Wrapper)**  
Aunque el API de Geopositioning es compatible con la mayoría de los navegadores modernos (incluyendo IE 9.0+, Firefox 3.5+, Chrome 5.0+, etc.), los navegadores más antiguos (como Internet Explorer anterior a la versión 9) pueden requerir plugins o librerías.  
Gears es un plugin de código abierto de Google que proporciona características para navegadores antiguos, incluido un API de geolocalización que es similar pero diferente al API W3C. Además, plataformas móviles antiguas como BlackBerry, Nokia, Palm y OMTP BONDI tenían sus propios API de geolocalización específicos.  
La librería geo.js (código abierto con licencia MIT) se utiliza para suavizar las diferencias entre el API de geolocalización W3C, el API Gears y las API de las plataformas móviles. Para usar geo.js, se deben incluir los scripts gears_init.js (para inicializar Gears) y geo.js. Se requiere una llamada explícita a geo_position_js.init() para verificar la disponibilidad del API. Actualmente, geo.js no admite la función watchPosition().  
Analogía: Pensar en la geolocalización como solicitar a un conserje que te diga dónde estás. El conserje (el navegador/dispositivo) primero debe preguntarte (el usuario) si quieres que comparta tu ubicación (el proceso opt-in y el infobar). Si dices que sí, el conserje tiene diferentes métodos para encontrarte: puede buscar el punto de acceso WiFi más cercano (baja precisión) o sacar un dispositivo GPS satelital (alta precisión). Una vez que te encuentra, te da la ubicación (el callback exitoso). Si dices que no, o si el conserje no puede contactar a nadie (problemas de red), se activa el proceso de manejo de errores.
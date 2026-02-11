# **El Problema Histórico del Almacenamiento Local**  
Históricamente, las aplicaciones nativas han tenido una ventaja sobre las aplicaciones web en cuanto al almacenamiento local persistente, ya que el sistema operativo proporciona capas de abstracción para datos específicos de la aplicación, como preferencias o estado.  
Las aplicaciones web se limitaron inicialmente a las cookies, inventadas al principio de la historia de la web, pero estas presentan tres inconvenientes importantes:  
1. Ralentización: Se incluyen con cada solicitud HTTP, transmitiendo innecesariamente los mismos datos una y otra vez.  
2. Seguridad: Envían datos sin cifrar por internet con cada solicitud (a menos que toda la aplicación use SSL).  
3. Límite de datos: Están limitadas a unos 4 KB, lo que es suficiente para ralentizar la aplicación, pero no lo suficiente para ser útil.  
Lo que realmente se buscaba era una gran cantidad de espacio de almacenamiento en el cliente, que persistiera más allá de la actualización de una página y que no se transmitiera al servidor.  
# **Breve Historia de los "Hacks" Antes de HTML5**  
**Antes de que HTML5 estandarizara una solución, existieron varios intentos de almacenamiento local, todos considerados insatisfactorios:**  
• userData (Internet Explorer): Permitió a las páginas web almacenar hasta 64 KB de datos por dominio en una estructura jerárquica basada en XML. No presentaba diálogo de permisos al usuario.  
• Objetos Locales Compartidos (LSOs) / "Flash cookies" (Adobe Flash): A partir de Flash 6, permitían almacenar hasta 100 KB de datos por dominio "gratuitamente". Más allá de eso, solicitaba permiso al usuario por cada orden de magnitud de aumento (1 Mb, 10 Mb, etc.). El puente Flash-a-JavaScript llamado AMASS fue integrado más tarde en Dojo Toolkit como dojox.storage.  
• Google Gears (Plugin, 2007): Proporcionó una API a una base de datos SQL incrustada basada en SQLite, permitiendo almacenar cantidades ilimitadas de datos por dominio tras obtener el permiso inicial del usuario.  
Un patrón común en todas estas soluciones previas era que dependían de un solo navegador o de un plugin de terceros, exponiendo interfaces y limitaciones radicalmente diferentes.  
# **Introducción al Almacenamiento HTML5 (Web Storage)**  
HTML5 Storage (oficialmente llamado Web Storage, también conocido como Local Storage o DOM Storage) se propuso resolver el problema proporcionando una API estandarizada, implementada de forma nativa y consistente en múltiples navegadores, sin depender de plugins de terceros  
**Características clave:**  
• Mecanismo: Es una forma de almacenar pares clave/valor con nombre localmente en el navegador del cliente.  
• Persistencia: Al igual que las cookies, los datos persisten después de que el usuario navega o cierra el navegador.  
• No Transmisión al Servidor: A diferencia de las cookies, estos datos nunca se transmiten al servidor web remoto (a menos que se envíen manualmente).  
• Soporte: Es compatible con la última versión de prácticamente todos los navegadores principales, incluyendo Internet Explorer 8.0+, Firefox 3.5+, Safari 4.0+, Chrome 4.0+, y Opera 10.5+.  
• API: Se accede a través del objeto localStorage en el objeto global window. El soporte se puede detectar con funciones como supports_html5_storage() o utilizando Modernizr.  
**Uso y Limitaciones**  
La interfaz Storage define métodos como getItem(key) y setItem(key, data), así como removeItem(key) y clear(). El objeto localStorage también puede tratarse como un array asociativo usando la sintaxis de corchetes, por ejemplo, localStorage["bar"].  
Nota importante sobre los tipos de datos: Aunque se pueden almacenar Booleans, enteros o floats de JavaScript, los datos se almacenan y se recuperan siempre como strings. Si se está almacenando algo que no es una cadena, es necesario utilizar funciones como parseInt() o parseFloat() para coaccionar los datos recuperados al tipo de datos esperado.  
Seguimiento de cambios: El evento storage se dispara en el objeto window cuando setItem(), removeItem() o clear() se llama y realmente cambia algo en el área de almacenamiento. El evento storage no es cancelable; es solo una notificación de que ha ocurrido un cambio.  
**Limitaciones de almacenamiento:**  
• El espacio de almacenamiento predeterminado por origen es de 5 megabytes (MB), lo cual es consistentemente adoptado por los navegadores.  
• Si se excede esta cuota, se lanzará la excepción QUOTA_EXCEEDED_ERR  
• Actualmente (a febrero de 2011), no existe un mecanismo para que los desarrolladores web soliciten más espacio de almacenamiento al usuario.  
# **Visiones Competidoras para el Almacenamiento Avanzado**  
Si bien HTML5 Storage proporciona una solución estandarizada de clave/valor, existen visiones alternativas para el almacenamiento local avanzado que van más allá de los 5 MB de pares clave/valor con nombre.   
**1. Web SQL Database**  
Esta especificación surgió de la influencia de Google Gears. Proporciona una capa delgada sobre una base de datos SQL (basada en SQLite) incrustada, permitiendo ejecutar sentencias SQL como SELECT, UPDATE, INSERT y DELETE desde JavaScript.  
Aunque cuatro navegadores y plataformas implementaron esta especificación (Safari 4.0+, Chrome 4.0+, Opera 10.5+, iPhone 3.0+, Android 2.0+), el esfuerzo de estandarización ha llegado a un punto muerto. El problema es que se requiere la implementación independiente de la especificación, pero todos los implementadores interesados utilizaron el mismo backend SQL (SQLite).  
**2. Indexed Database API (IndexedDB)**  
Conocida anteriormente como "WebSimpleDB," IndexedDB expone una tienda de objetos (object store). Comparte conceptos con las bases de datos SQL (bases de datos, registros, campos, transacciones), pero su principal diferencia es que no tiene un lenguaje de consulta estructurado (SQL). En su lugar, se utilizan métodos de la tienda de objetos para abrir cursores y enumerar o filtrar registros.  
Al momento de la redacción del texto (febrero de 2011), IndexedDB solo se había implementado en una versión beta de Firefox 4. Mozilla ha declarado que nunca implementará Web SQL Database, mientras que Google y Microsoft han expresado interés en IndexedDB.  

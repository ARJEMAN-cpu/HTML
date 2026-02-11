# **HTML5 Video: Codecs, Encoding, and Markup**   
# El Vídeo Antes y Después de HTML5  
Antes de HTML5, incrustar vídeo en una página web no se realizaba de manera estandarizada, sino que dependía de plugins de terceros, como QuickTime, RealPlayer o Flash (utilizado por YouTube)  
HTML5 define una forma estándar de incrustar vídeo utilizando el elemento video. Aunque el soporte para este elemento aún está evolucionando y no es universal, el elemento no tiene restricciones sobre qué códec de vídeo, códec de audio o formato contenedor se puede usar  
# **Componentes Fundamentales del Vídeo**  
Un archivo de vídeo generalmente se compone de múltiples pistas (una de vídeo y una o más de audio) que están interrelacionadas para sincronizar el sonido con el vídeo. La reproducción de un vídeo implica al menos tres acciones simultáneas: interpretar el formato contenedor, decodificar la transmisión de vídeo y decodificar la transmisión de audio.  
1. Contenedores de Vídeo *(Video Containers): Son formatos que definen cómo se almacenan las cosas dentro de un archivo, pero no qué tipos de datos se almacenan (similar a un archivo ZIP)  
◦ MPEG 4 (extensiones .mp4 o .m4v), basado en el contenedor QuickTime de Apple.  
◦ Flash Video (extensión .flv), usado por Adobe Flash.  
◦ Ogg (extensión .ogv), que es un estándar abierto, compatible con código abierto y libre de patentes conocidas.  
◦ WebM, un nuevo formato técnicamente similar a Matroska, diseñado para usarse exclusivamente con los códecs VP8 (vídeo) y Vorbis (audio).  
2. Códecs de Vídeo (Video Codecs): Son algoritmos por los cuales se codifica y decodifica una transmisión de vídeo. Los códecs pueden ser con pérdida (lossy), que pierden información durante la codificación para lograr altas tasas de compresión y archivos más pequeños, o sin pérdida (lossless), que son demasiado grandes para ser útiles en la web. Los tres códecs más relevantes son:  
◦ H.264 (también conocido como MPEG-4 AVC): Estándar desde 2003, busca ser compatible con una amplia gama de dispositivos (desde teléfonos móviles hasta computadoras de escritorio) mediante el uso de "perfiles" (como Baseline, Main y High). Este estándar está sujeto a patentes y su licencia es negociada a través del grupo MPEG LA.  
◦ Theora: Evolucionó del códec VP3 y es un códec libre de regalías y no está sujeto a patentes conocidas. Se usa a menudo en un contenedor Ogg.  
◦ VP8: Otro códec que produce una salida a la par con el perfil High de H.264, pero con una baja complejidad de decodificación a la par con H.264 Baseline. Google lo adquirió, publicó la especificación como código abierto y licenció sus patentes libre de regalías, por lo que VP8 es un códec moderno y libre de regalías.  
3. Códecs de Audio (Audio Codecs): Son algoritmos para codificar y decodificar una transmisión de audio. Los códecs de audio generalistas más importantes para la web son:  
◦ MP3 (MPEG-1 Audio Layer 3): Puede contener hasta 2 canales de sonido y está sujeto a patentes.  
 ◦ AAC (Advanced Audio Coding): Estandarizado en 1997, fue elegido por Apple para la iTunes Store. Puede codificar hasta 48 canales de sonido y utiliza "perfiles". El formato AAC está sujeto a patentes.  
 ◦ Vorbis (a menudo llamado Ogg Vorbis): No está sujeto a patentes conocidas. Soporta un número arbitrario de canales de sonido y se incrusta comúnmente en contenedores Ogg o WebM.  
 # **Compatibilidad y Flujo de Trabajo**  
 No existe una combinación única de contenedores y códecs que funcione en todos los navegadores HTML5. Para lograr la máxima compatibilidad, es necesario codificar el vídeo más de una vez:  
 1. Una versión que utilice WebM (VP8 + Vorbis).  
 2. Una versión que utilice H.264 Baseline (vídeo) y AAC low complexity (audio) en un contenedor MP4.  
 3. Una versión que utilice Theora (vídeo) y Vorbis (audio) en un contenedor Ogg.  
 Estos archivos múltiples se vinculan mediante el elemento video que contiene varios elementos source. El navegador intentará reproducir el primer archivo de vídeo que pueda manejar.  
 # **El Marcado HTML**  
 El elemento video debe incluir atributos como width y height. El atributo controls activa los controles de reproducción integrados del navegador.  
Para ofrecer múltiples formatos, se utiliza el elemento source anidado dentro de video. El atributo type en source es crucial, ya que permite al navegador verificar si puede reproducir el archivo antes de descargarlo, ahorrando ancho de banda.  
# **Fallback y Servidor**  
Para navegadores que no son compatibles con HTML5 (como IE 8), se puede anidar un elemento object dentro del elemento video para invocar un plugin Flash y asegurar la reproducción. Los navegadores que sí soportan video ignorarán el contenido anidado.  
Además, es fundamental que los archivos de vídeo se sirvan con el tipo MIME adecuado (ej. video/mp4 para .mp4, video/webm para .webm) a través del encabezado HTTP del servidor web. Una configuración incorrecta puede impedir que los vídeos se reproduzcan.  
# **Herramientas de Codificación**  
Existen varias herramientas de código abierto para codificar los diferentes formatos:  
• Miro Video Converter: Programa que produce salidas WebM, Theora y H.264/MP4 (etiquetado como "iPhone") sin opciones avanzadas.  
• Firefogg y ffmpeg2theora: Se utilizan para la codificación de vídeo Ogg (Theora + Vorbis).  
• HandBrake: Aplicación para codificar vídeo H.264. Se recomienda la codificación de dos pasadas para obtener una mejor calidad sin aumentar el tamaño del archivo.  
• ffmpeg: Se puede usar para codificar WebM (VP8 + Vorbis).  
El proceso de codificación en H.264 requiere especial atención a los costos de licencia asociados, ya que este códec está sujeto a patentes gestionadas por MPEG LA.  
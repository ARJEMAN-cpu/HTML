# *EL MANIFIESTO DE CACHE* 
  
# 1. EL CONCEPTO FUNDAMENTAL: 
# Una aplicación web offline no es una contradicción; es un proceso de dos pasos:  
# *CONECTADO*  
# El navegador descarga una lista de recursos especificados en un archivo especial.
# *DESCONECTADO* 
# El navegador sirve esos archivos desde una caché local en lugar de buscarlos en la red.  
# *2. EL ARCHIVO DE MANIFIESTO* 
# Es el corazón del sistema. Es un archivo de texto simple que debe servirse con el tipo de contenido text/cache-manifest. Se vincula en el HTML así: html manifest="archivo.manifest".  
# *EL ARCHIVO SE DIVIDE EN TRES SECCIONES PRINCIPALES* 
# *CACHE (EXPLÍCITA):*  
# Archivos que se descargarán y guardarán localmente (CSS, JS, imágenes).  
# *NETWORK (LISTA BLNCA)*  
# Recursos que siempre requieren conexción(como scripts de seguimiento o APls ) y nunca deben cacharse  
# *FALLBACK*  
# Define "planes B". Si un recurso no está disponible offline, el navegador muestra un sustituto (por ejemplo, una página de error genérica offline.html).  
# *3. EL FLUJO DE EVENTOS*  
# El navegador sigue un proceso estricto para gestionar la caché a través del objeto window.applicationCache:  
# 1. Checking: Comprueba si hay un manifiesto.  
# 2. Downloading/Progress: Si es nuevo o ha cambiado, descarga los archivos.  
# 3. Cached/UpdateReady: Avisa cuando la descarga termina. Si es una actualización, se necesita llamar a swapCache() o recargar para ver los cambios.  
# 4. Error: Si falla la descarga de un solo archivo, todo el proceso de caché falla.  

# *4. PROBLEMAS COMÚNES Y DEPURACIÓN*  
# El autor destaca que este sistema puede ser frustrante debido a la "doble caché":   
# Caché HTTP: Los servidores suelen decir a los navegadores que guarden archivos por horas. Si el archivo .manifest está cacheado por HTTP, el navegador ni siquiera buscará actualizaciones. Solución: Configurar el servidor para que el manifiesto expire inmediatamente.  

# Actualización de archivos: Si cambias un CSS pero no modificas el archivo .manifest, el navegador pensará que nada ha cambiado. Solución: Usar comentarios con números de versión (ej: # rev 43) dentro del manifiesto para forzar la actualización.  
#  


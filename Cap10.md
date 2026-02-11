# *¿QUÉ ES EL MICRODATOS?*  
# Es una forma de anotar el DOM (la estructura de la página) con pares de nombre/valor. Su objetivo es permitir que los desarrolladores definan vocabularios personalizados para describir objetos que el HTML estándar no cubre, como una Persona, un Evento o una Organización.  
# 1. *LOS ATRIBUTOS FUNDAMENTALES*:  
# Para aplicar microdatos se utilizan principalmente tres atributos:  
# .*ITEMSCOPE*: Delimita el alcance. Indica que todo lo contenido en ese elemento pertenece a un mismo objeto.  
# .*ITEMTTYPE*: Define el tipo de objeto mediante una URL que sirve como diccionario (ej. http://data-vocabulary.org/Person).  
# .*ITEMPROP*: Asigna una propiedad específica a un dato (ej. name, photo, url).  
# *EXTRACCIÓN DE DATOS*  
# *El valor de una propiedad depende del elemento HTML utilizado. HTML5 sigue estas reglas automáticas:*  
# URLs: En elementos a o link, el valor se toma del atributo href. En img, se toma del src.  
# *TIEMPO*: En elementos time, se extrae del atributo datetime.  
# *TEXTO PLANO*:En la mayoría de los demás elementos (span, h1, p), el valor es simplemente el texto que contienen.  
# 4.*ANIDACIÓN DE VOCABULARIOS*  
# El microdatos permite jerarquías. Puedes tener un objeto Persona que contenga dentro un objeto Dirección (Address). Esto se hace abriendo un nuevo itemscope e itemtype dentro de un elemento que ya tenía un itemprop.  
# *Ejemplo: Una persona tiene una propiedad address, y esa dirección a su vez tiene propiedades como street-address, locality y postal-code.*  
# 5.*LA UTILIDAD REAL: GOOGLE RICH SNIPPETS*:  
# *MEJORES RESULTADOS*: Si usas microdatos, Google puede mostrar información enriquecida en sus resultados (fotos, cargos, direcciones) en lugar de solo texto plano.  
# VISIBILIDAD: Estos "Rich Snippets" hacen que los resultados sean más atractivos y útiles para el usuario, aunque Google no garantiza su aparición en todos los casos.  
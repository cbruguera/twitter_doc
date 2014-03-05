===========================================================
Aplicación de "Canales Twitter": Análisis de requerimientos
===========================================================

Características actuales
------------------------

La aplicación actualmente cuenta con los siguientes módulos funcionales:


Usuarios
~~~~~~~~

* Acceso mediante usuario y contraseña
* Posibilidad de varios usuarios (creados mediante el admin), con su espacio separado de canales y configuraciones
* Posibilidad de registrar un número indefinido de "canales", que corresponden a cuentas autenticadas de twitter


Retweet automático
~~~~~~~~~~~~~~~~~~

* Inspección constante del *timeline* de cada canal, con posibilidad de retweet automático según ciertos criterios de filtrado
* Listado y manejo de **disparadores** (*triggers*): palabras o frases que indican que el tweet es candidato a re-envío
* Listado y manejo de **supresores**: palabras o frases para sustitución
* Listado y manejo de **retenedores**: palabras o frases que descartarán automáticamente el mensaje
* Listado y manejo de **horarios de publicación**: horarios en los que se permitirá el funcionamiento del módulo, con distinción para DMs y Mentions
* Listado y manejo de **usuarios bloqueados**: usuarios cuyos mensajes serán automáticamente descartados
* Botón para activar o desactivar la funcionalidad de retweet automático (detiene e inicia el streaming)
* Controles para activar o desactivar cada uno de los tipos de filtro (retenedores, supresores, disparadores, horarios, usuarios bloqueados)


Tweets programados
~~~~~~~~~~~~~~~~~~

* Listado y manejo de **bloques de publicación automática**
    - Un bloque consta de un texto, una hora del día y una serie de días de la semana para su publicación
    - El mensaje será enviado cada uno de los días seleccionados a la hora específica
    - El usuario puede "enviar inmediatamente" cualquiera de los bloques mediante un botón
* Botón para activar y desactivar la funcionalidad de tweets programados


Hashtags
~~~~~~~~

* Listado y manejo de **hashtags programables**
    - Cada hashtag cuenta con: un texto, una cantidad, un rango horario y una serie de días de la semana
    - Durante los días y horarios especificados, se incluirá el texto en forma de #hashtag en los tweets enviados que cuenten con espacio suficiente
    - la cantidad de hashtags será restada hasta alcanzar 0 (cero)


Notificaciones
~~~~~~~~~~~~~~

* Se envían notificaciones al usuario en caso de eventos
    - El único evento definido actualmente es la ocurrencia de *update limit* en algún canal


Otras características no-interactivas
-------------------------------------

* Prevención de update limit
    - Los canales hacen retweet automático con una separación mínima de un minuto, para evitar la publicación en ráfaga
    - Cada tweet es retrasado lo suficiente para cumplic con la separación mínima entre publicaciones
    - Si el retraso necesario de un tweet es mayor a 15 minutos, éste se descarta automáticamente
    - Si el canal llega a la condición de *update limit*, éste detiene el reenvío por ventanas progresivas de tiempo (5 min, 10 min, 15 min...) hasta que logre enviar exitosamente
    

.. Plataforma tecnológica
.. ----------------------


Soporte técnico
---------------

Se ha invertido un aproximado de 20 horas de soporte técnico durante el funcionamiento de la aplicación. 
Esto es un estimado según la cantidad de correos recibidos (115), asumiendo un tiempo de 10 minutos por cada correo.


Probables características futuras
---------------------------------

A continuación, se presenta un listado de dudas y características probables para implementar por cada módulo.


Usuarios
~~~~~~~~

* Roles: administrador, cliente, colaborador...
* Registro de usuarios
* Perfil del usuario
* Cambio de contraseña
* Super usuario (para el uso de posma)
* Poner un límite de canales para los usuarios de tipo cliente


Retweet automático
~~~~~~~~~~~~~~~~~~

* Sistema de modos de prioridad 
    - Qué representa un modo? Qué parámetros lo definen?
    - Son los modos una entidad configurable en el sistema?
    - Puede simularse los modos a través de funcionalidades existentes (horarios de publicación y otros parámetros de configuración)
* Permitir mentions sólo de seguidores
* Auto-respuestas según contenido
    - Cuáles son los parámetros para la activación de auto-respuestas? (Triggers, Bloqueos, otros...)
    - Aplica para DM únicamente o también para mentions?
* Uso de twitlonger para publicaciones grandes
    - Hay que enviar un email a twitlonger para solicitar acceso al API (http://www.twitlonger.com/api)
* Aclaratoria del mecanismo de "match" de palabras claves (disparadores, retenedores, supresores):
    - Las frases (palabras con espacios) harán un match textual con el contenido del tweet recibido
    - las palabras simples serán comparadas omitiendo espacios y caracteres especiales del tweet recibido
    - Existe una manera más inteligente de hacer las comparaciones?
        + Darle al usuario opciones de comparación por cada palabra clave ?
* Detallar requerimientos de la funcionalidad de hashtags


Tweets programados
~~~~~~~~~~~~~~~~~~

* Posibilidad de asociar un tweet programado a un conjunto de horas
* Desactivar y activar bloques automáticos sin necesidad de eliminarlos
* Programar tweets para envío futuro (una sola vez, no periódicamente)
    - mostrar listado de tweets programados para envío futuro (con posibilidad de eliminar / editar)
    - una vez enviados, estos tweets desaparecen del listado


Bloqueo automático
~~~~~~~~~~~~~~~~~~

* Permitir bloqueos por twitter
    - Esto se hará automáticamente según ciertas condiciones o manualmente a través del módulo de followers?
    - Cuáles serían los parámetros de configuración y criterios para el bloqueo automático?
* Detección de bots / spam  (?)
* Suspensión temporal de usuarios
    - Esto ocurre manual o automáticamente?
    - Qué parámetros de configuración tendría esta característica?
* Auto-respuestas
    - se le notifica al usuario bloqueado que ha sido bloqueado o temporalmente suspendido, explicando la razón.


Módulo de followers
~~~~~~~~~~~~~~~~~~~

* Listado de seguidores de cada canal
* Posibilidad de creación de listas de seguidores    (?)
* Cada follower tiene un vista de perfil (ficha)
    - muestra información básica (estadística de tweets, bio, seguidores, etc)
    - muestra si éste se encuentra bloqueado o en alguna otra lista
* Búsqueda manual de seguidores según parámetros (ej: localización según la biografía)
* Following automático
    - búsqueda "geolocalizada"
    - intervalos de tiempo configurable
        + aleatorización
    - dejar de seguir usuarios 
        + cuál es el criterio para dejar de seguir usuarios?
* Evaluación de seguidores
    - establecer un mecanismo concreto de evaluación / premiación de seguidores


Scanner
~~~~~~~

* Publicación de un tweet manual, a través de uno o más canales
* Listado y búsqueda de tweets enviados en los canales
    - Posibilidad de edición y re-publicación en uno o varios canales


Estadísticas y reportes
~~~~~~~~~~~~~~~~~~~~~~~~

* Falta definir qué estadísticas se requieren, por canal y globalmente
* En base a los datos que se requieran, se diseñarán las vistas de dashboard y los posibles reportes estadísticos

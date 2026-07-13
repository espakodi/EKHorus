# EKHorus - Repositorio para Kodi

Repositorio e instrucciones: https://espakodi.github.io/EKHorus/

- # ekhorus
EKHorus para Kodi: reproductor AceStream basado en Horus (Caperucitaferoz), adaptado para EspaKodi por RubénSDFA1laberot.

            Novedades de EKHorus 1.5.0:

            Menú principal
            - Ajustes pasa a ser la primera entrada, seguida de los dos menús nuevos: Descargar APKs y EspaKodi Addons.

            Descargar APKs
            - Menú nuevo para descargar e instalar los APK que hacen falta en un Fire TV o un TV box, donde pasar ficheros al aparato es un engorro: AceStream, AceServe, VLC y EspaKodi Warp. Se bajan a la carpeta del dispositivo que elijas cada vez. Son versiones de 32 bits, que es lo que instalan casi todos estos aparatos; hay un aviso en el propio menú que lo explica y enlaza a las de 64 bits.
            - Las descargas no te dejan tirado a medias: se comprueba que se pueda escribir en la carpeta antes de empezar, y no después de tragarte 100 MB. El archivo solo pasa a llamarse .apk si la descarga termina entera, y al acabar se comprueba que no esté corrupto. Si el disco se llena por el camino, avisa, en vez de dejarte un APK truncado con pinta de estar bien.
            - El botón Cancelar cancela de verdad y no deja archivos a medias en la carpeta.
            - Si el APK ya estaba descargado, se ofrece reutilizarlo en vez de bajarlo otra vez. Si el que había estaba dañado, se descarga de nuevo sin preguntar. Y dos pulsaciones seguidas ya no se pisan entre ellas.
            - En Android se ofrece instalar directamente: en Kodi 22 o posterior abre el instalador del sistema, y con root puede usar pm install. Cuando el sistema no lo permite, se dan las instrucciones para instalarlo a mano desde un gestor de archivos y un acceso directo a los ajustes de orígenes desconocidos.

            EspaKodi Addons
            - Menú nuevo con el ecosistema de addons de EspaKodi (EspaTV, EspaDaily, AtresDaily, Espanime, StreamNinja, TopZilla, loiolog, Flow FavManager, loiolink, Elementum y youtube-dl), indicando cuáles están instalados, cuáles deshabilitados y cuáles no.
            - Los instala solos: descarga el repositorio, lo registra y lanza la instalación, con reintentos y descarga directa del zip si Kodi se atasca. Si aun así falla, muestra las instrucciones para hacerlo a mano.
            - Incluye el repositorio de Elementum, así que no hace falta añadir ninguna fuente. También se instala youtube-dl, desde el repositorio oficial de Kodi.
            - Accesos al repositorio unificado y a la última versión del APK de EspaKodi.
            - Este menú no ensucia el registro de Kodi: comprueba qué addons hay instalados sin provocar un error por cada uno que falte.

            Ajustes y descargas
            - En los ajustes, los tres controles más usados (redirección a StreamNinja, reproductor externo y motor ace) pasan a estar los primeros.
            - Arreglada la barra de progreso de las descargas, que saltaba al 100% al instante y se quedaba clavada. Afectaba también a la instalación del motor AceStream.

            Novedades de EKHorus 1.4.0:

            Seguridad
            - Eliminado el uso de eval() en todo el addon. Antes, una lista de canales cargada desde una web podía ejecutar código arbitrario en el equipo, porque lo descargado se interpretaba como código Python. Ahora se interpreta como datos (JSON o literales) y nunca se ejecuta. Esto también afectaba a las cabeceras que llegan de otros addons, a los ajustes guardados y a los parámetros de las llamadas externas.

            Cuelgues y rendimiento
            - Todas las peticiones de red tienen ya un tiempo límite. Antes, un motor AceStream inalcanzable (IP mal configurada, equipo apagado) o una web de listas que no respondiera dejaban Kodi congelado.
            - Las descargas tienen un tope de tamaño, así que una dirección que devolviera gigabytes ya no puede agotar la memoria del equipo.
            - La limpieza de caché ya no recorre el disco entero. Antes, si no encontraba la carpeta de caché, escaneaba C:\ (o toda la memoria en Android) al terminar cada reproducción. Ahora comprueba las rutas conocidas y como mucho busca dentro de la carpeta del motor.
            - La versión del motor se consulta una sola vez, no en cada comprobación, así que el menú principal y el arranque de la reproducción van bastante más rápido.
            - Los códigos QR se generan una única vez y se reutilizan. Antes se reescribía un PNG por canal cada vez que se pintaba la lista.
            - Pintar una lista larga ya no relee los ajustes una vez por canal, ni reescribe el fichero de configuración al terminar cada reproducción.

            Integridad de los datos
            - El historial se escribe de forma atómica, así que si Kodi se cierra a mitad el fichero anterior queda intacto en vez de corromperse. Y si aun así apareciera dañado, el addon lo ignora en vez de fallar al abrir el historial.
            - Un código QR a medio escribir ya no queda cacheado como válido, se regenera.

            Compatibilidad
            - Eliminado distutils y las llamadas a setDaemon(), ambos retirados en Python 3.12. El addon habría dejado de arrancar en las próximas versiones de Kodi.
            - Eliminada la dependencia script.module.six (compatibilidad con Python 2, ya innecesaria) y declarada la dependencia de xbmc.python 3.0.0.
            - Los ajustes internos del addon (último ID, última búsqueda, ruta de la caché) ya se declaran como es debido. En Kodi 19 y posteriores podían no llegar a guardarse, y por eso "recordar el último ID" fallaba entre sesiones.

            Correcciones
            - Al reenviar un enlace a StreamNinja ya no aparece un aviso de "reproducción fallida" fantasma encima del vídeo que sí se estaba abriendo.
            - Un .torrent o un magnet inválido enviado por otro addon ya avisa en vez de no hacer absolutamente nada.
            - Los enlaces sin nombre ya no impiden reproducir. Antes, si el motor no daba título, la reproducción moría en silencio antes de empezar.
            - En OSMC, LibreELEC y Raspberry el motor podía darse por no arrancado y agotar la espera aunque ya estuviera funcionando.
            - El motor arranca aunque esté instalado en una ruta con espacios (por ejemplo un usuario de Windows llamado "Juan Pérez"). Antes no arrancaba nunca.
            - Si en la dirección del motor hay algo raro (esquema, barra final, espacios, un puerto pegado) ahora se entiende igual, en vez de dejar el addon mudo.
            - Un servicio que no sea AceStream respondiendo en la dirección configurada (un router, por ejemplo) ya no provoca un error interno.
            - El OSD ya no impide reproducir con skins que no declaran su resolución. Antes, con uno de esos, no arrancaba ningún vídeo.
            - Se acabaron las notificaciones de error por duplicado. Al fallar el arranque de un enlace se mostraba un segundo error inventado por el intento de parar un stream que nunca llegó a existir.
            - El menú del addon abre al instante aunque el motor esté configurado en un equipo remoto apagado. Antes se quedaba bloqueado hasta diez segundos en cada apertura.
            - Reproducir desde el historial conserva el título, la carátula y la sinopsis. Antes se perdían y la entrada se degradaba a un código.
            - Una búsqueda sin resultados (o cancelada) ya no deja una lista fantasma con solo los encabezados de origen.
            - Al buscar por texto, si uno de los dos buscadores está caído ya no se pierde también el otro. Antes un fallo en el primero anulaba la búsqueda entera.
            - Una entrada defectuosa dentro de una lista ya no descarta la lista completa, se ignora esa y se cargan las demás.
            - Si la instalación del motor quedó a medias, intentar reproducir mostraba un fallo interno en vez del aviso correspondiente.
            - Los enlaces ass:// ya no dependen en exclusiva de Google DNS. Si está bloqueado, se prueba con Cloudflare.
            - Los fallos de búsqueda ya no se silencian. Si una lista falla por red o por formato queda registrado en el log, en vez de aparecer siempre como "no se han encontrado enlaces".
            - El historial reordena, lo último visto vuelve al principio. Se amplía a 20 elementos y ahora se puede borrar, entero o elemento a elemento, desde el menú contextual (vaciarlo del todo pide confirmación).
            - Las listas que traen carátula propia vuelven a mostrarla. Hasta ahora se descartaba y se ponía el icono del addon.
            - Detener el motor es ahora fiable. Se ha corregido un fallo que podía saltar si el motor terminaba justo en ese momento, y en Linux ya no se queda a medias cuando el sistema no admite el método habitual.
            - En Windows, cerrar el motor ya no abre una consola negra encima de Kodi.
            - La instalación del motor ya no se queda colgada para siempre si el servidor de descarga no responde, y ahora avisa si la descarga falla en vez de terminar en silencio.
            - Corregida la etiqueta de velocidad de descarga del OSD, que mostraba el texto de "Estado".
            - Un vídeo que se cortaba nada más arrancar dejaba un error interno y de paso no llegaba a limpiar la caché del motor.
            - El diálogo de progreso ya no se queda colgado en pantalla si algo falla mientras se abre el enlace.
            - Los mensajes de error del motor se muestran limpios, sin los símbolos sueltos que arrastraban.
            - El código QR solo se genera para los enlaces de verdad, no para los encabezados de origen de las listas.
            - Un valor mal escrito en la IP o el puerto del motor ya no impide que el addon arranque, se usa el puerto por omisión en vez de dejar de cargar.
            - Al vaciar el historial desde el menú contextual, la lista se refresca en el acto. Antes se quedaba en pantalla la lista ya borrada.
            - Las llamadas de otros addons ya no fallan si algún parámetro contiene el carácter '='.

            Novedades de EKHorus 1.3.2:
            - Redirección a StreamNinja: ajuste nuevo que reenvía las llamadas de otros addons a horus al reproductor de StreamNinja, con protección anti-bucle.
            - Arreglado un fallo que impedía cargar el addon: el QR ahora usa pyqrcode (dependencia disponible) y es opcional.
            - Recuperado el diálogo de confirmación antes de abrir el motor AceStream en Android.
            - Cancelar la búsqueda ya no deja una entrada vacía.
            - Aviso al introducir un ID no válido, en vez de fallar en silencio.
            - Renombrado a EKHorus (adaptación para EspaKodi): nombre, enlaces de la comunidad y limpieza de recursos. El id sigue siendo script.module.horus para no romper las llamadas de otros addons. Dependencia añadida: script.module.pyqrcode.

            Diferencias respecto al Horus original de Caperucitaferoz (1.1.9):
            - Enlaces ass:// (se resuelven por DNS sobre elcano.top y se decodifican en base64/gzip, con listas anidadas).
            - Búsqueda directa por texto en acestreamsearch.net y search-ace.stream.
            - Varias fuentes a la vez separando las direcciones con ; (fusiona y elimina duplicados).
            - Formatos de lista nuevos: pastebin/.txt, elcano y páginas vercel.app / netlify.app.
            - Segundo motor org.free.aceserve (aceserve) en Android, seleccionable con el ajuste Motor ace.
            - Código QR del enlace acestream:// como carátula del elemento.
            - Listitems con la API moderna getVideoInfoTag y el ID manual admitiendo un hash de 40 caracteres.
Guía de EKHorus, AceStream y AceServe
RubénSDFA1laberot - https://espatv.github.io/
1. Las piezas y el papel de cada una
Aquí intervienen dos programas distintos:

El enlace AceStream. Un código de 40 caracteres hexadecimales (a0270364634d9c49279ba61ae3d8467809fb7095), a veces escrito como acestream://a027.... También puede ser un infohash, un enlace magnet: o un archivo .torrent. Identifica el contenido dentro de la red P2P. Por sí solo no es reproducible; no apunta a ningún servidor de vídeo.
El motor AceStream (engine). Un programa independiente: AceStream Media en Windows, el paquete snap en Ubuntu, la app Ace Stream en Android, AceServe o un contenedor Docker. Hace todo el trabajo. Se conecta a la red P2P, descarga el contenido de otros usuarios, lo reensambla y lo sirve como vídeo convencional por HTTP en http://IP:6878/...
EKHorus. El addon de Kodi. No reproduce nada por sí mismo y no incluye ningún canal. Actúa de intermediario: pide el enlace al motor, espera a que el stream arranque, pasa el vídeo resultante al reproductor de Kodi y muestra las estadísticas.
El motor convierte un enlace P2P en una dirección de vídeo normal, y EKHorus se comunica con él por HTTP. Por eso EKHorus necesita saber en qué dirección IP y en qué puerto está escuchando el motor. Es lo único que necesita saber de él. Si en esa dirección responde un motor, todo funciona. Si no responde nadie, aparece el error "Engine no iniciado".

Qué hace EKHorus por dentro, paso a paso
Cuando se reproduce un enlace ocurre lo siguiente:

EKHorus pregunta a http://IP:PUERTO/webui/api/service?method=get_version si hay un motor en esa dirección.
Si no lo hay y el motor es interno, lo arranca él mismo y espera durante el tiempo del ajuste Tiempo máximo para abrir el motor.
Pide el stream con http://IP:PUERTO/ace/getstream?id=EL_ID&format=json (o con manifest.m3u8 si se trata de un infohash, un magnet o una URL).
El motor devuelve tres direcciones, una para el vídeo, otra para las estadísticas y otra para los comandos.
Kodi reproduce la dirección del vídeo mientras EKHorus consulta las estadísticas cada segundo. De ahí sale el panel con la velocidad, las semillas y el estado del búfer.
Al parar la reproducción, EKHorus envía al motor la orden de detener el stream y borra la caché que este ha dejado en el disco.
Todo esto son peticiones HTTP corrientes contra la dirección configurada. No hay nada más.

2. Motor interno y motor externo
No existe un interruptor para elegir el modo. EKHorus lo decide según el sistema en el que corre. Aun así, entender la diferencia explica buena parte de los ajustes y de los mensajes que muestra.

Motor interno: EKHorus lo instala, lo arranca y lo detiene
La primera vez que se abre el addon, si la plataforma lo permite, descarga el motor automáticamente (aparece el mensaje "Descargando Acestream...") y lo guarda en la carpeta de datos del addon. Desde ese momento, cada vez que se reproduce algo, EKHorus lanza el proceso del motor y, si así se configura, lo cierra al terminar.

Plataformas con motor interno, y qué instala y ejecuta en cada una:

Windows. ace_engine.exe dentro de la carpeta del addon. Lo cierra con taskkill.
LibreELEC / CoreELEC / AlexELEC (ARM). acestream.start y acestream.stop.
LibreELEC x86 (root). acestream_chroot.start.
OSMC / Raspberry Pi OS / Raspbian. sudo acestream.start y sudo acestream.stop.
Ubuntu / Arch / Fedora / Mint. No descarga nada. Usa el paquete snap, que debe instalar el usuario (acestreamplayer). EKHorus lo lanza con snap run acestreamplayer.engine y avisa si no está.
En todos estos casos la dirección correcta es 127.0.0.1 y el puerto 6878, porque el motor corre en el mismo aparato que Kodi.

Motor externo: ya está en marcha y EKHorus solo lo usa
EKHorus queda en modo externo cuando no puede gestionar el motor por sí mismo. Eso ocurre siempre en Android, en Linux ARM sin root fuera de OSMC y Raspbian, en macOS y en arquitecturas poco comunes. En la práctica también ocurre cuando la IP configurada apunta a otra máquina.

En este modo EKHorus no arranca nada. Comprueba si hay un motor respondiendo en la dirección configurada y, si lo hay, reproduce. Si no lo hay, muestra el aviso "No hemos podido iniciar el motor Acestream. Asegúrese de que está iniciado antes de continuar" y espera durante los segundos configurados, para dar tiempo a arrancarlo a mano.

Casos típicos de motor externo:

AceStream Media instalado en el mismo Windows, cuando se prefiere ese en lugar del que descarga el addon. La dirección sigue siendo 127.0.0.1 y el puerto 6878.
Un motor corriendo en otro PC, un NAS o un contenedor Docker de la red local. La dirección es la IP de esa máquina.
Android, con la app Ace Stream o con AceServe.
Un Mac, donde no existe motor nativo. Lo habitual es ejecutarlo en Docker en el propio equipo (el comando está en el escenario C) y dejar la dirección en 127.0.0.1.
En las plataformas con motor interno no hace falta forzar nada para usar uno externo. Antes de arrancar el suyo, EKHorus comprueba si ya hay un motor respondiendo en la dirección configurada, y si lo hay, lo usa sin lanzar nada. Basta con tener el motor propio en marcha antes de reproducir.

Un detalle que ayuda a saber en qué modo se está. Con motor interno instalado aparecen dos ajustes adicionales, Detener el Motor Acestream automáticamente y el botón Reinstalar Acestream. Si no se ven, el addon funciona en modo externo.

3. Para qué sirven la dirección IP y el puerto
Son los dos ajustes que más se tocan sin necesidad y los que más configuraciones rompen. Su función es sencilla. No configuran el motor ni afectan a su rendimiento; solo indican a EKHorus dónde encontrarlo.

Dirección IP del servidor AceStream Engine
127.0.0.1 - Prácticamente siempre. El motor corre en el mismo aparato que Kodi, sea Windows, LibreELEC, Android o una Raspberry. Es el valor por defecto.
Una IP de la red local, por ejemplo 192.168.1.50 — El motor corre en otro equipo, como un PC de otra habitación, un NAS, un contenedor Docker o un móvil con AceServe. Kodi lo usa a través de la red.
Una IP pública o un VPS - Posible, pero desaconsejable si no se sabe exactamente lo que se hace, porque expone el motor a internet. Hay un aviso al respecto en el escenario C.
La ventaja real de apuntar a otra máquina está en el reparto del trabajo. El aparato donde se ve la televisión (un Fire TV, una Raspberry modesta, un televisor Android) no tiene que hacer el trabajo P2P, que es lo que consume procesador, memoria, red y disco. Ese esfuerzo recae en el equipo potente, y el aparato de Kodi recibe un vídeo ya convertido. Además, un solo motor puede servir a varios Kodi a la vez.

Si se usa una IP remota conviene vigilar tres cosas:

La IP del equipo del motor debe ser fija, o tener una reserva DHCP en el router. Si el router se la cambia, EKHorus dejará de encontrarlo.
El cortafuegos de la máquina del motor debe permitir conexiones entrantes al puerto 6878 desde la red local. En Windows es la causa más frecuente de que el motor funcione en el propio PC pero no se vea desde el salón.
El motor debe escuchar en la red, no solo en localhost. En Docker se resuelve publicando el puerto (-p 6878:6878). Si el motor solo escucha en 127.0.0.1, desde fuera no responderá aunque el cortafuegos esté abierto.
Y, evidentemente, el equipo del motor tiene que estar encendido. EKHorus ya no se queda bloqueado cuando no lo está (hace un sondeo rápido de dos segundos al abrir el menú), pero no podrá reproducir.

Puerto del servidor AceStream Engine
El valor por defecto es 6878, el puerto del API HTTP del motor. Conviene dejarlo así salvo que el motor escuche realmente en otro. Hay tres motivos legítimos para cambiarlo:

El motor corre en Docker con el puerto publicado en otro número. Si se publicó como -p 6880:6878, en EKHorus hay que poner 6880.
Hay dos motores en la misma máquina y el segundo escucha en otro puerto.
Otro programa ocupaba el 6878 y el motor se arrancó con un --http-port distinto.
Cambiar el puerto a ver si algo mejora no arregla nada; solo hace que EKHorus llame a una puerta donde no hay nadie. Ante la duda, los valores seguros son 127.0.0.1 y 6878.

EKHorus es tolerante con el formato. Si se escribe http://192.168.1.50/ o 192.168.1.50:6878, limpia el esquema, la barra final y el puerto pegado, y si el puerto no es un número válido recurre al 6878. Aun así, lo correcto es escribir solo la IP en un campo y solo el número en el otro.

Comprobación rápida del motor
Antes de tocar nada en Kodi se puede verificar dónde está el motor abriendo esta dirección en cualquier navegador de la misma red:

http://LA_IP:6878/webui/api/service?method=get_version&format=json
Si responde algo parecido a {"result": {"version": "3.2.3", ...}}, el motor está en marcha y es accesible desde ese punto; si EKHorus falla, el problema no es la dirección. Si la página no carga o da error de conexión, el motor no está arrancado, el cortafuegos lo bloquea o la IP y el puerto no son esos. En ese caso hay que arreglarlo ahí antes de seguir con Kodi.

Esta única comprobación resuelve la mayoría de las consultas sobre el error "Engine no iniciado".

4. Escenarios:
A) Windows, la opción más sencilla (motor interno)
Instala EKHorus desde el repositorio.
Ábrelo. La primera vez descargará el motor automáticamente.
Comprueba los ajustes. IP 127.0.0.1, puerto 6878, sin tocar nada más.
Entra en Reproducir identificador Acestream, pega un ID y espera a que cargue.
Si Windows Defender u otro antivirus bloquea ace_engine.exe, habrá que añadir una exclusión; de lo contrario el motor no arrancará nunca.

B) Windows con AceStream Media ya instalado (motor externo local)
Para usar la instalación oficial en lugar del motor que descarga el addon:

Arranca AceStream Media (o su Engine) antes de abrir el enlace en Kodi. Su icono aparece en la bandeja del sistema.
En EKHorus, IP 127.0.0.1 y puerto 6878. Al detectar un motor ya en marcha, el addon lo usará sin arrancar el suyo.
Puedes cerrarlo a mano o desde la entrada Detener motor Acestream del menú del addon. Ten en cuenta que el ajuste Detener el Motor Acestream automáticamente, si está activado, también cerrará este motor al terminar, porque el cierre se hace por nombre de proceso.
C) Motor en otro equipo (PC, NAS, Docker) y Kodi en el televisor
Es el montaje que mejor rinde en aparatos poco potentes.

En la máquina que hará de servidor, arranca el motor y asegúrate de que escucha en la red. En Docker, la vía más limpia es docker run -d --name acestream -p 6878:6878 vstavrinov/acestream-engine. En Windows o Linux nativo basta con arrancar el motor y abrir el puerto 6878 en el cortafuegos.
Averigua la IP de esa máquina con ipconfig o ip a, por ejemplo 192.168.1.50, y fíjala en el router.
Desde otro aparato de la red, abre en un navegador http://192.168.1.50:6878/webui/api/service?method=get_version&format=json. Si no responde, el problema está en el cortafuegos o en el propio motor, no en Kodi, y hay que resolverlo antes de continuar.
En EKHorus, IP 192.168.1.50 y puerto 6878.
Reproduce con normalidad.
Una limitación que conviene conocer. La entrada Detener motor Acestream del menú solo puede cerrar motores que corran en el mismo aparato que Kodi; con un motor remoto aparecerá el aviso "Motor Acestream NO cerrado". Un motor en otra máquina se detiene desde esa máquina.

Aviso de seguridad: no abras el puerto 6878 en el router hacia internet. El API del motor no tiene autenticación, de modo que cualquiera podría usar tu conexión para descargar y compartir contenido en tu nombre. Dentro de la red local no hay problema.
D) Android o Android TV con la app oficial Ace Stream
En Android EKHorus no puede arrancar el motor por su cuenta, porque el sistema no lo permite. Lo que hace es abrir la app correspondiente.

Instala la app Ace Stream (Ace Stream Media o Ace Stream Engine) en el mismo aparato.
En los ajustes de EKHorus, en Motor ace, deja seleccionada la opción org.acestream.----, que corresponde a la app oficial.
IP 127.0.0.1 y puerto 6878.
Al reproducir, EKHorus preguntará si quieres que abra el motor. Acepta y se abrirá la app de AceStream. Cuando el motor esté iniciado, vuelve a Kodi con el botón Atrás; EKHorus sigue esperando y continuará solo.
Si la app de AceStream queda abierta en segundo plano, ese diálogo no vuelve a aparecer.
En Fire TV y Fire Stick el procedimiento es el mismo, porque Fire OS es Android, con una salvedad. La app de AceStream no está en la tienda de Amazon, así que hay que instalar el APK aparte, normalmente con la aplicación Downloader. Una vez instalada, todo funciona igual que en cualquier Android TV.

E) Android con AceServe (org.free.aceserve)
AceServe es un motor AceStream para Android planteado como servidor y no como reproductor. Se queda en segundo plano, escucha en el puerto 6878, no tiene publicidad, puede arrancar con el sistema y trae su propia interfaz web. Es la opción preferida de muchos usuarios de televisores Android porque se comporta como el motor de Linux; una vez encendido, todo va por HTTP y no hay que saltar entre aplicaciones.

Instala el APK de AceServe y ábrelo una vez para que arranque el servicio. Si trae la opción de autoarranque, actívala.
En los ajustes de EKHorus, en Motor ace, selecciona org.free.aceserve.
IP 127.0.0.1 y puerto 6878, puesto que corre en el mismo aparato.
Reproduce con normalidad.
El ajuste Motor ace no es decorativo. Cambia dos cosas concretas. La primera, cómo se abre el motor cuando no está en marcha, porque cada app requiere una llamada distinta del sistema. La segunda, en qué carpeta se limpia la caché al terminar (/storage/emulated/0/org.free.aceserve/files/.ACEStream/ en AceServe y otra ruta en la app oficial). Si el ajuste no coincide con la app instalada, la caché no se limpia y el almacenamiento se va llenando.

F) AceServe y Kodi en aparatos distintos
AceServe corriendo en un móvil o televisor Android y Kodi en otro aparato es exactamente el escenario C. En EKHorus se pone la IP del dispositivo con AceServe y el puerto 6878. Conviene tener en cuenta que un móvil con la pantalla apagada puede dormir el servicio; para un servidor estable es preferible un PC o un contenedor Docker.

G) AceStream o AceServe con VLC, sin Kodi
Esta combinación no usa EKHorus, pero merece la pena conocerla porque es la mejor herramienta de diagnóstico disponible. Si un enlace funciona en VLC, el motor está bien y el problema está en Kodi.

Con el motor arrancado, en VLC se abre Medio > Abrir ubicación de red y se pega:

http://127.0.0.1:6878/ace/getstream?id=EL_ID_DE_40_CARACTERES
Variantes útiles:

http://IP:6878/ace/getstream?id=HASH — La forma habitual (MPEG-TS progresivo), con menos latencia.
http://IP:6878/ace/manifest.m3u8?id=HASH — Lo mismo en formato HLS. Funciona mejor en algunos reproductores y en Chromecast.
http://IP:6878/ace/getstream?infohash=HASH — Cuando se tiene un infohash de torrent en lugar de un identificador de contenido.
http://IP:6878/ace/getstream?url=http://.../algo.acelive — Cuando se tiene la URL de un fichero de transporte.
http://IP:6878/webui/app/mediaplayer — La interfaz web del propio motor.
Si el motor está en otra máquina se sustituye 127.0.0.1 por su IP. Es la misma URL que EKHorus construye internamente.

H) Reproductor externo en Android
Este ajuste, visible solo en Android, hace que EKHorus no reproduzca en Kodi y entregue el enlace a otra aplicación.

Con AceServe seleccionado, lanza la URL http://IP:PUERTO/ace/getstream?id=... como vídeo, de modo que Android ofrece abrirla con VLC, MX Player o el reproductor que haya instalado.
Con la app oficial, entrega el enlace a Ace Stream y reproduce ella.
Su utilidad real está en los canales que en Kodi se cortan, se ven a saltos o no arrancan (algo habitual con ciertos códecs o con el descodificador por hardware del televisor) pero que en VLC o en la app de AceStream funcionan sin problema. A cambio se pierde el panel de estadísticas, el historial deja de alimentarse y la reproducción ocurre fuera de Kodi. Además, este ajuste solo actúa con identificadores de contenido; los torrents y los magnets se reproducen siempre en Kodi.

5. Los ajustes de EKHorus:
Redirigir a StreamNinja las llamadas de otros addons. Solo aparece con StreamNinja instalado. Cuando otro addon pide reproducir un acestream, EKHorus se lo pasa al reproductor de StreamNinja, con protección contra bucles (si StreamNinja lo devuelve, lo reproduce EKHorus). Recomendación: activarlo solo si se prefiere el motor de StreamNinja.
Dirección IP del servidor AceStream Engine. Dónde está el motor (sección 3). Recomendación: 127.0.0.1 salvo motor remoto.
Puerto del servidor AceStream Engine. El puerto del API HTTP del motor. Recomendación: 6878 salvo que se sepa que es otro.
Tiempo máximo para abrir el motor Acestream (10 a 120 s). Cubre dos esperas, la del arranque del motor y la del inicio del enlace antes de darse por vencido. Recomendación: 30 segundos funcionan bien en un PC. En Raspberry, Fire TV o con motor remoto conviene subir a 60 o 90. Si aparece "Engine no iniciado" pero el motor acaba arrancando, es este ajuste.
Mostrar información Acestream en OSD. El panel con estado, velocidades, semillas y datos transferidos que aparece al mostrar los controles durante el vídeo. Recomendación: útil para saber si un canal va mal por falta de semillas. Puede desactivarse si molesta o si el skin da problemas con él.
Recordar último ID operativo. Deja precargado en el cuadro de reproducción el último enlace que funcionó más de tres minutos. Recomendación: cómodo si se repite canal a diario.
Mostrar QR. Usa como carátula de cada canal un código QR con su enlace acestream://, pensado para escanearlo con el móvil y abrirlo allí. Recomendación: mejor desactivado si no se usa; cada QR genera una imagen en la carpeta temporal.
Motor ace (solo Android). Elige entre la app oficial (org.acestream.----) y AceServe (org.free.aceserve). Determina cómo se abre el motor y dónde está su caché. Recomendación: debe coincidir con la app instalada.
Reproductor externo (solo Android). Entrega el enlace a otra aplicación en lugar de reproducir en Kodi (escenario H). Recomendación: alternativa para canales que fallan en Kodi.
Detener el Motor Acestream automáticamente (solo motor interno). Cierra el proceso del motor al terminar la reproducción. Recomendación: activarlo si molesta que el motor siga consumiendo red y procesador compartiendo contenido cuando ya no se ve nada. Mejor desactivado si se encadenan varios canales, porque volver a arrancarlo lleva su tiempo.
Reinstalar Acestream (solo motor interno). Vuelve a descargar y descomprimir el motor. Recomendación: lo primero que probar si el motor interno se ha dañado y no arranca.
En Ubuntu con snap el motor se detiene siempre al terminar, con independencia del ajuste.

6. Más allá de pegar un ID
Reproducir identificador Acestream / Torrent URI acepta varias cosas:

Un ID de 40 caracteres, con o sin el prefijo acestream://.
Un enlace magnet:.
Una URL que termine en .torrent.
La URL de un fichero de transporte (.acelive).
Buscar enlaces... admite en el mismo cuadro:

Texto libre (la 1, por ejemplo), que se busca en acestreamsearch.net y en search-ace.stream.
La URL de una lista, ya sea JSON, M3U, pastebin, .txt, páginas de elcano, vercel.app, netlify.app o cualquier página de la que se puedan extraer hashes de 40 caracteres.
Un enlace ass://, que se resuelve por DNS (primero Google y, si está bloqueado, Cloudflare).
Varias fuentes a la vez separadas con ;. Los resultados se fusionan y se eliminan los duplicados.
Historial de reproducciones guarda los veinte últimos vídeos vistos durante más de tres minutos, con su título y su carátula. Se puede borrar entrada a entrada o completo desde el menú contextual.

Detener motor Acestream solo aparece en el menú cuando se detecta un motor en marcha, y no está disponible en Android. Como se indicó en el escenario C, solo puede cerrar motores locales.

7. Diagnóstico
El orden correcto es siempre el mismo:

¿Responde http://IP:6878/webui/api/service?method=get_version&format=json en el navegador?
¿Funciona el enlace en VLC con http://IP:6878/ace/getstream?id=...?
Solo si las dos anteriores van bien, el problema está en Kodi o en EKHorus.
Síntomas habituales, su causa y su solución:

"Engine no iniciado". El motor no está arrancado, no está donde indica la configuración o tardó más de lo permitido. Comprobar con la URL del navegador. Revisar IP y puerto. Subir el tiempo máximo a 60 o 90 segundos. En Windows, comprobar que el antivirus no bloquee ace_engine.exe.
Funcionaba y dejó de funcionar (motor en otro equipo). El router cambió la IP del servidor. Reserva DHCP o IP fija.
Desde el PC funciona, desde el televisor no. Cortafuegos del equipo del motor, o motor escuchando solo en localhost. Abrir el 6878 en el cortafuegos. En Docker, publicar el puerto.
El canal se queda en "Pre-Buffer". No hay semillas: el enlace está muerto o el evento no ha empezado. No es un problema de configuración. Si el panel muestra cero o una semilla, ese enlace no va a dar vídeo; hay que probar otro.
Se ve a tirones o se corta. Pocas semillas, red insuficiente o el aparato no puede descodificar el vídeo. Probar el mismo ID en VLC. Si en VLC va bien y en Kodi no, el problema es del reproductor de Kodi (en Android puede servir Reproductor externo). También puede ayudar subir el búfer en vivo en los ajustes del propio motor, un valor entre 30 y 60 segundos.
"No se han encontrado enlaces en...". La lista cambió de formato o está caída. Probar otra fuente. Los fallos quedan registrados en el log de Kodi.
"El ID no tiene un formato válido". Lo pegado no es un hash hexadecimal de 40 caracteres. Copiar el enlace completo, sin espacios ni saltos de línea.
El almacenamiento se llena (Android). El ajuste Motor ace no coincide con la app instalada y la caché se limpia en la ruta equivocada. Corregir el ajuste y borrar a mano la carpeta .ACEStream.
El motor sigue consumiendo tras cerrar Kodi. Es el comportamiento normal; sigue compartiendo contenido. Activar Detener el Motor Acestream automáticamente o usar Detener motor Acestream.
El log de Kodi es la fuente definitiva. Todo lo que hace el addon queda registrado con la etiqueta [script.module.horus]. En Windows está en %APPDATA%\Kodi\kodi.log.

8. Preguntas frecuentes
¿EKHorus tiene canales? No. No incluye películas, series ni deportes. Es un reproductor, y los enlaces los aporta el usuario.

¿De dónde salen los enlaces entonces? De la función Buscar enlaces (sección 6), que admite búsqueda por texto y listas publicadas en la web, y de lo que compartan las comunidades de usuarios. La tecnología AceStream es legal; la legalidad de un contenido concreto depende de sus derechos de emisión y es responsabilidad de quien lo reproduce.

¿En qué versiones de Kodi funciona? En Kodi 19 (Matrix) y posteriores. En Kodi 18 o anteriores no, porque EKHorus usa Python 3.

¿Funciona en Xbox, Apple TV, iPhone o una Smart TV? Kodi existe para Xbox y Apple TV, pero el motor AceStream no, así que en esos aparatos la única vía es un motor remoto en otra máquina de la red, tal como se describe en el escenario C. En iPhone y en las Smart TV de webOS o Tizen no hay ni Kodi ni motor; lo más práctico es un motor remoto y reproducir su dirección con VLC o con cualquier app que acepte URL de red, como se explica en el escenario G.

¿Hay que instalar AceStream aparte? En Windows, LibreELEC, CoreELEC, OSMC y Raspberry no; EKHorus lo descarga automáticamente. En Android sí, la app oficial o AceServe. En Ubuntu y derivados también, mediante el snap acestreamplayer. Y en cualquier plataforma, si ya existe un motor propio en marcha, EKHorus lo usa sin arrancar el suyo.

¿AceServe o la app oficial? AceServe para tener un servidor limpio en segundo plano, sin publicidad, con autoarranque y al que puedan conectarse otros aparatos. La app oficial si además se quiere su reproductor. Lo único imprescindible es que el ajuste Motor ace coincida con la app instalada.

¿Puede un motor servir a varios Kodi? Sí, y es una de las mejores razones para cambiar la IP. Un motor y varios clientes apuntando a su dirección, cada uno con un canal distinto si el equipo lo aguanta.

¿Cambiar el puerto mejora algo? No. No arregla cortes, ni velocidad, ni canales muertos. Solo tiene sentido cuando el motor escucha realmente en otro puerto.

¿Por qué sube datos si solo se está viendo un canal? Porque es P2P. Mientras se ve, se comparte con otros usuarios, y eso aparece en el panel como subida. No se puede desactivar desde EKHorus; es el funcionamiento de la red, y es también el motivo para no exponer el motor a internet.

¿Hace falta VPN? EKHorus no la incluye ni la gestiona. En AceStream, como en cualquier red P2P, la IP del usuario es visible para el resto de participantes. Con ese dato, la decisión es de cada uno.

9. Importante:
El motor hace el trabajo y EKHorus solo se comunica con él por HTTP.
La IP y el puerto indican dónde está el motor. 127.0.0.1 y 6878 si corre en el mismo aparato; la IP de la otra máquina si corre en otra.
Motor interno significa que EKHorus lo instala y lo arranca (Windows, LibreELEC y similares, OSMC). Motor externo significa que ya está en marcha (Android, motor remoto, Docker o una instalación propia).
Ante cualquier fallo, lo primero es comprobar el motor en el navegador con http://IP:6878/webui/api/service?method=get_version&format=json.
Guía para EKHorus 1.4.0 (basado en Horus). Comunidad en t.me/espakodi.














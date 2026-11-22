# Letras para FreeShow

Página web para **buscar letras de canciones**, ordenarlas en grupos (Verso, Coro, Puente…) y **crearlas en FreeShow** con su formato nativo. La canción se guarda en la biblioteca, dentro de la categoría que elijas. **No se añade a ningún proyecto.**

**Abrir:** https://lordg95.github.io/letras-freeshow/

Funciona con cualquier computador que tenga FreeShow instalado, sin modificar FreeShow, así que las actualizaciones de FreeShow no la rompen.

## Configuración en cada computador (una sola vez)

1. En FreeShow abre **Configuración → Conexiones**.
2. Activa **API**. Usa el puerto 5505 por defecto.
3. Activa **RemoteShow** (puerto 5510) y anota su contraseña. Sirve para que la página muestre los nombres de tus categorías.
4. Abre la página en **Chrome o Edge**, pulsa ⚙ y escribe la contraseña de RemoteShow.
5. Si el navegador pide permiso para **acceder a dispositivos de la red local**, pulsa **Permitir**. Es la forma en que la página habla con FreeShow en el mismo computador. Si lo rechazaste por error: icono a la izquierda de la dirección → *Configuración del sitio* → *Acceso a la red local* → *Permitir*, y recarga.

La configuración se guarda solo en ese navegador.

## Uso

1. **Buscar**: escribe el título, el artista o el número de himno.
   - Primero aparece lo que **ya está en tu FreeShow**, por título o por número («245», «himno 245»). Al hacer clic se abre en FreeShow sin proyectarse.
   - Los resultados de **LRCLIB** traen la letra completa.
   - Los de **Letras.com** se intentan completar solos. Si no se puede, aparece un botón para abrir la página.
   - **Buscar en la web**: botones que abren la búsqueda en Google, Letras.com, Musixmatch, Musica.com, Genius, LaCuerda, Cifra Club, YouTube o Hymnary.
2. **Copiar y pegar**: en la página de la canción copia la letra, vuelve a la herramienta y pulsa **⌘V** (Ctrl+V en Windows) en cualquier parte. También sirve el botón **Pegar y ordenar**.
   - Se conservan los espacios entre estrofas. Sitios como Musixmatch los dibujan solo como margen y al copiar se pierden: la herramienta los recupera del formato que viaja con lo copiado.
   - Se quita sola la «basura» de la página: créditos, botones, contadores, enlaces, hashtags, acordes y tablaturas. En «Ver lo que se quitó» se puede revisar.
   - Los autores («Writer(s)», «Composición», «Escrita por») y el © se guardan como metadatos de la canción.
   - Si la página trae el título y el artista arriba, se usan para el nombre.
   - **Enlace de la canción**: si pegas la dirección (Musixmatch, Letras.com, Cifra Club, LaCuerda), se preparan el nombre y el artista y se busca la letra en LRCLIB. Si no está, solo queda copiar la letra de la página y pulsar ⌘V.
3. **Ordenar**: cada estrofa es un bloque con su grupo.
   - Si la letra trae títulos («Coro», «Verso 2», «[Puente]», «Pre-coro», también en inglés como en Genius), se respetan. Un «Coro» suelto sin texto significa que el coro se repite ahí.
   - En los himnos, las estrofas numeradas («1.», «2.») son versos. Si el coro aparece una sola vez, se repite después de cada estrofa.
   - Sin títulos, los grupos se detectan solos: lo que se repite es Coro, lo nuevo tras el segundo coro es Puente, etc. Se pueden cambiar a mano.
   - Una línea en blanco dentro de un bloque crea otra diapositiva del mismo grupo.
   - Cada bloque tiene botones para añadir otro bloque arriba o abajo (**+**), subir, bajar, duplicar o eliminar. Los bloques vacíos no se envían.
   - Opciones: líneas por diapositiva, quitar acordes, quitar «(x2)/Bis» y mayúscula inicial.
4. **Crear en FreeShow**: elige la categoría y listo. Si la categoría tiene plantilla, FreeShow la aplica sola.

## Cómo funciona

- Usa la acción `create_show` de la API de FreeShow (WebSocket, socket.io 4.8.1). Es el mismo convertidor de **Nuevo show → Texto**: grupos globales, diapositivas hijas y coros repetidos fusionados en una sola diapositiva.
- FreeShow inserta toda canción nueva en el proyecto abierto. La página la retira enseguida con `remove_project_item`, que usa índices desde 1, y verifica que el resto del proyecto quede intacto.
- Los encabezados se envían con el id global del grupo (`[verse]`, `[chorus]`, `[bridge]`…). Así FreeShow los reconoce en cualquier idioma y con sus colores.
- Las categorías se leen del canal RemoteShow. Si no está disponible, se usan «Canciones» y «Presentaciones».

Es un solo archivo (`index.html`) sin dependencias externas: el cliente socket.io va incrustado. También funciona abriéndolo con doble clic.

## Fuentes de letras

- Tu biblioteca de FreeShow, por nombre y número de acceso rápido.
- [LRCLIB](https://lrclib.net): base abierta, sin clave.
- Buscador de [Letras.com](https://www.letras.com): solo títulos y enlaces.
- **Cualquier otra página** (Musixmatch, Letras.com, Musica.com, Genius, LaCuerda, Cifra Club, YouTube, Hymnary…): se abre con los botones de «Buscar en la web», se copia la letra y se pega con ⌘V. La herramienta la limpia y la ordena.

Esos sitios no permiten que otra página web lea su contenido, por eso la letra se copia a mano. Leerlos de forma automática requeriría un servidor o un servicio de pago que copie sus páginas, que se rompe cuando cambian su diseño y va contra sus condiciones de uso. La herramienta no usa ninguna clave ni servicio de pago.

Respeta los derechos de autor y la licencia CCLI de tu iglesia al proyectar letras.

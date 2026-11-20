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

1. **Buscar**: escribe el título, el artista o ambos.
   - Los resultados de **LRCLIB** traen la letra completa.
   - Los de **Letras.com** se intentan completar solos. Si no se puede, aparece un botón para abrir la página: copias la letra y la pegas en «Pegar letra».
2. **Ordenar**: cada estrofa es un bloque con su grupo.
   - Los grupos se detectan solos: lo que se repite es Coro, lo nuevo tras el segundo coro es Puente, etc. Se pueden cambiar a mano.
   - Una línea en blanco dentro de un bloque crea otra diapositiva del mismo grupo.
   - Opciones: líneas por diapositiva, quitar acordes, quitar «(x2)/Bis» y mayúscula inicial.
3. **Crear en FreeShow**: elige la categoría y listo. Si la categoría tiene plantilla, FreeShow la aplica sola.

## Cómo funciona

- Usa la acción `create_show` de la API de FreeShow (WebSocket, socket.io 4.8.1). Es el mismo convertidor de **Nuevo show → Texto**: grupos globales, diapositivas hijas y coros repetidos fusionados en una sola diapositiva.
- FreeShow inserta toda canción nueva en el proyecto abierto. La página la retira enseguida con `remove_project_item`, que usa índices desde 1, y verifica que el resto del proyecto quede intacto.
- Los encabezados se envían con el id global del grupo (`[verse]`, `[chorus]`, `[bridge]`…). Así FreeShow los reconoce en cualquier idioma y con sus colores.
- Las categorías se leen del canal RemoteShow. Si no está disponible, se usan «Canciones» y «Presentaciones».

Es un solo archivo (`index.html`) sin dependencias externas: el cliente socket.io va incrustado. También funciona abriéndolo con doble clic.

## Fuentes de letras

- [LRCLIB](https://lrclib.net): base abierta, sin clave.
- Buscador de [Letras.com](https://www.letras.com): solo títulos y enlaces.

Respeta los derechos de autor y la licencia CCLI de tu iglesia al proyectar letras.

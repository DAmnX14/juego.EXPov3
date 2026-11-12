# Adiviná antes de ver

Juego para la exposición del informe estadístico sobre la **tasa de natalidad en Argentina (2000–2024)**.
El público apuesta contra el reloj y, recién después, se abre el telón y aparecen los datos reales.
Paleta verde, blanco y negro, con música retro en el menú de inicio.

Proyecto de Estadística y probabilidad, Tecnicatura Superior en Ciencia de Datos e IA.
Desarrollado por Damián Tejerina. Profesor: Sergio Mansilla.

## Cómo jugar

1. Escribí el nombre del jugador o equipo (se usa para el ranking).
2. Elegí la dificultad y el tiempo para votar (10, 15, 20, 30 segundos o sin tiempo).
3. Leé la pregunta en voz alta. El público vota levantando la mano.
4. Tocá la opción de la mayoría: se abre el telón y se muestra el gráfico real.

Teclas: `A`–`D` o `1`–`4` para elegir, `Enter` para seguir, `M` para silenciar sonido y música.
La música del menú empieza con el primer toque o tecla (los navegadores no permiten sonido automático) y se apaga al empezar la partida.

## Niveles

| Nivel | Preguntas | Tiempo sugerido | Puntos |
|---|---|---|---|
| Fácil | 10: años, máximos, mínimos, comparaciones | 30 s | x1 |
| Medio | 10: media, mediana, moda, porcentajes, tendencias | 20 s | x1,5 |
| Difícil | 10: dispersión, cuartiles, asimetría, variación porcentual | 15 s | x2 |
| Mixto | 10 al azar de las 30 | 20 s | x1,5 |

Cada acierto da 100 puntos más 10 por cada segundo que sobraba, multiplicado por el factor del nivel.
Todas las respuestas se calculan con los datos del CSV: no hay valores escritos a mano.

## Ranking

Por defecto se guarda en el navegador (`localStorage`) de la computadora donde se juega, separado por nivel.
Si se abre en otro dispositivo o navegador, empieza vacío. Los jugadores no ven botón para borrarlo; quien organiza lo reinicia
abriendo el juego con `?admin=1` al final de la dirección (no es una protección de seguridad: borrar los datos del sitio también lo reinicia).

### Ranking compartido entre todos los dispositivos (opcional, gratis)

Con una base de datos gratuita de Firebase, todos ven el mismo ranking aunque jueguen desde otro navegador, celular o computadora.
Se actualiza solo cada 10 segundos y tiene un botón **Actualizar**.

1. Entrá a <https://console.firebase.google.com> con una cuenta de Google y creá un proyecto (podés desactivar Google Analytics).
2. En el menú **Compilación → Realtime Database → Crear base de datos**. Elegí la ubicación y empezá en **modo bloqueado**.
3. Abrí la pestaña **Reglas**, borrá lo que hay, pegá el contenido de `firebase-rules.json` y tocá **Publicar**.
   Esas reglas permiten leer y agregar puntajes, pero no modificarlos ni borrarlos, y validan nombre y puntos.
4. Copiá la dirección de la base (arriba de la pestaña **Datos**, algo como `https://mi-proyecto-default-rtdb.firebaseio.com`).
5. En `index.html` buscá la línea `const RANK_DB = '';` y pegá la dirección entre las comillas. Guardá y subí el cambio a GitHub.

Notas:
- Los jugadores no pueden borrar el ranking. Para reiniciarlo, entrá a la consola de Firebase, abrí **Realtime Database → Datos** y eliminá el nodo `ranking` (o solo el de un nivel).
- Si un jugador pierde la conexión, su puntaje queda guardado en ese dispositivo y se envía la próxima vez que abra el ranking.
- La base es pública para leer y agregar: los nombres y puntajes los ve cualquiera que abra el juego, y alguien con conocimientos técnicos podría mandar un puntaje inventado. Para una clase alcanza; no sirve para competencias con premios.

## Contenido

| Archivo | Qué es |
|---|---|
| `index.html` | Juego principal (30 preguntas, niveles, ranking local o compartido, música, sonidos, temporizador) |
| `juegos/adivina-antes-de-ver-v3-violeta.html` | Misma versión con la paleta violeta, sin música |
| `juegos/mayor-o-menor.html` | Otro juego con los mismos datos |
| `firebase-rules.json` | Reglas para el ranking compartido (opcional) |
| `datos/tasa-natalidad-deis-2000-2024.csv` | Datos originales (DEIS) |

Cada HTML es un archivo único con los datos adentro: se abre con doble clic, sin instalar nada.

## Publicarlo en GitHub Pages

En el repositorio: **Settings → Pages → Deploy from a branch → main / (root)**.
Queda en `https://TU-USUARIO.github.io/NOMBRE-DEL-REPO/`.

## Datos

Tasa de natalidad por 1.000 habitantes, Argentina y 24 jurisdicciones, 2000–2024. Fuente: DEIS (Ministerio de Salud).

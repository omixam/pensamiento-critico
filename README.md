# pensamiento-critico

Skill para Claude Code que analiza textos argumentativos aplicando el marco de
los **8 elementos del pensamiento** y los **estándares intelectuales universales**
de Richard Paul y Linda Elder, junto con la **detección de falacias lógicas**
y **sesgos cognitivos** relevantes.

El objetivo no es destrozar el texto: es ayudarte a entenderlo mejor y a pensar
por ti mismo.

## Para quién es

Cualquier persona que use Claude Code y quiera leer con más rigor textos
argumentativos: artículos de opinión, ensayos, posts de redes, columnas,
discursos, comunicados, ponencias. Funciona también con PDFs (los convierte a
texto antes de analizar) y con imágenes (las transcribe primero).

## Qué hace

Cuando le pasas un texto, la skill produce un reporte estructurado con:

- **Síntesis** del texto en una o dos frases (lo que el autor está diciendo, sin
  estilizarlo ni caricaturizarlo).
- **Análisis por los 8 elementos** de Paul-Elder (propósito, pregunta, información,
  inferencias, conceptos, supuestos, implicaciones, punto de vista) evaluados
  contra los **9 estándares intelectuales** (claridad, exactitud, precisión,
  relevancia, profundidad, amplitud, lógica, importancia, justicia).
- **Falacias lógicas** detectadas, con cita literal del texto y explicación de
  por qué lo es y por qué importa.
- **Sesgos cognitivos** que parezcan operar en la selección o el peso de la
  evidencia.
- **Test de simetría ideológica** — ¿el mismo argumento aplicado al "otro lado"
  sostendría el mismo juicio?
- **Limitaciones del análisis** — incluida la **declaración explícita de
  no-neutralidad** del propio analizador (ver más abajo).

El tono es **conversacional y didáctico**, no forense. El reporte se ajusta a la
longitud y tipo de texto: un post breve no recibe el mismo despliegue que un
ensayo largo.

## Filosofía

- **Didáctica antes que forense.** Un reporte que enseña a leer mejor vale más
  que uno que demuestra haber encontrado todos los errores posibles.
- **Interpretación caritativa antes de criticar** (steel-manning). Reconstruir
  el argumento en su versión más fuerte antes de señalar su debilidad.
- **Honestidad sobre el analizador.** La skill corre sobre un modelo de lenguaje
  con valores morales ya cargados e inclinaciones políticas asimétricas. La
  skill **lo declara** en su reporte cuando el tema lo requiere. Usar esta skill
  en Claude **no es prueba de neutralidad**.
- **Ayuda a pensar, no sustituye al juicio.** El reporte es una segunda lectura
  estructurada, no un veredicto.

## Instalación

La skill se distribuye como un directorio con un archivo `SKILL.md` y carpetas
de referencia. Para que Claude Code la cargue:

1. Clona el repo en el directorio de skills de Claude Code de tu usuario:

   ```bash
   git clone https://github.com/<TU-USUARIO>/<NOMBRE-DEL-REPO>.git \
     ~/.claude/skills/pensamiento-critico
   ```

   (Si la ruta `~/.claude/skills/` no existe en tu sistema, créala con
   `mkdir -p ~/.claude/skills/`.)

2. Reinicia Claude Code (o recarga las skills, según tu versión).

3. Verifica que carga: en una conversación nueva, pega cualquier texto
   argumentativo corto y pide *"analízalo con pensamiento crítico"*. Si ves un
   reporte estructurado con los 8 elementos, está funcionando.

> Si tu instalación de Claude Code lee skills desde otra ruta, ajústalo. La
> documentación oficial de Claude Code tiene la ruta concreta para tu sistema.

## Cómo usarla

Tres formas habituales:

- **Pegando texto en el chat.** *"Analiza esto con pensamiento crítico: [texto]"*.
- **Adjuntando un archivo.** Funciona con `.md`, `.txt` y `.pdf` (convierte el
  PDF a texto antes de analizar).
- **Pasando un enlace.** *"Pásame este artículo por la skill: [URL]"*. La skill
  intentará leer el contenido; si está tras paywall o requiere login, te lo
  dirá y te pedirá que pegues el texto.
- **Pasando una imagen.** Foto de página de periódico, captura de un post largo,
  diapositiva. La skill transcribe primero y avisa en el reporte de que el
  análisis se hace sobre transcripción propia.

Algunos prompts útiles:

- *"¿Qué problemas tiene este argumento?"*
- *"¿Es sólido este razonamiento?"*
- *"Detecta falacias y sesgos en este texto."*
- *"Hazlo en versión breve, dos párrafos."* — la skill ajusta la profundidad.

## Limitaciones honestas

- **No es neutral.** El modelo subyacente tiene valores cargados; ante temas
  con consenso moral fuerte (violencia sexual, racismo, terrorismo,
  negacionismo) tenderá por defecto a alinearse con ese consenso, incluso
  cuando el ejercicio crítico exigiría aplicar la misma exigencia a las dos
  partes. Ante temas políticamente polarizados, la sensibilidad para detectar
  falacias suele ser asimétrica: más fina cuando el texto contradice el
  consenso del modelo, más laxa cuando lo confirma. La skill lo declara en el
  reporte, pero no lo elimina.
- **El catálogo de falacias es curado, no exhaustivo.** Cubre las que más
  aparecen en debate público. Para casos difíciles, ver
  [`doc/falacias-bibliografia.md`](doc/falacias-bibliografia.md).
- **No verifica datos automáticamente.** Si el texto cita una fuente, la skill
  intenta leerla (vía WebFetch) y contrastar; si no puede, lo dice. No reemplaza
  un *fact-check* riguroso.
- **No funciona bien con todo tipo de texto.** Está hecha para textos que
  argumentan o persuaden. En narrativa, ficción, documentación técnica o noticia
  informativa pura, rinde a medias o nada. En esos casos la propia skill avisa
  al principio del reporte.

## Bibliografía y créditos

El marco teórico viene de:

- **Richard Paul & Linda Elder** — Foundation for Critical Thinking
  ([criticalthinking.org](https://www.criticalthinking.org/)). Los 8 elementos
  del pensamiento y los estándares intelectuales son obra suya. La skill no
  redistribuye sus mini-guías oficiales; consúltalas en su web.
- **Montserrat Bordes Solanas** — *Las trampas de Circe: falacias lógicas y
  argumentación informal* (Cátedra, 2011). Tratado en español que ha servido de
  base teórica para el catálogo de falacias.
- **Douglas Walton** — *Informal Logic: A Pragmatic Approach* (Cambridge UP, 2008).
- **Charles Hamblin** — *Fallacies* (Methuen, 1970).

Bibliografía completa con citas en
[`doc/falacias-bibliografia.md`](doc/falacias-bibliografia.md).

## Licencia

[MIT](LICENSE). El código y la organización de la skill se distribuyen bajo MIT.
La skill **no redistribuye** ninguna de las obras citadas en la bibliografía:
para profundizar, adquiérelas o consúltalas en biblioteca.

## Contribuciones

Issues y PRs bienvenidos. Lo más útil:

- **Casos donde la skill falla**: textos en los que produce un análisis pobre,
  forzado o tendencioso. Pega el texto y describe qué esperabas. Esos casos son
  oro para mejorar los catálogos de `references/`.
- **Falacias mal etiquetadas o ausentes** en
  [`references/falacias-graves.md`](references/falacias-graves.md).
- **Sesgos cognitivos** relevantes que falten en
  [`references/sesgos-cognitivos.md`](references/sesgos-cognitivos.md).
- **Mejoras al test de simetría ideológica** o a la sección de no-neutralidad,
  desde cualquier perspectiva política — el objetivo es que la skill sea más
  honesta sobre su no-neutralidad, no que sea menos.

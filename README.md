# pensamiento-critico

> Skill de Claude · Plugin marketplace de Claude Code: `omixam` · Licencia MIT

Skill para Claude que analiza textos argumentativos aplicando el marco de
los **8 elementos del pensamiento** y los **estándares intelectuales universales**
de Richard Paul y Linda Elder, junto con la **detección de falacias lógicas**
y **sesgos cognitivos** relevantes.

El objetivo no es destrozar el texto: es ayudarte a entenderlo mejor y a pensar
por ti mismo.

## Para quién es

Está pensada sobre todo para gente que **escribe o lee opinión con cierta
exigencia**: redactores de newsletters y blogs, profesores que enseñan
argumentación, periodistas que contrastan, alumnos preparando ensayos,
lectores que quieren entender mejor qué les están vendiendo. Pero
funciona para cualquiera que tenga delante un texto argumentativo y
quiera leerlo con más rigor.

Acepta artículos de opinión, ensayos, posts de redes, columnas, discursos,
comunicados, ponencias.

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

El tono es **conversacional y didáctico**, no forense.

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
de referencia. Funciona en las tres superficies donde Claude permite skills
personalizadas, con un mecanismo de instalación distinto en cada una. Las
skills **no se sincronizan entre superficies**: si quieres usarla en claude.ai
y en Claude Code, hay que instalarla en cada una por separado.

### En Claude Code

Tres formas, en orden de comodidad:

#### 1. Como plugin del marketplace omixam (recomendado)

Este repo está empaquetado como **plugin marketplace** de Claude Code. La
forma más cómoda de instalar la skill son dos comandos, **uno por uno** —
pégalos por separado en Claude Code, esperando la salida de cada uno antes
del siguiente.

1. Añade el marketplace:

   ```
   /plugin marketplace add omixam/pensamiento-critico
   ```

   (Si la CLI te pide URL y el shorthand falla, usa la URL completa:
   `https://github.com/omixam/pensamiento-critico.git`.)

2. Instala el plugin:

   ```
   /plugin install pensamiento-critico@omixam
   ```

3. Reinicia Claude Code (o recarga skills, según tu versión) y verifica:
   en una conversación nueva, pega un texto argumentativo y pide
   *"analízalo con pensamiento crítico"*.

#### 2. Como skill de proyecto del repo (web y móvil)

El repo incluye `.claude/skills/pensamiento-critico/` con symlinks al
`SKILL.md` y a las carpetas de referencia. Esto permite que, al abrir el
repo directamente como directorio de trabajo en Claude Code (típicamente
en la web o desde el móvil, donde no hay `~/.claude/skills/` propio), la
skill se cargue automáticamente como skill de proyecto sin necesidad de
instalarla aparte.

#### 3. Instalación manual

Si prefieres instalación manual sin pasar por el marketplace, clona el repo
y copia solo la carpeta de la skill a tu directorio de skills:

```bash
git clone https://github.com/omixam/pensamiento-critico.git /tmp/pensamiento-critico-source
mkdir -p ~/.claude/skills/
cp -R /tmp/pensamiento-critico-source/skills/pensamiento-critico ~/.claude/skills/
```

### En claude.ai (web, desktop, móvil)

Disponible en todos los planes de claude.ai (Free, Pro, Max, Team y
Enterprise), con la ejecución de código activada. Las skills personales son
**individuales a cada usuario**: claude.ai no tiene distribución org-wide,
así que cada miembro de un equipo tiene que subirla por separado en su cuenta.

1. Clona el repo y comprime **solo la carpeta de la skill** (no el repo
   entero — claude.ai espera un ZIP cuya raíz sea la carpeta con el
   `SKILL.md`):

   ```bash
   git clone https://github.com/omixam/pensamiento-critico.git /tmp/pensamiento-critico-source
   cd /tmp/pensamiento-critico-source/skills
   zip -r ~/Desktop/pensamiento-critico.zip pensamiento-critico
   ```

   El ZIP queda en tu escritorio para que lo encuentres fácil al subirlo.

2. En claude.ai, abre **Configuración → Personalizar** (igual ruta en la app
   de Mac, en la web y en móvil). En versiones recientes la antigua sección
   "Skills" de Configuración se trasladó a **Personalizar**, donde se
   gestionan habilidades y conectores en una sola página. Pulsa el botón
   para añadir una habilidad nueva y sube `pensamiento-critico.zip` desde
   el escritorio.
3. Activa el toggle de la habilidad. Asegúrate además de que **Ejecución
   de código** esté habilitada en Configuración (puede aparecer dentro de
   Personalizar o en una pestaña adyacente según versión).
4. Verifica que carga: en una conversación nueva, pega cualquier texto
   argumentativo corto y pide *"analízalo con pensamiento crítico"*. Si ves un
   reporte estructurado con los 8 elementos, está funcionando.

### En Claude API

Las skills personalizadas también pueden usarse vía la Claude API subiéndolas
al endpoint `/v1/skills` con el contenido de `skills/pensamiento-critico/`.
Si vas a integrarla en una aplicación propia, consulta la [guía oficial de
skills en la API](https://platform.claude.com/docs/en/build-with-claude/skills-guide).

## Quick start

Una vez instalada, abre una conversación y pega un texto argumentativo
con la frase *"analízalo con pensamiento crítico"*. Como mini-prueba:

> Hay que prohibir el patinete eléctrico en las ciudades. Cada año mueren
> más peatones por culpa de patinetes que por coches en los nuevos carriles
> bici. Si los políticos no actúan ya, es porque viven de las subvenciones
> de Xiaomi y compañía. Cualquier persona razonable lo ve: o se prohíben
> o seguirán las muertes.

La skill responderá con un reporte estructurado. Resumen del que produce
con este texto:

<details>
<summary>Ver reporte abreviado</summary>

**Síntesis:** el autor defiende la prohibición de patinetes eléctricos
basándose en (1) datos de mortalidad y (2) sospecha de corrupción política.

**Falacias detectadas:**
- *Falsa dicotomía* — "o se prohíben o seguirán las muertes" (omite
  alternativas: regulación, carriles segregados, formación obligatoria).
- *Ad hominem circumstancial* — atribuir la inacción política a corrupción
  ("viven de las subvenciones") sin evidencia, sustituye argumento por
  acusación.
- *Apelación a la opinión popular* — "cualquier persona razonable lo ve"
  desplaza la carga de la prueba al lector.

**Información cuestionable:** la afirmación "mueren más peatones por
patinetes que por coches" no se sostiene con cifras públicas; el autor
no cita fuente.

*[el reporte completo continúa con los 8 elementos, sesgos, test de
simetría ideológica y limitaciones]*

</details>

Para ejemplos completos de reportes en distintos registros (editorial
forense, ensayo constructivo, post breve), ver
[ejemplos de reportes](skills/pensamiento-critico/references/ejemplos-reportes.md).

## Cómo usarla

**Cómo invocarla** — cuatro modos de pasarle el texto:

- **Pegando texto en el chat.** *"Analiza esto con pensamiento crítico: [texto]"*.
- **Adjuntando un archivo.** Funciona con `.md`, `.txt` y `.pdf` (convierte el
  PDF a texto antes de analizar).
- **Pasando un enlace.** *"Pásame este artículo por la skill: [URL]"*. La skill
  intentará leer el contenido; si está tras paywall o requiere login, te lo
  dirá y te pedirá que pegues el texto.
- **Pasando una imagen.** Foto de página de periódico, captura de un post largo,
  diapositiva. La skill transcribe primero y avisa en el reporte de que el
  análisis se hace sobre transcripción propia.

**Prompts útiles:**

- *"¿Qué problemas tiene este argumento?"*
- *"¿Es sólido este razonamiento?"*
- *"Detecta falacias y sesgos en este texto."*
- *"Hazlo en versión breve, dos párrafos."* — la skill ajusta la profundidad.

El reporte se ajusta a la longitud y tipo de texto: un post breve no recibe
el mismo despliegue que un ensayo largo.

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
  aparecen en debate público. Para casos difíciles, ver la
  [bibliografía completa con citas](skills/pensamiento-critico/doc/falacias-bibliografia.md).
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

Ver la [bibliografía completa con citas](skills/pensamiento-critico/doc/falacias-bibliografia.md).

## Licencia

[MIT](LICENSE). El código y la organización de la skill se distribuyen bajo MIT.
La skill **no redistribuye** ninguna de las obras citadas en la bibliografía:
para profundizar, adquiérelas o consúltalas en biblioteca.

## Contribuciones

Issues y PRs bienvenidos. Lo más útil:

- **Casos donde la skill falla**: textos en los que produce un análisis pobre,
  forzado o tendencioso. Pega el texto y describe qué esperabas. Esos casos son
  oro para mejorar los catálogos de `references/`.
- **Falacias mal etiquetadas o ausentes** en el
  [catálogo de falacias](skills/pensamiento-critico/references/falacias-graves.md).
- **Sesgos cognitivos** relevantes que falten en el
  [catálogo de sesgos cognitivos](skills/pensamiento-critico/references/sesgos-cognitivos.md).
- **Mejoras al test de simetría ideológica** o a la sección de no-neutralidad,
  desde cualquier perspectiva política — el objetivo es que la skill sea más
  honesta sobre su no-neutralidad, no que sea menos.

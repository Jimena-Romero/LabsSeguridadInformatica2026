# Laboratorio 01 — Rúbrica de evaluación

**Total:** 100 puntos
**Aprobación:** 60 puntos
**Nivel de promoción práctica (nota 8):** 80 puntos

> **Leé esta rúbrica antes de empezar, no después de entregar.** Tiene una
> penalización específica y tiene causales de rechazo automático. Saber cómo
> se corrige un trabajo antes de hacerlo no es hacer trampa: es lo normal.

---

## Resumen

| Componente | Puntos | Peso |
|---|---:|---:|
| **Parte A** — Análisis del incidente bajo la lente CIA | 35 | 35 % |
| **Parte B** — Implementación y preguntas de análisis | 40 | 40 % |
| **Mini-research** | 20 | 20 % |
| **Proceso** — uso de Git y colaboración | 5 | 5 % |
| **Total** | **100** | |

---

## Parte A — Análisis del incidente (35 puntos)

### A.1 — Cronología (6 pts)

| Puntos | Descriptor |
|---:|---|
| 6 | Cronología precisa, ordenada, dentro del límite de 10 líneas. **Cada hecho con su fuente verificable.** |
| 4 | Cronología correcta pero con fuentes parciales, o con algún hecho sin respaldo. |
| 2 | Relato general del incidente sin precisión temporal, o sin fuentes. |
| 0 | Ausente, o contiene afirmaciones falsas sobre el caso. |

### A.2 — Activo afectado (5 pts)

| Puntos | Descriptor |
|---:|---|
| 5 | Identifica el activo con precisión (qué dato, de quién, en qué sistema) y justifica la priorización cuando hay más de uno. |
| 3 | Identifica el activo pero de forma genérica («los datos de los clientes») sin bajar al detalle. |
| 1 | Confunde el activo con el sistema atacado o con el vector de ataque. |
| 0 | Ausente. |

### A.3 — Matriz CIA (12 pts)

Se evalúa **cada propiedad por separado**: 4 puntos cada una.

| Puntos por propiedad | Descriptor |
|---:|---|
| 4 | Determinación correcta **y** evidencia concreta del incidente que la respalda. |
| 2 | Determinación correcta pero la evidencia es genérica o no demuestra lo afirmado. |
| 1 | Determinación discutible pero con razonamiento explícito y defendible. |
| 0 | Determinación incorrecta, o marcada sin evidencia alguna. |

> **El error más frecuente:** marcar las tres propiedades como violadas porque
> el incidente fue grave. La gravedad no es una propiedad de la tríada. Si
> afirman que se violó la integridad, tienen que mostrar **qué dato fue
> alterado**. Si no pueden, la respuesta correcta es «No», y responder «No»
> con fundamento vale los 4 puntos completos.

### A.4 — Encadenamiento amenaza → vulnerabilidad → impacto (6 pts)

| Puntos | Descriptor |
|---:|---|
| 6 | Los cuatro elementos identificados correctamente y encadenados con precisión terminológica. |
| 4 | Encadenamiento correcto con una imprecisión terminológica menor. |
| 2 | Confunde amenaza con vulnerabilidad, o vulnerabilidad con exploit, o impacto con ataque. |
| 0 | Ausente, o el encadenamiento no se sostiene. |

### A.5 — Dos controles mitigantes (6 pts)

3 puntos por control.

| Puntos por control | Descriptor |
|---:|---|
| 3 | Control específico, correctamente asociado a una propiedad de la tríada, y justificado **contra este caso concreto**. |
| 2 | Control específico y bien asociado, pero la justificación es genérica. |
| 1 | Control demasiado general («tener antivirus», «capacitar al personal») aunque bien asociado. |
| 0 | Ausente, o el control no habría tenido efecto sobre el incidente descrito. |

---

## Parte B — Implementación y análisis (40 puntos)

### B.1 — Subcomando `generar` (8 pts)

| Criterio | Puntos |
|---|---:|
| Recorrido recursivo correcto (entra en subdirectorios) | 2 |
| Rutas relativas y en formato POSIX | 2 |
| Claves ordenadas alfabéticamente | 1 |
| Excluye el propio archivo de manifiesto | 1 |
| Solo archivos regulares; no rompe con directorios | 1 |
| Reutiliza `sha256_archivo()` en vez de reescribir la lectura por bloques | 1 |

### B.2 — Subcomando `verificar` (10 pts)

| Criterio | Puntos |
|---|---:|
| Clasifica correctamente `OK` | 2 |
| Clasifica correctamente `MODIFICADO` | 2 |
| Clasifica correctamente `FALTANTE` | 2 |
| Clasifica correctamente `NUEVO` | 2 |
| Devuelve siempre las cuatro claves, aunque alguna lista quede vacía | 1 |
| Código de salida `1` ante hallazgos, `0` si está todo `OK` | 1 |

> ⚠️ **Penalización de −12 puntos** si `verificar` no detecta la modificación
> de un solo byte sobre un archivo del directorio. Es la prueba obligatoria del
> enunciado y es la razón de ser de toda la Parte B: un verificador de
> integridad que no detecta un byte no es un verificador de integridad.
> **La penalización se aplica sobre el total del laboratorio**, no sobre el
> puntaje de B.2.

### B.3 — Subcomando `avalancha` (5 pts)

| Criterio | Puntos |
|---|---:|
| Calcula la distancia **en bits**, sobre los bytes crudos | 3 |
| Valida que los digests tengan el mismo largo y lanza `ValueError` si no | 1 |
| Devuelve 0 para dos entradas idénticas | 1 |

> Contar diferencias sobre la cadena hexadecimal en vez de sobre los bits da
> **0 en los 3 primeros puntos**, aunque el programa corra sin errores. Es el
> punto central del ejercicio.

### B.4 — Subcomando `mac` (5 pts)

| Criterio | Puntos |
|---|---:|
| HMAC-SHA256 correcto usando el módulo `hmac` de la biblioteca estándar | 2 |
| Verificación con `hmac.compare_digest()` | 2 |
| Distingue los tres estados: no verificado (`None`), válido, inválido | 1 |

> Implementar HMAC a mano, aunque el resultado sea correcto, da **0 en los
> primeros 2 puntos**. La consigna es explícita.
> Comparar con `==` da **0 en los 2 puntos de verificación**, aunque funcione.

### B.5 — Evidencia de ejecución (2 pts)

| Puntos | Descriptor |
|---:|---|
| 2 | Salidas reales pegadas de la terminal para todos los comandos pedidos, incluyendo los códigos de salida. |
| 1 | Evidencia parcial, o transcripta a mano en vez de copiada. |
| 0 | Ausente. |

### B.6 — Preguntas de análisis (10 pts)

2 puntos por pregunta.

| Puntos por pregunta | Descriptor |
|---:|---|
| 2 | Respuesta técnicamente correcta, fundamentada, con desarrollo propio. |
| 1 | Idea correcta pero sin fundamentación, o respuesta de una línea. |
| 0 | Ausente, incorrecta, o es una paráfrasis del enunciado sin contenido. |

---

## Mini-research (20 puntos)

### R.1 — Calidad de las fuentes (6 pts)

| Puntos | Descriptor |
|---:|---|
| 6 | Tres o más fuentes, de las cuales al menos dos son primarias o arbitradas, pertinentes al tema y efectivamente usadas en el texto. |
| 4 | Cumple el mínimo formal pero alguna fuente primaria es tangencial al argumento. |
| 2 | Solo una fuente primaria, o las fuentes están listadas pero no se usan en el cuerpo. |
| 0 | Solo fuentes secundarias, o menos de tres fuentes. |

### R.2 — Análisis propio y sección de tensión (7 pts)

| Puntos | Descriptor |
|---:|---|
| 7 | Toma posición, la defiende con la evidencia citada, e identifica con precisión qué queda sin resolver o dónde falla la solución descrita. |
| 5 | Buen desarrollo pero la sección de tensión es superficial. |
| 3 | Resumen correcto de las fuentes, sin aporte propio. |
| 1 | Paráfrasis de una sola fuente. |
| 0 | Ausente o fuera de tema. |

### R.3 — Citación APA (4 pts)

| Puntos | Descriptor |
|---:|---|
| 4 | Formato correcto, citas en el cuerpo donde corresponde, lista completa, marcación primaria/arbitrada/secundaria. |
| 2 | Formato con errores menores, o citas solo al final sin referencia en el cuerpo. |
| 0 | Sin citación, o citación que no permite localizar la fuente. |

### R.4 — Extensión y estructura (3 pts)

| Puntos | Descriptor |
|---:|---|
| 3 | Entre 800 y 1000 palabras, con estructura clara. |
| 2 | Entre 700-799 o 1001-1100 palabras. |
| 1 | Entre 600-699 o 1101-1300 palabras. |
| 0 | Fuera de ese rango. |

---

## Proceso (5 puntos)

### P.1 — Distribución del trabajo en el historial (2 pts)

| Puntos | Descriptor |
|---:|---|
| 2 | Todos los integrantes tienen commits propios desde sus cuentas, y la distribución es consistente con lo declarado en el informe. |
| 1 | Todos tienen commits pero la distribución es muy despareja sin explicación. |
| 0 | Falta al menos un integrante en el historial. *(Ver también causales de rechazo.)* |

### P.2 — Calidad de los mensajes de commit (1 pt)

| Puntos | Descriptor |
|---:|---|
| 1 | Mensajes descriptivos que permiten seguir la evolución del trabajo. |
| 0 | Mensajes vacíos de contenido (`cambios`, `arreglos`, `.`), o un único commit con todo. |

### P.3 — Pull Request completo (1 pt)

| Puntos | Descriptor |
|---:|---|
| 1 | Plantilla de PR completa, checklist marcado honestamente, comandos de verificación indicados. |
| 0 | Plantilla sin completar o borrada. |

### P.4 — Aislamiento del directorio de grupo (1 pt)

| Puntos | Descriptor |
|---:|---|
| 1 | Todos los cambios están dentro de `entregas/lab01/grupoXX/`. Nada de `labs/`, de la raíz ni de otros grupos fue modificado. |
| 0 | Se modificaron archivos fuera del directorio del grupo. |

---

## Penalizaciones

| Penalización | Puntos |
|---|---:|
| `verificar` no detecta la modificación de un solo byte | **−12** |
| Entrega fuera de la estructura de directorios pedida | −3 |
| `data/muestra/` o `manifest.sha256` versionados en el repositorio | −2 |
| `INTEGRANTES.md` con datos personales que exceden lo pedido (DNI, teléfono, dirección, correo) | −2 |

Las penalizaciones se aplican sobre el total y pueden acumularse. El puntaje
final no baja de 0.

---

## Causales de rechazo automático

Un trabajo con cualquiera de estas condiciones **no se corrige** y se devuelve
al grupo. Se puede rehacer según el régimen de recuperación de la cátedra.

1. **Commits de una sola cuenta.** El laboratorio es grupal. Un historial con
   un solo autor no acredita trabajo grupal, independientemente de lo que diga
   el informe.

2. **Falta la declaración de uso de asistentes de IA.** Está en el informe y
   en el mini-research. No está prohibido usarlos; está prohibido no
   declararlo. Una declaración honesta no baja la nota.

3. **Cita inexistente o no localizable.** Una referencia que no se puede
   encontrar invalida el trabajo de investigación completo. Verifiquen cada
   fuente entrando a ella, especialmente si usaron un asistente de IA para
   buscarla: fabrican citas con formato impecable y contenido inexistente.

4. **Código de otro grupo sin atribución.** El repositorio es público y las
   entregas son visibles. Mirar cómo resolvió otro grupo está bien y es parte
   de aprender. Copiar sin citar es plagio. Si se inspiraron en la solución de
   otro grupo, cítenlo como citarían cualquier otra fuente — eso no penaliza.

---

## Escala de calificación

| Puntos | Nota | Condición |
|---:|---:|---|
| 0 – 59 | 1 – 5 | No aprobado |
| 60 – 69 | 6 | Aprobado |
| 70 – 79 | 7 | Aprobado |
| 80 – 89 | 8 | Aprobado — nivel de promoción práctica |
| 90 – 100 | 9 – 10 | Aprobado — destacado |

---

## Consulta de la corrección

La devolución se publica como comentarios en el Pull Request. Si algo del
puntaje no queda claro, respondé en el mismo hilo: la discusión sobre la
corrección también forma parte del proceso.

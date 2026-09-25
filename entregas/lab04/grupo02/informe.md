# Informe — Laboratorio 04 · Marcos normativos y gestión de la seguridad

**Grupo:** 02

**Integrantes:**

| Nombre y apellido | Legajo | Usuario de GitHub |
|---|---|---|
| Romero Jimena Soledad | 15377 | @Jimena-Romero |
| Milanesio Hebe Del Lourdes | 15343 | @hebemilanesio1 |
| Toranzo Juan Cruz | 15308 | @JuanToranzo |
| Torres Damaris | 14563 | @damaris412 |

---

## 0. Declaración de uso de IA

Se utilizó Gemini (Google) como asistente conversacional para:
- Guiar la estructuración del flujo de trabajo en Git (gestión de ramas `lab04-grupo02` y sincronización remota).
- Asistir en la implementación de las funciones cuantitativas de `src/riesgo.py` (`ale`, `roi_control`, `priorizar`).
- Estructurar el archivo de datos `riesgos.json` adaptado al escenario de PhantomCorp.
- Colaborar en la redacción técnica y análisis del informe.

Todo el código fue probado de manera local ejecutando `src/verify.py` y los resultados del script fueron validados por el equipo.

---

## 1. Parte A — Marco aplicado

### A.1 — Marco elegido y justificación
*(A COMPLETAR POR INTEGRANTE 2)*

### A.2 — Mapeo de cinco debilidades a controles/funciones del marco
*(A COMPLETAR POR INTEGRANTE 2)*

### A.3 — Respuestas al riesgo elegidas (mitigar/transferir/aceptar/evitar) con justificación
*(A COMPLETAR POR INTEGRANTE 3)*

---

## 2. Parte B — Riesgo cuantitativo

### B.1 — El ranking por ALE. ¿Coincide con tu intuición? ¿Dónde no?

Se ejecutó el script `src/riesgo.py priorizar --archivo riesgos.json` utilizando los datos cuantitativos del escenario PhantomCorp. El resultado obtenido fue:

```text
  ALE ($)     Riesgo / Incidente
  -----------------------------------------------------------------------------------
  30000.00    Filtración de datos de tarjetas/DNI por Servidor Web público
  20000.00    Acceso no autorizado por falta de MFA en empleados remotos
  15000.00    Falta de política de contraseñas (fuerza bruta / credential stuffing)
   3000.00    Pérdida de backups físicos por daño o robo en la oficina
```
¿Dónde coincide con la intuición? Coincide ampliamente al situar la filtración de datos en el servidor web público ($30.000,00) y el acceso no autorizado por falta de MFA ($20.000,00) en el tope de las prioridades. Dado que son activos expuestos hacia internet con información crítica de clientes (tarjetas, DNI), la intuición sugiere atacarlos primero.

¿Dónde NO coincide con la intuición? A primera vista, la pérdida de backups en la oficina suena como una catástrofe operativa grave que requeriría atención urgente. Sin embargo, al calcular cuantitativamente con el ARO (frecuencia estimada de 0.2 veces/año), su ALE resulta ser el más bajo de la lista ($3.000,00). Por el contrario, la falta de política de contraseñas parece un problema menor a nivel intuitivo, pero su alta probabilidad de ocurrencia continua (ARO: 0.6) genera un costo esperado anual considerablemente mayor ($15.000,00).

### B.2 — Para el riesgo #1, proponé un control, estimá su costo y el ALE resultante, y calculá el ROI. ¿Conviene?
*(A COMPLETAR POR INTEGRANTE 4)*

### B.3 — Un riesgo donde la respuesta correcta sea aceptar o transferir (no mitigar), y por qué
*(A COMPLETAR POR INTEGRANTE 4)*
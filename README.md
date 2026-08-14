# Laboratorios — Seguridad Informática 2026

Repositorio de trabajos prácticos de laboratorio de la asignatura **Seguridad
Informática**, carrera de Ingeniería en Sistemas de Información.

| | |
|---|---|
| **Institución** | UTN — Facultad Regional Villa María |
| **Asignatura** | Seguridad Informática (Quinto nivel) |
| **Docente** | Ing. Fernando Boiero — Prof. Adj. Int. Simple |
| **Ciclo lectivo** | 2026 |
| **Carga horaria** | 96 h totales · 6 h semanales · 16 semanas |

---

## Cómo se trabaja

Los laboratorios se entregan mediante **fork + Pull Request** contra este
repositorio. El procedimiento completo, paso a paso, está en
[`CONTRIBUTING.md`](CONTRIBUTING.md). **Leelo antes de tocar nada.**

Reglas que valen para todos los labs:

1. **Grupos de 4 a 5 integrantes.** El grupo se mantiene durante todo el
   cuatrimestre salvo autorización expresa del docente.
2. Cada grupo entrega dentro de su propio directorio:
   `entregas/labNN/grupoXX/`. **Nunca** modifiquen archivos de otro grupo ni
   del enunciado.
3. El historial de commits es parte de la evaluación. Se espera ver
   **contribuciones de todos los integrantes** desde sus propias cuentas de
   GitHub.
4. Todo uso de asistentes de IA debe declararse. No está prohibido: está
   **obligatoriamente documentado**. Ver la sección correspondiente en cada
   plantilla de entregable.

> **Advertencia legal.** Todo el material de esta asignatura se practica sobre
> entornos propios, entornos de laboratorio provistos por la cátedra o
> aplicaciones deliberadamente vulnerables de uso público. Ejecutar cualquier
> técnica de las que se estudian contra sistemas de terceros sin autorización
> escrita constituye delito en la República Argentina (Ley 26.388). Ver
> [`CONTRIBUTING.md`](CONTRIBUTING.md) § Uso responsable.

---

## Índice de laboratorios

| Lab | Unidad | Tema | Estado |
|---|---|---|---|
| [01](labs/lab01-introduccion/) | 1 | Introducción: la tríada CIA, historia de la seguridad informática e integridad con funciones de hash | **Publicado** |
| 02 | 2 | Criptografía | Por publicar |
| 03 | 3 | *Título según programa analítico* | Por publicar |
| 04 | 4 | Marcos normativos y gestión de la seguridad | Por publicar |
| 05 | 5 | Vulnerabilidades: identificación, clasificación y explotación | Por publicar |
| 06 | 6 | *Título según programa analítico* | Por publicar |
| 07 | 7 | *Título según programa analítico* | Por publicar |
| 08 | 8 | *Título según programa analítico* | Por publicar |
| 09 | 9 | *Título según programa analítico* | Por publicar |

Cada laboratorio se habilita al inicio de la unidad correspondiente. Los
títulos marcados *«según programa analítico»* se completan al publicarse el
enunciado.

---

## Requisitos técnicos

- **Python 3.10 o superior.** Los laboratorios que involucran código usan
  exclusivamente la **biblioteca estándar** salvo indicación contraria en el
  enunciado. No hay que instalar dependencias.
- **Git** y una cuenta de **GitHub** por integrante.
- Un editor de texto o IDE. Cualquiera sirve.

Verificá tu versión de Python:

```bash
python3 --version
```

---

## Estructura del repositorio

```
LabsSeguridadInformatica2026/
├── CONTRIBUTING.md          # Flujo de trabajo: fork, rama, PR
├── labs/                    # Enunciados y esqueletos de código (NO modificar)
│   └── lab01-introduccion/
│       ├── README.md        # Enunciado
│       ├── src/             # Esqueleto de código con TODO a completar
│       ├── data/            # Generador de datos de muestra
│       └── docs/            # Plantilla de entregable, research y rúbrica
└── entregas/                # Acá va el trabajo de cada grupo
    └── lab01/
        └── grupo01/         # Lo crea el grupo
```

---

## Contacto

Consultas sobre los enunciados: por el canal de la cátedra o abriendo un
**Issue** en este repositorio. Los Issues son públicos y la respuesta le sirve
a todos — usalos.

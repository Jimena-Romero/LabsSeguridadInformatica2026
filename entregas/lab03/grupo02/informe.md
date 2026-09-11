# Informe — Laboratorio 03 · Autenticación

**Grupo:** 02

**Integrantes:**

| Nombre y apellido | Legajo | Usuario de GitHub |
|---|---|---|
| Romero Jimena Soledad | 15377 | @Jimena-Romero |
| Milanesio Hebe Del Lourdes | 15343 | @hebemilanesio1 |
| Toranzo Juan Cruz | 15308 | @JuanToranzo |
| Torres Damaris | 14563 | @damaris412 |

## 0. Declaración de uso de IA
Para este trabajo utilizamos Claude (Anthropic) como herramienta de apoyo, principalmente para:

- **Parte A:** pedimos ayuda para investigar y estructurar el análisis del
  caso de brecha asignado a nuestro grupo (Credential stuffing — 23andMe,
  2023), incluyendo búsqueda de fuentes.
- **Soporte de git/terminal:** consultamos comandos de Git (creación de rama,
  commits, push) y resolución de errores de sintaxis entre PowerShell y Git
  Bash durante la preparación del entorno de entrega.

Todo el código generado fue revisado, ejecutado y verificado por el equipo
antes de incorporarlo a la entrega. Las respuestas conceptuales (por qué salt
por usuario, por qué iteraciones, por qué el 2FA frena credential stuffing,
qué no protege el TOTP) fueron redactadas por el equipo con apoyo de la IA
para organizar y revisar la claridad de la explicación.

## 1. Parte A — Análisis de la brecha (caso, falla, explotación, lo correcto; con fuentes)
**Caso:** Credential stuffing — 23andMe (2023)

### Qué se guardó/comparó mal
23andMe no sufrió una intrusión directa a sus sistemas: entre abril y septiembre
de 2023, atacantes probaron de forma automatizada pares usuario/contraseña
filtrados en *otras* brechas contra el login de 23andMe [1][2]. Consiguieron
acceso directo a unas 14.000 cuentas simplemente porque muchos usuarios
reutilizaban contraseñas ya expuestas en otros sitios [1]. A diferencia de los
casos de LinkedIn o RockYou, acá la falla no fue un algoritmo de hash roto ni
una comparación insegura — fue una falla de **diseño de control de acceso**: no
se exigía un segundo factor por defecto y no había límites efectivos a los
intentos de login masivos [5].

### Cómo se explotó

### La forma correcta

### Por qué el 2FA corta este ataque específicamente
A diferencia de los casos que rompen el *almacenamiento* de contraseñas, acá la
contraseña del usuario podía ser perfectamente robusta — el problema es que ya
estaba filtrada por *otro* servicio. El 2FA no depende de que la contraseña sea
secreta; depende de un factor adicional (algo que tenés) que el atacante no
posee aunque tenga la lista completa de combos usuario/contraseña.

### Fuentes
1. Enzoic — *Lessons from the 23andMe Breach and NIST SP 800-63B*.
   https://www.enzoic.com/blog/23andme-breach/
2. Security.org — *23andMe Data Breach: What Was Exposed, Who Was Affected*.
   https://www.security.org/identity-theft/breach/23andme/
3. Breachsense — *23andMe Data Breach: How Credential Stuffing Exposed Genetic
   Data*. https://www.breachsense.com/blog/23andme-data-breach-case-study/
4. IT World Canada — *Privacy commissioners slam 23andMe for huge data theft
   from credential stuffing*.
   https://solomonh.substack.com/p/privacy-commissioners-slam-23andme
5. Wikipedia — *Credential stuffing*.
   https://en.wikipedia.org/wiki/Credential_stuffing

## 2. Parte B.1 — Contraseñas (por qué salt por usuario, por qué muchas iteraciones)
## 3. Parte B.2 — TOTP (por qué frena el robo de contraseña; qué NO protege)
## 4. Bitácora de comandos

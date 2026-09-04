# Informe — Laboratorio 02 · Criptografía

**Grupo:** 02 · **Integrantes:** *(vos — usuario GitHub), (tu compañera — usuario GitHub)* · **Fecha:** 2026-09-04

## 0. Declaración de uso de IA
*(acá ponen si usaron IA y cómo, según pida el enunciado)*

## 1. Parte A — Análisis de la falla
**Caso:** Sony PS3 (ECDSA) — reutilización del nonce k al firmar

**A.1 — Qué prometía**

La PS3 implementaba una cadena de confianza (chain of trust) con ejecutables firmados y un hipervisor, cuyo objetivo era que la consola sólo ejecutara código autorizado por Sony. El esquema de firma usado era ECDSA (Elliptic Curve Digital Signature Algorithm): la promesa criptográfica era autenticidad e integridad, que sólo Sony pudiera producir código que la consola aceptara como legítimo, y que nadie pudiera falsificar una firma válida sin conocer la clave privada de Sony.

**A.2 — El mal uso**

El algoritmo ECDSA no estaba roto sino que presentaba un fallo en la implementación. Cada firma ECDSA requiere un número aleatorio k (el "nonce") que debe ser distinto en cada firma. Sony reutilizó siempre el mismo valor de k para firmar, en vez de generarlo aleatoriamente cada vez. La falla crítica fue que un parámetro que debía ser aleatorizado en cada generación de clave no se aleatorizó en absoluto, algo que la propia documentación de ECDSA advierte explícitamente.
Es crucial elegir un k distinto para cada firma, de lo contrario la ecuación puede resolverse para obtener la clave privada. La reutilización de nonce en ECDSA revela la clave privada directamente porque dos firmas que comparten el mismo valor r exponen k algebraicamente; no se necesita ninguna suposición de dificultad computacional, es álgebra pura que se completa en microsegundos. Esto le permitió a GeoHot (George Hotz) publicar la clave raíz de la PS3, que puede usarse para firmar cualquier código y hacerlo aparecer como firmado por Sony, lo que rompió por completo el control de Sony sobre qué software podía ejecutarse en la consola.

**A.3 — Propiedad comprometida y cómo se explotó**

La propiedad que se rompió fue la **autenticidad** del firmware (y, como consecuencia, su integridad). ECDSA le permite a Sony firmar cada firmware/software oficial con su clave privada, de modo que la consola pueda verificar —usando la clave pública de Sony— que ese código efectivamente proviene de Sony y no fue modificado. Si la firma se compromete, deja de haber forma de distinguir código oficial de código falsificado: cualquiera que consiga la clave privada puede firmar su propio software y la PS3 lo va a aceptar como legítimo.

El mecanismo de la explotación fue el siguiente:

1. ECDSA exige que en cada firma se use un número aleatorio distinto llamado *nonce* (k), generado de forma impredecible.
2. Sony implementó mal el algoritmo y usaba **siempre el mismo valor de k** para firmar todos los mensajes, en lugar de generar uno nuevo cada vez.
3. El grupo fail0verflow, en 2010, analizó varias firmas oficiales de Sony y detectó que provenían del mismo k.
4. Con dos firmas distintas (de dos mensajes distintos) generadas con el mismo k, es posible plantear un sistema de ecuaciones y despejar algebraicamente la clave privada de Sony.
5. Con la clave privada obtenida, fail0verflow pudo firmar cualquier código propio (homebrew, jailbreaks, firmwares modificados) y la PS3 lo aceptaba como si fuera software oficial de Sony.

La idea central es que reutilizar el nonce en ECDSA dos veces equivale, matemáticamente, a exponer la clave privada. El algoritmo ECDSA en sí no fue roto ni tiene una debilidad matemática: lo que falló fue la implementación de Sony, que violó un requisito no negociable del esquema de firma.

**Fuente:** fail0verflow, "Console Hacking 2010: PS3 Epic Fail" (27C3, 2010).

**A.4 — Forma correcta**

El nonce k debe generarse de manera aleatoria y criptográficamente segura (usando un CSPRNG) en cada operación de firma, sin reutilizarlo nunca ni derivarlo de forma predecible. Como alternativa más robusta, se puede usar ECDSA determinístico (RFC 6979), que deriva k de manera segura y reproducible a partir del mensaje y la clave privada, eliminando la dependencia de un generador aleatorio externo y evitando así este tipo de fallo por implementación.

## 2. Parte B.1 — Romper el XOR
...

## 3. Parte B.2 — Autenticación
...

## 4. Bitácora


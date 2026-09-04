# Informe — Laboratorio 02 · Criptografía

**Grupo:** 02 · **Integrantes:** *(vos — usuario GitHub), (tu compañera — usuario GitHub)* · **Fecha:** 2026-09-04

## 0. Declaración de uso de IA
*(acá ponen si usaron IA y cómo, según pida el enunciado)*

## 1. Parte A — Análisis de la falla
**Caso:** Sony PS3 (ECDSA) — reutilización del nonce k al firmar

**A.1 — Qué prometía:** *(tu compañera)*
**A.2 — El mal uso:** *(tu compañera)*

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


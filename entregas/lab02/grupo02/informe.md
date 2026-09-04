# Informe — Laboratorio 02 · Criptografía

> Copiala a `entregas/lab02/grupoXX/informe.md`. Borrá las notas en cursiva.

**Grupo:** XX · **Integrantes:** *(nombre — usuario GitHub)* · **Fecha:**

## 0. Declaración de uso de IA

## 1. Parte A — Análisis de la falla
**Caso:** *(el asignado)*
**A.1 — Qué prometía · A.2 — El mal uso · A.3 — Propiedad rota y explotación · A.4 — Lo correcto**

## A1 - ¿Que prometía?
La PS3 implementaba una cadena de confianza (chain of trust) con ejecutables firmados y un hipervisor, cuyo objetivo era que la consola sólo ejecutara código autorizado por Sony. El esquema de firma usado era ECDSA (Elliptic Curve Digital Signature Algorithm): la promesa criptográfica era autenticidad e integridad, que sólo Sony pudiera producir código que la consola aceptara como legítimo, y que nadie pudiera falsificar una firma válida sin conocer la clave privada de Sony.

## A2 - El mal uso
El algoritmo ECDSA no estaba roto sino que presentaba un fallo en la implementación. Cada firma ECDSA requiere un número aleatorio k (el "nonce") que debe ser distinto en cada firma. Sony reutilizó siempre el mismo valor de k para firmar, en vez de generarlo aleatoriamente cada vez. La falla crítica fue que un parámetro que debía ser aleatorizado en cada generación de clave no se aleatorizó en absoluto, algo que la propia documentación de ECDSA advierte explícitamente.
Es crucial elegir un k distinto para cada firma, de lo contrario la ecuación puede resolverse para obtener la clave privada. La reutilización de nonce en ECDSA revela la clave privada directamente porque dos firmas que comparten el mismo valor r exponen k algebraicamente; no se necesita ninguna suposición de dificultad computacional, es álgebra pura que se completa en microsegundos. Esto le permitió a GeoHot (George Hotz) publicar la clave raíz de la PS3. Cuatro días después, el hacker GeoHot publicó la clave raíz de la PS3, que puede usarse para firmar cualquier código y hacerlo aparecer como firmado por Sony, lo que rompió por completo el control de Sony sobre qué software podía ejecutarse en la consola.

## 2. Parte B.1 — Romper el XOR
*(clave hallada, mensaje en claro, y por qué el cifrado clásico falla)*

## 3. Parte B.2 — Autenticación
**B.2.1 length-extension · B.2.2 cómo lo resuelve HMAC · B.2.3 tiempo constante**

## 4. Bitácora
```bash
# python3 src/cripto.py romper --hex ...
```

# Simulador de la jerarquía de Chomsky

Aplicación gráfica que visualiza, simula y valida el comportamiento de los cuatro modelos de cómputo de la jerarquía de Chomsky:

| Nivel | Modelo | Lenguaje de ejemplo |
|---|---|---|
| 3 | Autómata finito determinista | Cadenas que terminan en `ab` |
| 2 | Autómata de pila | aⁿbⁿ, paréntesis balanceados |
| 1 | Autómata linealmente acotado | aⁿbⁿcⁿ |
| 0 | Máquina de Turing | Suma unaria `1ᵐ+1ⁿ`, aⁿbⁿ sin cota |

## Requisitos

Un navegador moderno (Chrome, Firefox, Edge o Safari). No necesita instalación ni librerías externas.

## Ejecución

Opción 1 (directa): abre `index.html` con doble clic.

Opción 2 (servidor local, opcional):

```bash
cd chomsky-simulador
python3 -m http.server 8000
```

Luego visita `http://localhost:8000`.

## Uso

1. Elige un módulo en la barra superior.
2. Elige un **preajuste** o edita las **reglas de transición**, el estado inicial y los estados finales.
3. Escribe una cadena o pulsa uno de los **ejemplos** (botones redondos).
4. Usa **Ejecutar** (resultado final), **Paso** (un paso a la vez), **Automático** o **Reiniciar**.

### Formato de reglas

- **Nivel 3:** `estado símbolo estado_siguiente`, por ejemplo `q0 a q1`.
- **Nivel 2:** `estado entrada tope estado_siguiente símbolos_a_apilar`, por ejemplo `q0 a Z q0 AZ`. Usa `-` para ε. El primer símbolo apilado queda arriba.
- **Niveles 1 y 0:** `estado símbolo nuevo_estado escritura movimiento`, por ejemplo `q0 a q1 X R`. Movimientos: `L`, `R`, `S`. El estado de aceptación es `qacc`. El blanco es `_`.

## Cadenas de prueba

**Nivel 3 (terminan en `ab`):** `aab`, `bab`, `ababab` (aceptan); `abba`, `ba` (rechazan).
**Nivel 3 (número par de `a`):** `aabb`, `abab`, `bbb` (aceptan); `aba`, `abb` (rechazan).
**Nivel 2 (aⁿbⁿ):** `aaabbb`, `ab`, `""` (aceptan); `aab`, `ba` (rechazan).
**Nivel 2 (paréntesis):** `(())()`, `()()` (aceptan); `(()`, `())` (rechazan).
**Nivel 1 (aⁿbⁿcⁿ):** `aabbcc`, `abc` (aceptan); `aabbc`, `abcc` (rechazan).
**Nivel 0 (suma unaria):** `11+111` (resultado `11111`), `1+1` (resultado `11`), `111+11`.
**Nivel 0 (aⁿbⁿ sin cota):** `aabb`, `ab` (aceptan); `aab` (rechaza).

## Estructura del repositorio

```
chomsky-simulador/
├── index.html   # Aplicación completa (HTML, CSS y JavaScript)
└── README.md    # Este manual
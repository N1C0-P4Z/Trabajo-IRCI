# Arquitectura de Computadoras - Soluciones

## Estructura del Proyecto

```
Coba/
├── bibliografia/          # Material de referencia y apuntes
│   ├── pac_a.md          # Apéndice A del libro (Lógica Digital)
│   ├── pac_a.pdf         # PDF del Apéndice A
│   ├── oc_ab.md          # Otro material bibliográfico
│   └── ...               # Otros PDFs de referencia
│
├── ejercicios/           # Soluciones de ejercicios
│   ├── p1_numeros.md     # Práctica 1: Representación numérica
│   ├── p2_digital.md     # Práctica 2: Lógica Digital (enunciados)
│   ├── EJERCICIO_4.md    # Soluciones ejercicio 4 (MEF) - ver detalle abajo
│   ├── ejercicio_3_minimizacion.md  # Soluciones ejercicio 3
│   ├── practica_p1_p2.md # Soluciones combinadas
│   ├── Resumen coba 1er prueba.md   # Resumen para estudiar
│   └── clases coba.md    # Notas de clase
│
└── proyecto_latex/       # Proyecto LaTeX limpio
    ├── main.tex         # Documento principal
    ├── .gitignore       # Archivos a ignorar
    └── README.md        # Este archivo
```

## Cómo compilar el proyecto LaTeX

### Opción 1: Usando pdflatex
```bash
cd proyecto_latex
pdflatex main.tex
pdflatex main.tex  # Compilar dos veces para referencias
```

### Opción 2: Usando latexmk (recomendado)
```bash
cd proyecto_latex
latexmk -pdf main.tex
```

## Estructura del documento LaTeX

El archivo `main.tex` está organizado en:

- **Sección 1**: Introducción
- **Sección 2**: Práctica 1 — Representación de la Información
  - Conversión de bases numéricas (ej. 1.1 a 1.6)
  - Números enteros signados (ej. 2.1 a 2.6)
  - Punto flotante IEEE 754 (ej. 3.1 a 3.14)
  - Aritmética en C2 de 5 bits (ej. 4.1 a 4.11)
- **Sección 3**: Práctica 2 — Lógica Digital
  - Tablas de verdad (ej. 1.1 a 1.4)
  - Formas canónicas (ej. 2.1 a 2.4)
  - Minimización (ej. 3.1 a 3.10, detallados con grupos coloreados)
  - **Máquinas de Estados Finitos** (ej. 4.1, 4.2, 4.4, 4.5)

## Máquinas de Estados Finitos — Estructura de Ejercicios

Cada ejercicio del apartado de Máquinas de Estados Finitos (Práctica 2) sigue la siguiente estructura:

### Estructura General de un Ejercicio MEF

```
Subsubsection: Ejercicio 4.X --- [Nombre del ejercicio]

1. ENUNCIADO
   - Descripción clara del problema
   - Especificación de entradas/salidas
   - Comportamiento esperado

2. TABLA DE VERDAD
   - Columnas: estado anterior (Q_a), entradas, estado próximo (Q_p), salida(s)
   - Todas las combinaciones posibles

3. FUNCIÓN(ES) MINIMIZADA(S)
   - Expresión algebraica simplificada
   - Formato: Z = ... (o Z0 = ..., Z1 = ... si hay múltiples salidas)

4. MÁQUINA REALIZADA EN CIRCUITVERSE
   - Imagen del circuito: \includegraphics[width=0.9\textwidth]{img/circuito_4_X.png}
   - Espacio reservado para captura
```

---

### Ejercicio 4.1 — Paridad de bits por X e Y

**Enunciado:** Realizar una máquina que posea entradas X e Y y una salida Z. El sistema 
debe calcular la paridad de los bits entrantes por X e Y. La salida Z será 1 si la 
cantidad total de bits en uno es impar, 0 en caso contrario.

**Tabla de Verdad:**
| Q_a | X | Y | Q_p | Z |
|-----|---|---|-----|---|
| 0   | 0 | 0 |  0  | 0 |
| 0   | 0 | 1 |  1  | 1 |
| 0   | 1 | 0 |  1  | 1 |
| 0   | 1 | 1 |  0  | 0 |
| 1   | 0 | 0 |  1  | 1 |
| 1   | 0 | 1 |  0  | 0 |
| 1   | 1 | 0 |  0  | 0 |
| 1   | 1 | 1 |  1  | 1 |

**Función minimizada:** `Z = X ⊕ Y ⊕ Q_a` (XOR de las tres variables)

**Próximo estado:** `Q_p = X ⊕ Y ⊕ Q_a` (igual que la salida Z)

**Imagen:** `img/circuito_4_1.png`

---

### Ejercicio 4.2 — Paridad con habilitación C

**Enunciado:** Realizar una máquina que posea entradas C, X e Y y una salida Z. El 
sistema debe calcular la paridad de los bits entrantes por X e Y. La salida Z será 
1 si la cantidad total de bits en uno es impar **y C está en 1**, 0 en caso contrario.

**Tabla de Verdad:**
| Q_a | C | X | Y | Q_p | Z |
|-----|---|---|---|-----|---|
|  X  | 0 | X | X |  0  | 0 |
|  0  | 1 | 0 | 0 |  0  | 0 |
|  0  | 1 | 0 | 1 |  1  | 1 |
|  0  | 1 | 1 | 0 |  1  | 1 |
|  0  | 1 | 1 | 1 |  0  | 0 |
|  1  | 1 | 0 | 0 |  1  | 1 |
|  1  | 1 | 0 | 1 |  0  | 0 |
|  1  | 1 | 1 | 0 |  0  | 0 |
|  1  | 1 | 1 | 1 |  1  | 1 |

**Función minimizada:** `Z = C · (X ⊕ Y ⊕ Q_a)`

**Próximo estado:** `Q_p = C · (X ⊕ Y ⊕ Q_a)` si C=1; Q_p = 0 si C=0 (reset)

**Imagen:** `img/circuito_4_2.png`

---

### Ejercicio 4.3 — Detector de paridad con habilitación condicional

**Estado:** ✓ INCLUIDO EN EL DOCUMENTO LaTeX

**Enunciado:** Realizar una máquina que posea entradas E (estado anterior), C, X e Y y salidas E+1 y Z. 
El sistema debe detectar la paridad de X e Y cuando E está en 1.

**Tabla de Verdad Simplificada:**
| E | C | X | Y | E+1 | Z |
|---|---|---|---|-----|---|
| 0 | X | X | X | C   | 0 |
| 1 | 0 | 0 | 1 | 0   | 1 |
| 1 | 0 | 1 | 0 | 0   | 1 |
| 1 | 1 | 0 | 1 | 1   | 1 |
| 1 | 1 | 1 | 0 | 1   | 1 |

**Función minimizada:** `Z = E · (X ⊕ Y)`

**Imagen:** `img/circuito_4_3.png`

---

### Ejercicio 4.4 — Relación entre valores anteriores de X e Y

**Enunciado:** Realizar una máquina que posea entradas X e Y y dos salidas Z0 y Z1. 
El sistema debe monitorear la relación entre los valores anteriores de las entradas 
X e Y según la siguiente tabla de salida:

**Tabla de Relación (salidas en función de estados anteriores):**
| X_ant | Y_ant | Z_0 | Z_1 |
|-------|-------|-----|-----|
|   0   |   0   |  1  |  1  |
|   0   |   1   |  0  |  1  |
|   1   |   0   |  1  |  0  |
|   1   |   1   |  1  |  1  |

**Funciones minimizadas:**
- `Z_0 = Y_ant' + X_ant`
- `Z_1 = X_ant' + Y_ant`

**Próximo estado:** `Q_x_next = X`, `Q_y_next = Y` (almacenar entrada actual)

**Imagen:** `img/circuito_4_4.png`

---

### Ejercicio 4.5 — Comparación de número binario XY anterior vs actual

**Enunciado:** Realizar una máquina que posea entradas X e Y y una salida Z. El sistema 
debe monitorear la relación entre el número binario formado XY anterior y el actual. 
La salida Z será:
- Z = 0 si XY_ant ≤ XY_act
- Z = 1 si XY_ant > XY_act

**Tabla de Verdad:**
| X_ant | Y_ant | X | Y | Z |
|-------|-------|---|---|---|
|   0   |   0   | 0 | 0 | 0 |
|   0   |   0   | 0 | 1 | 0 |
|   0   |   0   | 1 | 0 | 0 |
|   0   |   0   | 1 | 1 | 0 |
|   0   |   1   | 0 | 0 | 1 |
|   0   |   1   | 0 | 1 | 0 |
|   0   |   1   | 1 | 0 | 0 |
|   0   |   1   | 1 | 1 | 0 |
|   1   |   0   | 0 | 0 | 1 |
|   1   |   0   | 0 | 1 | 1 |
|   1   |   0   | 1 | 0 | 0 |
|   1   |   0   | 1 | 1 | 0 |
|   1   |   1   | 0 | 0 | 1 |
|   1   |   1   | 0 | 1 | 1 |
|   1   |   1   | 1 | 0 | 1 |
|   1   |   1   | 1 | 1 | 0 |

**Minterms donde Z=1:** {4, 8, 9, 12, 13, 14}

**Función minimizada:**
```
Z = X_ant·X' + Y_ant·X'·Y' + X_ant·Y_ant·Y'
```

O equivalentemente:
```
Z = Xant·X' + Yant·X'·Y' + Xant·Yant·Y'
```

**Próximo estado:** `Q_x_next = X`, `Q_y_next = Y` (almacenar entrada actual)

**Imagen:** `img/circuito_4_5.png`

---

### Ejercicio 4.6 — Contador binario creciente

**Estado:** ✓ INCLUIDO EN EL DOCUMENTO LaTeX

**Enunciado:** Realizar una máquina que posea entrada UP y dos salidas Z1 y Z0. El sistema 
debe comportarse como un contador binario de 2 bits que incrementa cuando UP=1.

**Tabla de Verdad:**
| UP | Q1 | Q0 | Q1+ | Q0+ | Z1 | Z0 |
|----|----|----|-----|-----|----|----|
| 0  | 0  | 0  | 0   | 0   | 0  | 0  |
| 0  | 0  | 1  | 0   | 1   | 0  | 1  |
| 0  | 1  | 0  | 1   | 0   | 1  | 0  |
| 0  | 1  | 1  | 1   | 1   | 1  | 1  |
| 1  | 0  | 0  | 0   | 1   | 0  | 0  |
| 1  | 0  | 1  | 1   | 0   | 0  | 1  |
| 1  | 1  | 0  | 1   | 1   | 1  | 0  |
| 1  | 1  | 1  | 0   | 0   | 1  | 1  |

**Funciones minimizadas:**
- `Q0+ = Q0 ⊕ UP`
- `Q1+ = Q1 ⊕ (Q0 · UP)`

**Imagen:** `img/circuito_4_6.png`

---

### Ejercicio 4.7 — Contador binario creciente con reset

**Estado:** ✓ INCLUIDO EN EL DOCUMENTO LaTeX

**Enunciado:** Contador binario con entrada RESET que lo lleva a 00 cuando RESET=1.

**Funciones minimizadas:**
- `Q0+ = RESET' · (Q0 ⊕ UP)`
- `Q1+ = RESET' · (Q1 ⊕ (Q0 · UP))`

**Imagen:** `img/circuito_4_7.png`

---

### Ejercicio 4.8 — Contador binario bidireccional con reset

**Estado:** ✓ INCLUIDO EN EL DOCUMENTO LaTeX (tabla con \resizebox para mejor legibilidad)

**Enunciado:** Contador de 2 bits que puede incrementar (UP) o decrementar (DN), con reset (R).

**Funciones minimizadas:**
- `Q0+ = R' · (Q0 ⊕ UP ⊕ DN)`
- `Q1+ = R' · (Q1 ⊕ (UP·DN'·Q0 + DN·UP'·Q0'))`

**Características:**
- R=1: Reset a 00
- UP=1, DN=0: Incremento
- UP=0, DN=1: Decremento
- UP=DN: Hold (mantiene estado)

**Imagen:** `img/circuito_4_8.png`

---

### Ejercicio 4.9 — Detector de transición de 0 a 1

**Estado:** ✓ INCLUIDO EN EL DOCUMENTO LaTeX

**Enunciado:** Máquina que detecta la transición de X de 0 a 1 y activa la salida Z.

**Tabla de Verdad:**
| Q | X | Qp | Z |
|---|---|----|----|
| 0 | 0 | 0  | 0  |
| 0 | 1 | 1  | 0  |
| 1 | 0 | 0  | 1  |
| 1 | 1 | 1  | 0  |

**Funciones minimizadas:**
- `Qp = X`
- `Z = Q · X'`

**Imagen:** `img/circuito_4_9.png`

---

### Ejercicio 4.10 — Máquina de estados de 6 estados

**Estado:** ✓ INCLUIDO EN EL DOCUMENTO LaTeX

**Enunciado:** Máquina con entrada X y salida Z que transiciona entre 6 estados diferentes.

**Funciones minimizadas:**
- `D1 = Q1' · Q0 · X'`
- `D0 = X · (Q1' + Q0')`
- `Z = Q1 · Q0' · X`

**Imagen:** `img/circuito_4_10.png`

---

### Ejercicio 4.11 — Detector XOR entre entrada y estado anterior

**Estado:** ✓ INCLUIDO EN EL DOCUMENTO LaTeX

**Enunciado:** Máquina que detecta cambios en la entrada X (transiciones 01 o 10).

**Tabla de Verdad:**
| Q | X | Qp | Z |
|---|---|----|----|
| 0 | 0 | 0  | 0  |
| 0 | 1 | 1  | 1  |
| 1 | 0 | 0  | 1  |
| 1 | 1 | 1  | 0  |

**Funciones minimizadas:**
- `Qp = X`
- `Z = Q ⊕ X`

**Imagen:** `img/circuito_4_11.png`

---

```latex
\xor   % ⊕  (XOR)
\xnor  % ⊙  (XNOR)
```

## Paquetes utilizados

`amsmath`, `amssymb`, `geometry`, `graphicx`, `xcolor`, `booktabs`,
`array`, `fancyhdr`, `lastpage`, `hyperref`, `inputenc`, `fontenc`

## Pendientes / próximos pasos

1. **Agregar enunciados completos** en los espacios reservados de los ejercicios 4.3 a 4.11
   - Los espacios están marcados en el .tex con comentarios `% Espacio para que el usuario agregue el enunciado`

2. **Insertar capturas de CircuitVerse** para todos los ejercicios (4.1 a 4.11)
   - Crear carpeta `img/` si no existe
   - Archivos esperados:
     - `img/circuito_4_1.png` hasta `img/circuito_4_11.png`

3. **Nota sobre formato de tablas**
   - Ejercicio 4.8 utiliza `\resizebox{\textwidth}{!}` para mejor legibilidad de tablas grandes
   - Se puede ajustar manualmente a `\resizebox{0.8\textwidth}{!}` si es necesario

## Estado de completitud

✓ Ejercicios 4.1 a 4.11 completados en main.tex
✓ Tablas de verdad y funciones minimizadas agregadas
✓ Descripciones breves en subsubsection para formato uniforme
✓ Compilación exitosa sin errores LaTeX
⏳ Pendiente: Enunciados detallados (copiar/pegar desde EJERCICIO 4(3).md)
⏳ Pendiente: Imágenes de CircuitVerse

## Cambios recientes en el documento

### Actualización (12 de abril de 2026)

**Ejercicios 4.3 a 4.11 - ✓ COMPLETOS**

1. ✓ Agregados todos los ejercicios 4.3 a 4.11 al documento LaTeX
2. ✓ Tablas de verdad completadas para cada ejercicio
3. ✓ Funciones minimizadas en formato LaTeX
4. ✓ Descripciones breves en los títulos (subsubsection)
5. ✓ Tabla 4.8 optimizada con `\resizebox{\textwidth}{!}` para mejor legibilidad
6. ✓ Espacios reservados para:
   - Enunciados detallados
   - Imágenes de CircuitVerse

**Próximas actividades:**
- Copiar/pegar enunciados desde EJERCICIO 4(3).md
- Agregar imágenes de CircuitVerse en la carpeta `img/`
- Compilar nuevamente después de agregar las imágenes

## Referencias

- Libro: Stallings, "Arquitectura y Organización de Computadores"
- Apéndice A: Lógica Digital (incluido en bibliografia/)
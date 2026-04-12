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

### Ejercicio 4.3

**Estado:** No incluido en el documento LaTeX. Pendiente de resolver.

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

## Comandos personalizados en main.tex

```latex
\xor   % ⊕  (XOR)
\xnor  % ⊙  (XNOR)
```

## Paquetes utilizados

`amsmath`, `amssymb`, `geometry`, `graphicx`, `xcolor`, `booktabs`,
`array`, `fancyhdr`, `lastpage`, `hyperref`, `inputenc`, `fontenc`

## Pendientes / próximos pasos

1. Insertar capturas de CircuitVerse en los placeholders de los ej. 4.1, 4.2, 4.4, 4.5
   - Usar `\includegraphics[width=\textwidth]{img/circuito_4_X.png}` dentro del fbox
   - Crear carpeta `img/` en el proyecto LaTeX
2. Resolver y agregar ejercicio 4.3
3. Agregar minimizaciones de salidas Z0, Z1 para ejercicio 4.4

## Referencias

- Libro: Stallings, "Arquitectura y Organización de Computadores"
- Apéndice A: Lógica Digital (incluido en bibliografia/)
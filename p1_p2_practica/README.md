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

## Contenido de EJERCICIO_4.md

El archivo `EJERCICIO_4.md` contiene las soluciones de los ejercicios de
Máquinas de Estados Finitos de la Práctica 2.

### Ejercicio 4.1 — Paridad de bits (X e Y)
- **Entradas:** X, Y | **Estado:** Qa | **Salida:** Z
- **Tabla:** 8 filas (Qa × {X,Y} ∈ {0,1}²)
- **Función:** `Z = X ⊕ Y ⊕ Qa`
- **Próximo estado:** `Qp = X ⊕ Y ⊕ Qa` (igual que Z)
- Imagen del circuito: placeholder en LaTeX (insertar captura de CircuitVerse)

### Ejercicio 4.2 — Paridad con habilitación C
- **Entradas:** C, X, Y | **Estado:** Qa | **Salida:** Z
- **Comportamiento:** cuando C=0 → Qp=0, Z=0 (reset); cuando C=1 → calcula paridad
- **Función:** `Z = C · (X ⊕ Y ⊕ Qa)`
- Imagen del circuito: placeholder en LaTeX

### Ejercicio 4.3
- **No incluido** en el archivo EJERCICIO_4.md. Pendiente de resolver.

### Ejercicio 4.4 — Relación entre valores anteriores de X e Y
- **Entradas:** X, Y | **Salidas:** Z0, Z1
- Solo se cuenta con la tabla de salida en función de (Xant, Yant):
  - (0,0)→Z0=1,Z1=1 | (0,1)→Z0=0,Z1=1 | (1,0)→Z0=1,Z1=0 | (1,1)→Z0=1,Z1=1
- No se incluye minimización (no figura en el archivo fuente)
- Imagen del circuito: placeholder en LaTeX

### Ejercicio 4.5 — Comparación XYant vs XYact
- **Entradas:** X, Y | **Estado:** Qx (MSB), Qy (LSB) = XYant | **Salida:** Z
- Z = 1 si XYant > XYact; Z = 0 si XYant ≤ XYact
- **Tabla completa:** 16 filas. Z=1 en minterms {4, 8, 9, 12, 13, 14}
- **Minimización** (método algebraico desde suma canónica de productos):
  - Forma canónica SOP con los 6 minterms donde Z=1
  - Paso 1: agrupar m8,m9,m12,m13 → factor Qx·X' → **QxX'**
  - Paso 2: agrupar m4,m12 (idempotencia) → factor QyX'Y' → **QyX'Y'**
  - Paso 3: agrupar m12,m14 (idempotencia) → factor QxQyY' → **QxQyY'**
  - **Resultado:** `Z = Qx·X' + Qy·X'·Y' + Qx·Qy·Y'`
  - Equivalente: `Z = Xant·X' + Yant·X'·Y' + Xant·Yant·Y'`
- **Próximo estado:** Qx_next = X, Qy_next = Y
- Imagen del circuito: placeholder en LaTeX (circuito verificado en CircuitVerse)

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
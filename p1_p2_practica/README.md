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

### Opción 3: Usando make (si instalas el Makefile)
```bash
cd proyecto_latex
make
```

## Archivos generados (ignorados por git)

- `*.aux` - Archivos auxiliares
- `*.log` - Logs de compilación
- `*.out` - Archivos de hyperref
- `*.toc` - Tabla de contenidos
- `*.pdf` - PDF generado (compílalo localmente)
- `*.synctex.gz` - Sincronización editor-PDF

## Estructura del documento LaTeX

El archivo `main.tex` está preparado con:
- Paquetes matemáticos (amsmath, amssymb)
- Configuración de página (geometry)
- Encabezados y pies de página (fancyhdr)
- Hiperenlaces (hyperref)
- Soporte para español (babel)
- Entornos para ejercicios y soluciones
- Comandos personalizados para álgebra booleana

## Próximos pasos

1. Copiar el contenido de los ejercicios de `ejercicios/` a `main.tex`
2. Organizar por secciones
3. Agregar figuras si es necesario (crear carpeta `img/`)
4. Compilar y revisar

## Referencias

- Libro: Stallings, "Arquitectura y Organización de Computadores"
- Apéndice A: Lógica Digital (incluido en bibliografia/)

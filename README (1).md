# Mini-Calc – Analizador léxico y sintáctico

Trabajo Práctico Final de **Teoría de Autómatas** (Ingeniería en Informática, UNIDA).
Analizador léxico y analizador sintáctico descendente recursivo para el lenguaje
Mini-Calc, escritos en Python sin librerías de terceros ni generadores de
lexers/parsers.

## Integrantes

| Matrícula | Rama |
|---|
|  | 2023100352 | DEV-TIAGO |
|  | 2024100094 | DEV-ANDREA-DEOLINDA |
|  | 2024102176 | DEV-EDUARDO |
|  | 2022100633 | DEV-LEANDRO |
|  | 2019100853 | dev-lucas-alfaro |

## Requisitos

- **Python 3.8 o superior** (probado con Python 3.12).
- No hace falta instalar ningún paquete: usa solo la biblioteca estándar.

Para verificar la versión instalada:

    python --version

En Linux/macOS puede ser `python3 --version`.

## Instalación

1. Clonar el repositorio:

        git clone https://github.com/namnamopt/proyecto-TDA.git
        cd proyecto-TDA

2. Cambiarse a la rama con la versión integrada:

        git checkout QA

No hay paso de compilación ni dependencias que instalar.

## Ejecución

Analizar un archivo de código fuente `.calc`:

    python main.py ruta/al/archivo.calc

Sin argumentos, ejecuta un ejemplo incluido:

    python main.py

En Linux/macOS usar `python3` en lugar de `python`.

El programa muestra, en orden: los tokens reconocidos (análisis léxico), el
resultado del análisis sintáctico y la evaluación de cada asignación. Termina
con código `0` si todo es correcto y con código `1` si hay un error léxico,
sintáctico o de evaluación, indicando la línea y la columna.

## Ejemplo de archivo de entrada

`ejemplo.calc`:

    x = 10;
    y = 5;
    resultado = (x + y) * 2;
    promedio = resultado / 3;

Salida (resumida):

    --- ANÁLISIS SINTÁCTICO ---
    Correcto: 4 instrucción(es) cumplen la gramática.

    --- EJECUCIÓN ---
    x = 10
    y = 5
    resultado = 30
    promedio = 10

## Ejemplos de errores

| Entrada | Mensaje |
|---|---|
| `x = 5 $ 3;` | `Carácter no reconocido '$' en línea 1, columna 7.` |
| `x = 10` (sin `;`) seguido de otra línea | `Se esperaba ';' al final de la instrucción, pero se encontró 'y' en línea 2, columna 1.` |
| `x = (3 + 4;` | `Se esperaba ')', pero se encontró ';' en línea 1, columna 11.` |
| `x = 4 / 0;` | `No se puede dividir entre cero.` |

## Estructura del proyecto

    main.py      Punto de entrada: lee el .calc y ejecuta léxico, sintaxis y evaluación
    tokens.py    Tipos de token y clase Token
    lexer.py     Analizador léxico
    parser.py    Parser descendente recursivo, AST y evaluación
    errors.py    Excepciones de error léxico, sintáctico y de evaluación

## Gramática

    programa   = { asignacion } ;
    asignacion = IDENTIFIER "=" expresion ";" ;
    expresion  = termino { ("+" | "-") termino } ;
    termino    = factor { ("*" | "/") factor } ;
    factor     = NUMBER | IDENTIFIER | ("+" | "-") factor | "(" expresion ")" ;

La precedencia (`*` y `/` sobre `+` y `-`) y la asociatividad por la izquierda
quedan resueltas por la estructura de las funciones `_expression`, `_term` y
`_factor`.

## Pruebas

Casos de prueba disponibles en la carpeta `tests/` (completar con los archivos
`.calc` usados).

## Video demo

Ver el archivo de video incluido en esta carpeta `Documentacion/`.

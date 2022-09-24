---
description: Buscar texto
---

# Grep

Grep (por sus siglas en inglés Globally Search For Regular Expression and Print out) **es una herramienta de líneas de comando usada para buscar cadenas de texto** y encontrar coincidencias dentro de este. También puede ser utilizada para encontrar una palabra o combinación de palabras dentro de un fichero.

### Sintaxis

A continuacion esta la sintaxis de este comando de una manera simplificada:

```
grep '<texto-buscado>' <archivo/archivos>
```

Tenga en cuenta que las comillas simples o dobles son requeridas alrededor del texto si es más de una palabra.

Tú puedes además usar el comodín (\*) para seleccionar todos los archivos en un directorio.

El resultado de esto son las ocurrencias del patrón (por la línea en la que se encuentra) en los archivos. Si no existe una coincidencia, no se imprimirá ninguna salida en la terminal.

En el **manual** aparece de esta manera la sintaxis de grep:

```
grep [OPTION...] PATTERNS [FILE...]
```

* **grep**: la instrucción de comando
* **\[opciones]**: modificadores del comando
* **pattern**: el patrón que queremos encontrar con la búsqueda
* **\[ARCHIVO]**: el archivo en el que estás realizando la búsqueda

### Flags

Antes que nada explicaremos las opciones disponibles:

| Flags | Descripcion                                                                    |
| ----- | ------------------------------------------------------------------------------ |
| -i    | no diferenciará entre mayúsculas y minúsculas.                                 |
| –w    | fuerza que sólo encuentre palabras concretas y no con una coincidencia parcial |
| -v    | selecciona las líneas que no coinciden                                         |
| -n    | muestra el número de la línea con las palabras de solicitadas                  |
|       |                                                                                |
|       |                                                                                |
|       |                                                                                |
|       |                                                                                |

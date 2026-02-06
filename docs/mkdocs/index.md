# Guía Completa: Configuración de MkDocs con Material y UV

Esta guía proporciona todos los pasos necesarios para crear y configurar un proyecto MkDocs con el tema Material, utilizando `uv` para mantener las dependencias aisladas.

---

## Creación del proyecto con uv

### Paso inicial: Inicializar el proyecto

```bash
uv init misdocs
```

Este comando creará una nueva carpeta `misdocs` con la estructura básica del proyecto.

---

## Configuración del entorno y dependencias

### Navegar al directorio del proyecto

```bash
# Navega al directorio del proyecto
cd misdocs
```

### Crear un entorno virtual Python

```bash
# Crea un entorno virtual Python
uv venv
```

### Activar el entorno virtual

```bash
# Activa el entorno virtual
source .venv/bin/activate  # En Linux/Mac

# o
.\.venv\Scripts\activate  # En Windows
```

### Instalar MkDocs y plugins útiles

```bash
# Instala MkDocs y plugins útiles
uv pip install mkdocs mkdocs-material
```

---

## Estructura inicial del proyecto

### Inicializar la estructura de MkDocs

```bash
# Inicializa la estructura de MkDocs
mkdocs new .
```

Esto creará:

- `docs/` - Carpeta para tu documentación
- `mkdocs.yml` - Archivo de configuración principal

---

## Configuración básica de mkdocs.yml

Edita el archivo `mkdocs.yml` con la siguiente configuración inicial:

```yaml
site_name: Mis Documentos
theme:
  name: material
  language: es
  palette:
    primary: blue
    accent: indigo

nav:
  - Inicio: index.md
```

---

## Comandos útiles para desarrollo

### Iniciar servidor de desarrollo

```bash
# Iniciar servidor de desarrollo
mkdocs serve
```

### Construir el sitio estático

```bash
# Construir el sitio estático
mkdocs build
```

### Desplegar (si usas GitHub Pages)

```bash
# Desplegar (si usas GitHub Pages)
mkdocs gh-deploy
```

---

## Mejores prácticas

### 1. Añade un `.gitignore`

Crea un archivo `.gitignore` con el siguiente contenido:

```
.venv/
site/
*.pyc
__pycache__/
```

### 2. Crea un `requirements.txt`

Para mantener un registro de tus dependencias:

```bash
uv pip freeze > requirements.txt
```

---

## Uso del plugin mkdocs-awesome-pages-plugin

Este plugin te permite organizar mejor la navegación de tu documentación.

### Paso 1: Instalar el plugin

```bash
# Asegúrate de estar en tu entorno (con .venv activado)
source .venv/bin/activate  # Linux/Mac
# o
.\.venv\Scripts\activate  # Windows

# Instala el plugin
uv pip install mkdocs-awesome-pages-plugin
```

### Paso 2: Configurar `mkdocs.yml`

Edita tu archivo `mkdocs.yml` y **elimina la sección `nav`** (si la tienes). Luego añade el plugin:

```yaml
site_name: Mis Documentos
theme:
  name: material
  language: es
  features:
    - navigation.tabs
    - navigation.top

plugins:
  - awesome-pages
```

> **💡 Importante:** Sin `nav`, el plugin construirá la navegación automáticamente desde tus carpetas.

---

## Paso 3: Organiza tus archivos en carpetas por categoría

Ejemplo de estructura sugerida:

```bash
docs/
├── index.md              # Página principal
├── guias/
│   ├── intro.md
│   └── instalacion.md
├── referencia/
│   ├── api.md
│   └── config.md
└── tutoriales/
    ├── basico.md
    └── avanzado.md
```

---

## Paso 4 (opcional pero recomendado): Crea archivos `.pages` para personalizar

Dentro de cada carpeta, crea un archivo `.pages` para darle título y orden:

### `docs/guias/.pages`

```yaml
title: Guías
nav:
  - Introducción: intro.md
  - Instalación: instalacion.md
```

### `docs/referencia/.pages`

```yaml
title: Referencia Técnica
nav:
  - API: api.md
  - Configuración: config.md
```

### `docs/tutoriales/.pages`

```yaml
title: Tutoriales
nav:
  - Básico: basico.md
  - Avanzado: avanzado.md
```

> **📝 Nota:** Si no pones `.pages`, usará el nombre de la carpeta y orden alfabético.

---

## Paso 5: Prueba tu sitio

```bash
mkdocs serve
```

Verás las pestañas: **Guías | Referencia Técnica | Tutoriales**, con subpáginas organizadas según tus `.pages`.

---

## 💡 Consejo final

Guarda tus dependencias actualizadas:

```bash
uv pip freeze > requirements.txt
```

---

## Configuración completa del archivo mkdocs.yml

Aquí tienes un ejemplo de configuración más completa con características adicionales:

```yaml
site_name: misdocs
theme:
  name: material
  language: es
  palette:
    primary: blue
    accent: indigo
  features:
    - navigation.tabs          # Activa pestañas horizontales
    - navigation.sections      # Opcional: permite secciones colapsables
    - navigation.expand        # Expande secciones automáticamente

plugins:
  - awesome-pages
  - git-revision-date-localized
  - search
```

---

## Estructura de archivos del proyecto

Al finalizar, tu proyecto debería tener esta estructura:

```
MISDOCS/
├── .venv/
├── docs/
│   ├── index.md
│   ├── guias/
│   │   ├── intro.md
│   │   └── instalacion.md
│   ├── referencia/
│   │   ├── api.md
│   │   └── config.md
│   └── tutoriales/
│       ├── basico.md
│       └── avanzado.md
├── .gitignore
├── python-version
├── main.py
├── mkdocs.yml
├── pyproject.toml
└── README.md
```

---

## Comandos de referencia rápida

| Comando | Descripción |
|---------|-------------|
| `uv init misdocs` | Crear nuevo proyecto |
| `uv venv` | Crear entorno virtual |
| `source .venv/bin/activate` | Activar entorno (Linux/Mac) |
| `.\.venv\Scripts\activate` | Activar entorno (Windows) |
| `uv pip install mkdocs mkdocs-material` | Instalar dependencias base |
| `uv pip install mkdocs-awesome-pages-plugin` | Instalar plugin de páginas |
| `mkdocs new .` | Inicializar estructura MkDocs |
| `mkdocs serve` | Servidor de desarrollo local |
| `mkdocs build` | Construir sitio estático |
| `mkdocs gh-deploy` | Desplegar a GitHub Pages |
| `uv pip freeze > requirements.txt` | Guardar dependencias |

---

## Recursos adicionales

- [Documentación oficial de MkDocs](https://www.mkdocs.org/)
- [Material for MkDocs](https://squidfunk.github.io/mkdocs-material/)
- [Awesome Pages Plugin](https://github.com/lukasgeiter/mkdocs-awesome-pages-plugin)
- [UV Package Manager](https://github.com/astral-sh/uv)

---

## Conclusión

Con esta configuración tienes un proyecto MkDocs completamente funcional con:

✅ Gestión de dependencias aislada con `uv`  
✅ Tema Material moderno y responsive  
✅ Navegación automática organizada por carpetas  
✅ Servidor de desarrollo local  
✅ Preparado para despliegue en GitHub Pages

¡Ahora puedes comenzar a escribir tu documentación en los archivos `.md` dentro de la carpeta `docs/`!
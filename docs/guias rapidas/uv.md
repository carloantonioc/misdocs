# Guía Completa de `uv` - Gestor Moderno de Proyectos Python

## 📚 Tabla de Contenidos

- [¿Qué es uv?](#qué-es-uv)
- [Instalación](#instalación)
- [Conceptos Fundamentales](#conceptos-fundamentales)
- [Comandos Esenciales](#comandos-esenciales)
- [Flujos de Trabajo](#flujos-de-trabajo)
- [Gestión de Dependencias](#gestión-de-dependencias)
- [Buenas Prácticas](#buenas-prácticas)
- [Solución de Problemas](#solución-de-problemas)

---

## ¿Qué es uv?

`uv` es un gestor de paquetes y proyectos Python ultrarrápido, escrito en Rust, creado por Astral (los mismos desarrolladores de Ruff). Es una alternativa moderna a `pip`, `pip-tools`, `pipenv` y `poetry`.

### ✨ Ventajas principales

- ⚡ **10-100x más rápido** que pip
- 🔒 **Gestión automática** de entornos virtuales
- 📦 **Resolución de dependencias** inteligente
- 🎯 **Reproducibilidad** garantizada
- 🧹 **Sin configuración compleja**

---

## Instalación

### Linux / macOS / WSL

```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```

Luego, recarga tu terminal:

```bash
source ~/.bashrc
# o
source ~/.zshrc
```

### Verificar instalación

```bash
uv --version
```

Deberías ver algo como: `uv 0.9.27` (o superior)

---

## Conceptos Fundamentales

### 🔑 Diferencias clave entre comandos

| Comando | Propósito | Crea `.venv/` | Modifica `pyproject.toml` |
|---------|-----------|---------------|---------------------------|
| `uv init` | Inicializa estructura del proyecto | ❌ | ✅ Crea el archivo |
| `uv venv` | Crea entorno virtual | ✅ | ❌ |
| `uv add` | Agrega dependencia | ✅ (si no existe) | ✅ Actualiza |
| `uv pip install` | Instala paquete (legacy) | ❌ | ❌ |
| `uv sync` | Sincroniza dependencias | ✅ (si no existe) | ❌ |

### 📂 Estructura de un proyecto con `uv`

```
mi-proyecto/
├── .venv/              # Entorno virtual (auto-generado)
├── .python-version     # Versión de Python del proyecto
├── pyproject.toml      # Configuración y dependencias
├── README.md           # Documentación
└── src/                # Tu código
    └── __init__.py
```

### 💡 `uv init` - Inicializa un proyecto

Con `uv init <nombre>`, **creas un proyecto completo**:

- ✅ Crea la carpeta `<nombre>`
- ✅ Genera `pyproject.toml` con metadatos del proyecto
- ✅ Crea `README.md` inicial
- ✅ Define la versión de Python (`.python-version`)
- ✅ Opcionalmente, con `--package`, crea estructura de paquete Python

**Resultado de `uv init mi-proyecto`:**
```
mi-proyecto/
├── pyproject.toml    ← Configuración del proyecto
├── README.md         ← Documentación inicial
├── .python-version   ← Versión de Python especificada
└── hello.py          ← Archivo de ejemplo
```

### 🔄 `uv venv` - Crea el entorno virtual

`uv venv` crea el espacio aislado para dependencias:

- ✅ Crea la carpeta `.venv/`
- ✅ Instala un intérprete de Python aislado
- ✅ Configura espacio aislado para dependencias
- ✅ **NO** modifica `pyproject.toml` automáticamente

**Resultado después de `uv venv`:**
```
mi-proyecto/
├── .venv/            ← Entorno virtual aislado
│   ├── bin/
│   ├── lib/
│   └── pyvenv.cfg
├── pyproject.toml
├── README.md
└── .python-version
```

> **💡 Nota importante:** `uv venv` es **opcional** si usas `uv add` o `uv sync`, ya que estos comandos crean `.venv/` automáticamente si no existe.

---

## Comandos Esenciales

### 1️⃣ Inicializar un nuevo proyecto

```bash
# Posiciónate donde quieres crear el proyecto
cd ~/Proyectos

# Crea un nuevo proyecto
uv init mi-proyecto

# Resultado:
# mi-proyecto/
# ├── pyproject.toml
# ├── README.md
# ├── .python-version
# └── hello.py
```

**Opciones útiles:**

```bash
# Crear un paquete (estructura más completa)
uv init --package mi-paquete

# Especificar versión de Python
uv init --python 3.12 mi-proyecto
```

### 2️⃣ Crear entorno virtual (opcional)

```bash
cd mi-proyecto
uv venv
```

**💡 Nota:** Este paso es **opcional** si usarás `uv add` o `uv sync`, ya que crean `.venv/` automáticamente.

### 3️⃣ Activar entorno virtual (opcional)

**Linux / macOS / WSL:**
```bash
source .venv/bin/activate
```

**Windows (PowerShell):**
```powershell
.venv\Scripts\Activate.ps1
```

**Windows (CMD):**
```cmd
.venv\Scripts\activate.bat
```

Verás `(mi-proyecto)` al inicio de tu terminal cuando esté activo.

### 4️⃣ Agregar dependencias (método recomendado)

```bash
# Agrega un paquete
uv add requests

# Agrega con extras
uv add "fastapi[standard]"

# Agrega como dependencia de desarrollo
uv add --dev pytest

# Agrega versión específica
uv add "django==5.0"
```

**Resultado en `pyproject.toml`:**

```toml
[project]
dependencies = [
    "requests>=2.31.0",
    "fastapi[standard]>=0.109.0",
]

[dependency-groups]
dev = [
    "pytest>=8.0.0",
]
```

### 5️⃣ Remover dependencias

```bash
uv remove requests
```

### 6️⃣ Listar paquetes instalados

```bash
uv pip list

# Mostrar info de un paquete específico
uv pip show requests
```

---


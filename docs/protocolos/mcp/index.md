# Proyecto MCP

## Guía Paso a Paso: Configuración de MCP en WSL desde cero

**Entorno validado**\
- Windows 11\
- WSL2\
- Ubuntu 22.04\
- Python 3.10\
- MCP v1.26.0

------------------------------------------------------------------------

## 1. ¿Qué es MCP? (Visión conceptual)

**MCP (Model Context Protocol)** es un protocolo estándar que permite a
los modelos de lenguaje grandes (LLMs) interactuar de forma segura y
estructurada con herramientas externas, como APIs, bases de datos o
sistemas de archivos.

-   Define contratos claros para:
    -   **Tools**
    -   **Resources**
    -   **Prompts**
-   Usa **HTTP/JSON**
-   Soporta autenticación, descubrimiento automático y validación de
    esquemas
-   Se ejecuta como un **servidor ASGI** (uvicorn)
-   Es mantenido por **Anthropic**

En términos simples: MCP es un "traductor universal" que le da *manos* a
la IA.\
Permite que no solo responda, sino que **actúe** (sumar, buscar, leer
archivos, consultar datos).\
Es usado por clientes como **Claude** y **Cursor**.

------------------------------------------------------------------------

## 2. Arquitectura técnica (resumen)

-   Cliente LLM (Claude, Cursor, etc.)
-   Servidor MCP (Python)
-   uvicorn como motor ASGI
-   Comunicación vía HTTP/JSON sobre `localhost`

------------------------------------------------------------------------

## Prerrequisitos

# Requisitos para Proyecto MCP + Qwen

Tabla de dependencias y herramientas necesarias para replicar la integración MCP-Qwen.

| Programa / Librería | Descripción breve | Guía rápida de instalación |
|---------------------|-------------------|----------------------------|
| **Python ≥ 3.8** | Entorno base para ejecutar scripts y servidores MCP | [Instalación oficial](https://www.python.org/downloads/) |
| **uv** | Gestor de paquetes y entornos virtuales rápido (reemplaza a pip + venv) | ver guia rapida |
| **WSL (opcional)** | Entorno Linux en Windows para desarrollo terminal-based | ver guia rapida |
| **fastmcp** | Implementación del protocolo MCP (servidor y cliente) | ```uv add fastmcp``` |
| **requests** | Biblioteca para llamadas HTTP a la API de DashScope | ```uv add requests```<br>[Documentación](https://requests.readthedocs.io/) |
| **DashScope Account** | Cuenta en Alibaba Cloud para acceder a Qwen-Turbo | [Registro gratuito](https://dashscope.aliyun.com/) |
| **Token sk-...** | Clave API con prefijo `sk-` para modo compatible | Generar en [DashScope Console > API Keys](https://dashscope.aliyun.com/console/api-key) |
| **Endpoint compatible** | URL específica para modo OpenAI-compatible | Usar: `https://dashscope-intl.aliyuncs.com/compatible-mode/v1/chat/completions` |

## Notas críticas verificadas:
- ✅ **Token**: Debe incluir `sk-` (ej: `sk-eb0dd39e8aaf4902b0ba22c8fa509af8`)
- ✅ **URL**: Solo funciona con `/compatible-mode/v1/chat/completions` (no con rutas nativas)
- ✅ **Entorno**: Todo probado en WSL + Ubuntu + Python 3.10 + uv 0.2+
- ✅ **Dependencias**: Solo se requieren `fastmcp` y `requests` (no se necesita `openai` ni `dashscope` SDK)

## 3. Preparar el entorno de trabajo

**Desde la terminal de Ubuntu (WSL), navega al sistema de archivos de
Windows y crea tu carpeta de proyecto:**

``` bash
cd /mnt/c/Users/Carlos.Cornejo/Documents/Proyectos
mkdir -p mcp
cd mcp
```

Esto permite que el proyecto resida en Windows, pero se ejecute
completamente dentro de WSL.

------------------------------------------------------------------------

## 4. Configurar VS Code con WSL

Desde la carpeta del proyecto:

``` bash
code .
```

En VS Code: - Abrir una nueva terminal - Verificar que sea **Ubuntu /
WSL**, no PowerShell ni CMD

------------------------------------------------------------------------

## 5. Instalar el SDK de MCP

``` bash
pip install "mcp[cli]"
```

Verificación:

``` bash
pip show mcp
```

Salida esperada:

    Name: mcp
    Version: 1.26.0
    Author: Anthropic, PBC

------------------------------------------------------------------------

## 6. Requisito adicional: Node.js (solo para modo desarrollo)

⚠️ **Solo necesario para `mcp dev`**, ya que utiliza el MCP Inspector
vía `npx`.

``` bash
curl -fsSL https://deb.nodesource.com/setup_20.x | sudo -E bash -
sudo apt install -y nodejs
```

------------------------------------------------------------------------

## 7. Crear tu servidor MCP

``` python
from mcp.server.fastmcp import FastMCP

app = FastMCP("mi-servidor")

@app.tool()
def sumar(a: int, b: int) -> int:
    return a + b

@app.resource("saludo://{nombre}")
def obtener_saludo(nombre: str) -> str:
    return f"¡Hola {nombre}! 👋"

if __name__ == "__main__":
    app.run()
```

------------------------------------------------------------------------

## 8. Ejecutar el servidor


``` bash
mcp dev server.py
```

Manual

``` bash
npx @modelcontextprotocol/inspector mcp run server.py
```

------------------------------------------------------------------------

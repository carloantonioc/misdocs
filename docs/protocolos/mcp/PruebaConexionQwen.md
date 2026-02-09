# Prueba: Conexion LLM Qwen

## 1. Crear entorno desde cero con `uv init`

```bash
uv init nombre-del-proyecto
```

## 2. Entrar al directorio del proyecto

```bash
cd nombre-del-proyecto
```

## 3. crear entorno virtual

```bash
uv venv
```

Puedes instalar paquetes con:

```bash
uv add nombre-paquete
```


## 4. Verificar la versión de Python

```bash
~/.venv/bin/python --version
```

**Salida:**

```bash
carlos@SGKX-P2-04V0:/mnt/c/Users/Carlos.Cornejo/Documents/Proyectos/mcp-pruebaclient$ ~/.venv/bin/python --version
Python 3.10.12
```

---

## 5: Instalar dashscope

```bash
uv add dashscope
```

### ℹ️ ¿Por qué `dashscope`?

Porque es el SDK oficial de Alibaba para acceder a Qwen.

**Esto instala:**

- El paquete `dashscope`
- Sus dependencias mínimas

### Ejecuto estos comando para estar seguro de la versión

**Salida del comando:**

```bash
carlos@SGKX-P2-04V0:/mnt/c/Users/Carlos.Cornejo/Documents/Proyectos/mcp-pruebaclient$ source .venv/bin/activate
(mcp-pruebaclient) carlos@SGKX-P2-04V0:/mnt/c/Users/Carlos.Cornejo/Documents/Proyectos/mcp-pruebaclient$ uv pip show dashscope
Name: dashscope
Version: 1.20.11
Location: /mnt/c/Users/Carlos.Cornejo/Documents/Proyectos/mcp-pruebaclient/.venv/lib/python3.10/site-packages
Requires: certifi, cryptography, requests, websocket-client
Required-by:
```

## 6. Crea archivo client.py en Python

```bash
# prueballm.py
from dashscope import Generation

# 🔑 PON TU TOKEN REAL AQUÍ
API_KEY = "Aquí tu Token"

# Llamada mínima a Qwen-Turbo
r = Generation.call(
    model="qwen-turbo",
    messages=[{"role": "user", "content": "test"}],
    max_tokens=5,
    api_key=API_KEY  # ← Esto es obligatorio en versiones recientes
)

# Verificación segura
if r and hasattr(r, 'output'):
    print("✅ OK")
else:
    print("❌ FAIL")
```

### Realizar Prueba

**comando:**

```bash
uv run python prueballm.py
```
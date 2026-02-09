# Guía de Instalación de WSL (Windows Subsystem for Linux) en Windows 11

## Requisitos Previos

- Windows 11 (con las últimas actualizaciones)
- Permisos de Administrador
- Conexión a Internet

## Paso 1: Habilitar WSL y la Plataforma de Máquina Virtual

Estos comandos deben ejecutarse en **PowerShell como Administrador**.

### 1.1 Habilitar el Subsistema de Windows para Linux

```powershell
dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
```

Este comando habilita la característica WSL en Windows.

### 1.2 Habilitar la Plataforma de Máquina Virtual

```powershell
dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
```

Este comando habilita la característica de Plataforma de Máquina Virtual, necesaria para WSL2.

### 1.3 Reiniciar el sistema

```powershell
shutdown /r /t 0
```

⚠️ **Importante**: El reinicio es obligatorio después de habilitar estas características.

---

## Paso 2: Verificar y Configurar WSL2

Después del reinicio, abre **PowerShell como Administrador** nuevamente.

### 2.1 Verificar que WSL2 es la versión predeterminada

```powershell
wsl --status
```

**Salida esperada:**
```
Default Version: 2
```

Si WSL2 no es la versión predeterminada, establécela manualmente:

```powershell
wsl --set-default-version 2
```

---

## Paso 3: Instalar Ubuntu 22.04 LTS

### 3.1 Instalar la distribución

```powershell
wsl --install -d Ubuntu-22.04
```

📌 **Nota**: Este comando realiza las siguientes acciones automáticamente:

| Paso | Acción |
|------|--------|
| 1 | Habilita la característica "Subsistema de Windows para Linux" (WSL) |
| 2 | Habilita la característica "Plataforma de máquina virtual" |
| 3 | Descarga e instala el paquete del kernel de Linux para WSL2 |
| 4 | Establece WSL2 como versión predeterminada |
| 5 | Descarga desde Microsoft Store e instala **solo Ubuntu 22.04 LTS** |
| 6 | Te pide crear usuario y contraseña UNIX dentro de Ubuntu |

⚠️ **Advertencia**: No instala la distro genérica "Ubuntu" (que suele ser la versión más reciente, ej. 24.04). Solo instala `Ubuntu-22.04`.

### 3.2 Configuración inicial de Ubuntu

Al finalizar la instalación, se abrirá automáticamente la terminal de Ubuntu y te pedirá:

1. **Crear un nombre de usuario UNIX**
   ```
   Enter new UNIX username: tu_usuario
   ```

2. **Crear una contraseña**
   ```
   New password: ********
   Retype new password: ********
   ```

---

## Paso 4: Verificar la Instalación

### 4.1 Listar distribuciones instaladas

```powershell
wsl --list --verbose
```

o su forma abreviada:

```powershell
wsl -l -v
```

**Salida esperada:**
```
  NAME            STATE      VERSION
* Ubuntu-22.04    Running    2
```

Donde:
- `NAME`: Nombre de la distribución instalada
- `STATE`: Estado actual (Running/Stopped)
- `VERSION`: Versión de WSL (debe ser 2)
- `*`: Indica la distribución predeterminada

### 4.2 Verificar la versión de Ubuntu

Desde PowerShell o desde dentro de Ubuntu:

```bash
wsl -d Ubuntu-22.04 lsb_release -a
```

o dentro de Ubuntu:

```bash
lsb_release -a
```

**Salida esperada:**
```
No LSB modules are available.
Distributor ID: Ubuntu
Description:    Ubuntu 22.04.x LTS
Release:        22.04
Codename:       jammy
```

---

## Comandos Útiles de WSL

### Gestión de distribuciones

```powershell
# Listar todas las distribuciones disponibles para instalar
wsl --list --online

# Listar distribuciones instaladas
wsl --list --verbose

# Establecer una distribución como predeterminada
wsl --set-default Ubuntu-22.04

# Iniciar una distribución específica
wsl -d Ubuntu-22.04

# Detener una distribución
wsl --terminate Ubuntu-22.04

# Detener todas las distribuciones
wsl --shutdown
```

### Actualización y mantenimiento

```powershell
# Actualizar WSL
wsl --update

# Verificar versión de WSL
wsl --version

# Cambiar la versión de WSL de una distribución
wsl --set-version Ubuntu-22.04 2
```

### Desinstalación

```powershell
# Desinstalar una distribución
wsl --unregister Ubuntu-22.04
```

⚠️ **Advertencia**: Esto eliminará permanentemente todos los datos de la distribución.

---

## Acceso a Archivos

### Desde Windows a Ubuntu

Los archivos de Ubuntu están accesibles desde el Explorador de Windows en:

```
\\wsl$\Ubuntu-22.04\home\tu_usuario
```

O simplemente escribe en el Explorador de Windows:

```
\\wsl$
```

### Desde Ubuntu a Windows

Las unidades de Windows están montadas en `/mnt/`:

```bash
# Acceder a C:\
cd /mnt/c/

# Acceder a D:\
cd /mnt/d/
```

---

## Actualizar el Sistema Ubuntu

Una vez instalado Ubuntu, es recomendable actualizar los paquetes:

```bash
sudo apt update && sudo apt upgrade -y
```

---

## Solución de Problemas Comunes

### Error: "WSL 2 requiere una actualización del componente kernel"

**Solución**: Descarga e instala el paquete de actualización del kernel de Linux desde:
- https://aka.ms/wsl2kernel

### Ubuntu no inicia o muestra error

**Solución**: Reinicia WSL

```powershell
wsl --shutdown
wsl -d Ubuntu-22.04
```

### Cambiar la versión de una distribución de WSL1 a WSL2

```powershell
wsl --set-version Ubuntu-22.04 2
```

---

## Recursos Adicionales

- [Documentación oficial de Microsoft sobre WSL](https://docs.microsoft.com/es-es/windows/wsl/)
- [Ubuntu WSL Wiki](https://wiki.ubuntu.com/WSL)
- [Foro de la comunidad WSL](https://github.com/microsoft/WSL/issues)

---

## Notas Finales

✅ WSL2 ofrece mejor rendimiento que WSL1  
✅ Puedes instalar múltiples distribuciones de Linux simultáneamente  
✅ Cada distribución funciona de manera independiente  
✅ Los archivos se pueden compartir fácilmente entre Windows y Linux  

---

**Fecha de última actualización**: Febrero 2026  
**Versión del documento**: 1.0
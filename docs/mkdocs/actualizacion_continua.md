# Workflow de Actualizacion Continua

Cada vez que hagas cambios en tu documentación:

```bash
# 1. Edita tus archivos .md en la carpeta docs/

# 2. Si usas uv activar el ambiente virtual/
source .venv/bin/activate

# 3 Antes de trabajar
git pull origin main


# 4. Guarda los cambios en la rama main
git add .
git commit -m "Actualización de documentación"
git push origin main

# 5. Despliega los cambios a GitHub Pages
mkdocs gh-deploy
```

**¡Eso es todo!** Tu sitio se actualizará automáticamente en 1-2 minutos.

# Si hay problemas en gh-pages:

```bash
# Paso 1: Eliminar la rama gh-pages local
git branch -D gh-pages

#Por qué:
# La rama gh-pages es generada automáticamente por MkDocs
# No contiene trabajo manual importante
# Sus archivos se pueden regenerar desde cero
# Eliminar el historial conflictivo era más fácil que resolverlo

# Paso 2 : Eliminar la rama gh-pages remota
git push origin --delete gh-pages

#Por qué:
# GitHub tenía la rama conflictiva
# Necesitabas eliminarla para poder crear una nueva limpia
# El próximo deploy crearía una rama fresca sin conflictos

# Paso 3: Deploy limpio desde cero
mkdocs gh-deploy

# Qué hizo:
# Construyó la documentación nueva (mkdocs build)
# Creó una rama gh-pages local nueva
# Subió los archivos generados a GitHub
# Como no existía gh-pages remoto, no hubo conflictos

```

# 🎯 ¿POR QUÉ FUNCIONÓ ESTA SOLUCIÓN?
- gh-pages es una rama "desechable"
- Solo contiene archivos generados (HTML, CSS, JS)
- No hay código fuente importante
- Se puede regenerar en cualquier momento
- Eliminar el historial conflictivo
- En lugar de intentar fusionar versiones diferentes de archivos generados
- Se eliminó todo y se creó desde cero
- GitHub aceptó la nueva rama sin problemas
- Clean slate (Pizarra limpia)
- Sin commits divergentes
- Sin archivos binarios en conflicto
- Solo la versión más reciente de la documentación
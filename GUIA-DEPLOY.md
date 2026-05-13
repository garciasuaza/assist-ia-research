# Guía: construcción, deploy y actualización de Assist-IA-Research

**Proyecto:** Assist-IA-Research  
**URL pública:** https://garciasuaza.github.io/assist-ia-research/  
**Repositorio:** https://github.com/garciasuaza/assist-ia-research  
**Directorio local:** `E:\Google drive\Personal Docs\Configurar GPTs\Academic research project\assist-ia-redesign\`

---

## 1. Estructura del proyecto

Todos los archivos están en una sola carpeta. La página es un único archivo HTML autocontenido.

```
assist-ia-redesign/
├── index.html                          ← página principal (todo el CSS y JS está aquí)
├── AI_HEI_Colombia_WorkingPaper.pdf    ← paper estructurado
├── AI_HEI_Colombia_WorkingPaper_Naive.pdf ← paper prompt directo
├── paper-page-1.png                    ← preview primera página del paper
├── paper_lifecycle_v3.svg              ← diagrama ciclo de vida
├── command_table_v2.svg                ← diagrama tabla de comandos
├── tools_connections_v4.svg            ← diagrama conexiones de herramientas
└── GUIA-DEPLOY.md                      ← este archivo
```

**Regla principal:** todo el código (HTML, CSS, JavaScript) vive dentro de `index.html`. No hay archivos separados de estilos ni scripts.

---

## 2. Secciones de la página (orden actual)

| ID | Título | Descripción |
|----|--------|-------------|
| `#problema` | El problema y la solución | Dos columnas: causas del problema + solución del sistema |
| `#validacion` | Alcance | Banda oscura: qué produce, qué no reemplaza, qué acelera |
| `#sistema` | Un sistema de investigación | 4 tarjetas (DETECT/EXPLORE/BUILD/WRITE) + 2 diagramas |
| `#flujo` | Flujo de trabajo | 5 pasos interactivos con prompt y salida por etapa |
| `#comparacion` | Comparación de outputs | Naive vs. estructurado lado a lado |
| `#academica` | Evaluación académica | Assessment general: puntajes y fortalezas/limitaciones |

---

## 3. Cómo hacer cambios al sitio

Todos los cambios se hacen directamente sobre `index.html` con cualquier editor de texto (VS Code, Notepad++, etc.).

### Cambiar texto de una sección
Abre `index.html`, busca el `id` de la sección (ej. `id="problema"`) y edita el contenido HTML.

### Agregar un PDF nuevo
1. Copia el PDF a la carpeta del proyecto.
2. En `index.html`, agrega o actualiza el enlace:
   ```html
   <a href="nombre-del-archivo.pdf" target="_blank">Ver documento</a>
   ```
3. En git, agrega el archivo nuevo antes de hacer commit (ver sección 5).

### Cambiar colores o tipografía
Los colores están definidos como variables CSS al inicio de `index.html`, dentro de `:root { }`:
```css
:root {
  --blue: #2f6bff;    /* color principal de acento */
  --cyan: #20d3ee;    /* color del hero y botón primario */
  --mint: #47e0a1;    /* color de métricas y highlights */
  --navy: #081b3a;    /* color de títulos */
  --muted: #657083;   /* color de texto secundario */
}
```

---

## 4. Requisitos previos (ya instalados)

Estos pasos ya están completos. Se documentan por si se necesita reconfigurar en otro equipo.

### Git
```powershell
# Verificar instalación
git --version

# Configurar identidad (ya hecho)
git config --global user.name "andres.garcia"
git config --global user.email "garciasuaza@gmail.com"
```

### GitHub CLI (gh)
```powershell
# Instalar via winget (ya instalado)
winget install --id GitHub.cli

# Autenticar (ya hecho — si expira, repetir)
gh auth login
# Seleccionar: GitHub.com → HTTPS → Login with a web browser
# Copiar el código de 8 caracteres, pegarlo en el browser que se abre
```

---

## 5. Subir cambios a GitHub (flujo normal)

Desde PowerShell, navegar a la carpeta del proyecto y ejecutar:

```powershell
cd "E:\Google drive\Personal Docs\Configurar GPTs\Academic research project\assist-ia-redesign"

# Ver qué archivos cambiaron
git status

# Agregar los archivos modificados (ajustar nombres según lo que cambió)
git add index.html

# Si también agregaste un PDF u otro archivo nuevo:
git add nombre-del-archivo.pdf

# Crear el commit con una descripción del cambio
git commit -m "descripción breve del cambio"

# Subir a GitHub
git push
```

El sitio se actualiza automáticamente en **1-2 minutos** después del `git push`.

### Ejemplo real
```powershell
cd "E:\Google drive\Personal Docs\Configurar GPTs\Academic research project\assist-ia-redesign"
git add index.html
git commit -m "fix: actualizar abstract del paper estructurado"
git push
```

---

## 6. Cómo se creó el repositorio (primera vez — no repetir)

Estos pasos ya están hechos. Se documentan como referencia.

```powershell
# 1. Inicializar git en la carpeta del proyecto
cd "E:\Google drive\Personal Docs\Configurar GPTs\Academic research project\assist-ia-redesign"
git init

# 2. Agregar todos los archivos y hacer el primer commit
git add index.html AI_HEI_Colombia_WorkingPaper.pdf paper-page-1.png ...
git commit -m "initial: Assist-IA-Research page"

# 3. Crear el repositorio en GitHub y subir
gh repo create assist-ia-research --public --source=. --push

# 4. Activar GitHub Pages (rama master, carpeta raíz)
gh api repos/garciasuaza/assist-ia-research/pages \
  --method POST \
  -f "source[branch]=master" \
  -f "source[path]=/"
```

---

## 7. Solución de problemas frecuentes

| Problema | Causa probable | Solución |
|----------|---------------|----------|
| `gh: command not found` | gh no está en el PATH | Abrir una nueva ventana de PowerShell |
| `You are not logged into any GitHub hosts` | Sesión expirada | Ejecutar `gh auth login` de nuevo |
| El sitio no se actualiza | GitHub Pages tarda | Esperar 2 minutos y recargar con Ctrl+Shift+R |
| `error: pathspec did not match` | Nombre de archivo con espacios | Poner el nombre entre comillas: `git add "archivo con espacios.pdf"` |
| El PDF no abre en el sitio | No fue incluido en el commit | Verificar con `git status` y hacer `git add nombre.pdf` |

---

## 8. URL de referencia rápida

| Recurso | URL |
|---------|-----|
| Sitio publicado | https://garciasuaza.github.io/assist-ia-research/ |
| Repositorio | https://github.com/garciasuaza/assist-ia-research |
| Configuración de Pages | https://github.com/garciasuaza/assist-ia-research/settings/pages |

# ChemSafe Vision - Resumen del Proyecto

## Descripción General
App móvil 100% offline para seguridad industrial química que identifica productos mediante OCR/cámara, muestra requisitos EPP, Fichas de Datos de Seguridad (FDS) y medidas de emergencia.

---

## 🎯 Funcionalidades Implementadas

### Módulos principales:
1. **Dashboard** - Panel con estadísticas y escaneos recientes
2. **Scanner** - Simulación de escaneo OCR con selección rápida de químicos
3. **Base de Datos de Químicos** - Lista de productos con cards detalladas
4. **Detalle de Químico** - Información completa: peligros, primeros auxilios, EPP, almacenamiento, descarga de FDS
5. **Catálogo EPP** - Equipos de protección por tipo de químico
6. **Historial** - Registro de escaneos
7. **PWA** - Progressive Web App instalable en Android

### Base de datos actual:
- 3 químicos registrados: Ácido Sulfúrico, Hipoclorito de Sodio, Acetona
- Cada químico tiene: nombre, CAS, fórmula, nivel de riesgo, peligros, primeros auxilios, almacenamiento, 4 EPP, FDS PDF

---

## 📁 Estructura de Archivos

### En GitHub:
```
chem-safe-vision/ (repo)
├── index.html              → App principal (carga dinámica desde chemicals.json)
├── chemicals.json          → Base de datos de químicos (EDITAR PARA AGREGAR)
├── manifest.json           → Configuración PWA
├── sw.js                   → Service Worker (actualizaciones automáticas)
├── demo.html               → Versión anterior (no usar)
├── assets/                 → Imágenes y PDFs
│   ├── acido sulfurico.png
│   ├── Hipoclorito de Sodio.png
│   ├── FDS_Acetona.pdf
│   ├── FDS_acido sulfurico.pdf
│   └── FDS_Hipoclorito de Sodio.pdf
└── amazon-package/          → Proyecto Android para APK
    ├── app/
    │   ├── build.gradle
    │   └── src/main/
    │       ├── AndroidManifest.xml
    │       ├── java/com/chemsafe/vision/MainActivity.java
    │       └── res/...
    └── README.md
```

### En computadora local:
```
C:\Users\Estudiante 08\Documents\Pedro_Noriega\PROYECTOS_IA\OpenCode\
├── index.html
├── chemicals.json
├── manifest.json
├── sw.js
├── demo.html
├── chemicals.json
├── upload.ps1
├── upload-amazon.ps1
├── assets/
│   ├── acido sulfurico.png
│   ├── Hipoclorito de Sodio.png
│   ├── FDS_*.pdf
│   └── epp/ (vacío)
└── amazon-package/ (completo)
```

---

## 🌐 URLs del Proyecto

- **PWA en GitHub Pages:** https://pedronoriega-eng.github.io/chem-safe-vision/
- **Repo GitHub:** https://github.com/pedronoriega-eng/chem-safe-vision

---

## 🔧 Cómo Agregar Nuevos Químicos

### Solo 3 pasos:

#### 1. Subir imagen y PDF al repo
- Ve a: https://github.com/pedronoriega-eng/chem-safe-vision
- Click **Add file** → **Upload files**
- Sube `nombre-quimico.png` (imagen del químico)
- Sube `FDS_nombre-quimico.pdf` (ficha de seguridad)
- Commit a main

#### 2. Editar chemicals.json
- Ve a: https://github.com/pedronoriega-eng/chem-safe-vision/edit/main/chemicals.json
- Agrega al final (antes del `]` final):

```json
,
{
  "id": "nuevo-quimico",
  "name": "Nombre del Químico",
  "cas": "XXXXX-XX-X",
  "formula": "XYZ",
  "riskLevel": "Alto",
  "hazardClass": "CORROSIVO",
  "gradient": "from-red-600 to-red-800",
  "image": "nombre-quimico.png",
  "fdsFile": "FDS_nombre-quimico.pdf",
  "hazards": "Descripción de peligros...",
  "firstAid": {
    "inhalation": "...",
    "skin": "...",
    "eyes": "...",
    "ingestion": "..."
  },
  "storage": "Instrucciones de almacenamiento...",
  "epp": [
    { "name": "EPP 1", "desc": "Descripción", "color": "blue" },
    { "name": "EPP 2", "desc": "Descripción", "color": "green" },
    { "name": "EPP 3", "desc": "Descripción", "color": "orange" },
    { "name": "EPP 4", "desc": "Descripción", "color": "purple" }
  ]
}
```

#### 3. Esperar 1-2 minutos
La app se actualiza automáticamente.

---

## 🎨 Personalización

### Colores para gradient (headers de químicos):
- `from-red-600 to-red-800` - Rojo (Alto riesgo)
- `from-orange-500 to-amber-600` - Naranja (Medio riesgo)
- `from-blue-500 to-indigo-600` - Azul (Bajo riesgo)
- `from-green-500 to-emerald-600` - Verde
- `from-purple-500 to-violet-600` - Púrpura

### Colores para EPP:
- `blue`, `green`, `orange`, `purple`, `yellow`, `red`, `slate`

---

## 📱 Publicación en Amazon AppStore

### Estado: Proyecto Android listo en `amazon-package/`

### Pasos para generar APK:
1. Descargar el repo de GitHub
2. Abrir carpeta `amazon-package` en Android Studio
3. Generar APK: Build → Build APK
4. Firmar APK (obligatorio para Amazon)
5. Subir a Amazon Developer Console: https://developer.amazon.com/

### Documentación completa en:
`amazon-package/README.md`

---

## 🔄 Sistema de Actualización

### PWA (GitHub Pages):
- Cuando actualizas `chemicals.json` o `index.html` en GitHub
- El Service Worker detecta cambios
- Muestra notificación "Nueva versión disponible"
- Usuario acepta y se actualiza

### APK (Amazon):
- La app carga la PWA desde GitHub
- No necesita actualizar el APK cuando la PWA cambia

---

## ⚠️ Notas Importantes

1. **No editar `index.html` directamente** - Está configurado para cargar desde `chemicals.json`
2. **Solo editar `chemicals.json`** para agregar/modificar químicos
3. **Imágenes en `assets/`** - Deben subirse manualmente al repo
4. **FDS PDFs** - Están en `assets/` con prefijo `FDS_`

---

## 🛠️ Tecnologías Usadas

- **Frontend:** HTML5, CSS3 (Tailwind CSS), JavaScript ES6
- **PWA:** Service Worker, Web App Manifest
- **Alojamiento:** GitHub Pages (gratis)
- **Base de datos:** JSON (chemicals.json)
- **Mobile:** Android Studio + WebView wrapper
- **Distribución:** Amazon AppStore (gratis)

---

## 📋 Pendiente / Mejoras Futuras

1. [ ] Agregar imagen de acetona (no existe `acetona.png`)
2. [ ] Agregar más químicos a la base de datos
3. [ ] Crear iconos de EPP reales (carpeta `assets/epp/` vacía)
4. [ ] Generar APK firmado y subir a Amazon AppStore
5. [ ] Implementar OCR real con ML Kit (actualmente simulado)
6. [ ] Agregar autenticación de usuarios
7. [ ] Sincronización de historial entre dispositivos
8. [ ] Agregar más idiomas (actualmente solo español)

---

## 🔑 Token de GitHub (para acceso programático)

**NOTA:** Generar nuevo token en:
https://github.com/settings/tokens
- Seleccionar permisos: `repo` (Full control of private repositories)

**Nota de seguridad:** No guardar tokens en archivos del repo. Usar variables de entorno.

---

## 📞 Comandos Útiles

### Subir archivos a GitHub (PowerShell):
```powershell
# Desde carpeta OpenCode
$headers = @{"Authorization" = "token TOKEN"; Accept = "application/vnd.github.v3+json"}
$baseUri = "https://api.github.com/repos/pedronoriega-eng/chem-safe-vision/contents"
$content = [Convert]::ToBase64String([System.IO.File]::ReadAllBytes("archivo"))
Invoke-RestMethod -Uri "$baseUri/archivo" -Method PUT -Headers $headers -ContentType "application/json" -Body ([System.Text.Encoding]::UTF8.GetBytes(@{"message" = "Update"; "content" = $content} | ConvertTo-Json -Compress))
```

---

## 📅 Fecha de creación del proyecto
30 de Abril de 2026

## 👤 Desarrollador
Pedro Noriega / pedronoriega-eng

---

*Este documento sirve como referencia para continuar el desarrollo en futuras sesiones.*
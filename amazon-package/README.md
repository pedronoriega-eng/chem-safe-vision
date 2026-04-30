# ChemSafe Vision - Amazon AppStore Package

## Descripción

Este proyecto es un wrapper de Android (APK) que carga la PWA de ChemSafe Vision desde GitHub Pages.

**URL de la PWA:** https://pedronoriega-eng.github.io/chem-safe-vision/

---

## 📦 Archivos incluidos

```
amazon-package/
├── app/
│   ├── build.gradle              (configuración del módulo)
│   └── src/main/
│       ├── AndroidManifest.xml   (permisos y declaración de actividad)
│       ├── java/com/chemsafe/vision/
│       │   └── MainActivity.java (WebView que carga la PWA)
│       └── res/
│           ├── layout/activity_main.xml
│           └── values/ (colors, strings, themes)
├── build.gradle                  (configuración del proyecto)
├── settings.gradle
├── gradle.properties
└── gradle/wrapper/gradle-wrapper.properties
```

---

## 🚀 Cómo construir el APK

### Opción 1: Android Studio (Más fácil)

1. **Descarga e instala Android Studio:**
   https://developer.android.com/studio

2. **Abre el proyecto:**
   - File → Open
   - Selecciona la carpeta `amazon-package`

3. **Espera a que Gradle sincronice**

4. **Conecta tu celular Android** o inicia un emulador

5. **Genera el APK:**
   - Build → Build Bundle(s) / APK(s) → Build APK(s)
   - El APK estará en: `app/build/outputs/apk/debug/app-debug.apk`

---

### Opción 2: Línea de comandos

1. **Instala Android SDK** y configura `ANDROID_HOME`

2. **Instala Gradle** (o usa el wrapper incluido)

3. **Ejecuta:**
   ```bash
   cd amazon-package
   ./gradlew assembleDebug
   ```

4. **El APK estará en:**
   `app/build/outputs/apk/debug/app-debug.apk`

---

## 🔐 Cómo firmar el APK (OBLIGATORIO para Amazon)

Amazon AppStore requiere que el APK esté **firmado digitalmente**.

### Crear un keystore (solo una vez):

```bash
keytool -genkey -v -keystore chemsafe-vision.keystore -alias chemsafe-vision -keyalg RSA -keysize 2048 -validity 10000
```

### Firmar el APK:

```bash
jarsigner -verbose -sigalg SHA1withRSA -digestalg SHA1 -keystore chemsafe-vision.keystore app.apk chemsafe-vision
```

### Verificar la firma:

```bash
jarsigner -verify -verbose -certs app.apk
```

---

## 📱 Publicar en Amazon AppStore

### 1. Crear cuenta de desarrollador
- Ve a: https://developer.amazon.com/
- Regístrate gratuitamente
- Completa tu perfil de desarrollador

### 2. Crear nueva app en Amazon Developer Console
1. Click **Add new App**
2. Selecciona **Android** como plataforma
3. Completa la información:
   - **Title:** ChemSafe Vision
   - **Category:** Education
   - **Price:** Free (o tu precio)
   - **Languages:** Spanish

### 3. Subir assets
- **Screenshots:** Tomar capturas de la app
- **Icon:** 512x512 PNG
- **Description:** Descripción de la app
- **Keywords:** chemical safety, safety, EPP, FDS

### 4. Subir el APK
1. En **App File**, click **Upload**
2. Selecciona tu APK firmado

### 5. Configurar clasificación de contenido
- Responde el cuestionario de clasificación de contenido
- ChemSafe no contiene contenido para adultos

### 6. Enviar para revisión
- Click **Submit App**
- Amazon revisa en 1-3 días
- Recibirás email cuando sea aprobado

---

## ⚠️ IMPORTANTE: Cambiar la URL de la PWA

Antes de compilar, **edita `MainActivity.java`** y cambia la URL si es diferente:

```java
webView.loadUrl("https://TU-USUARIO.github.io/TU-REPO/");
```

---

## 🔄 Actualizaciones

Cuando actualices la PWA en GitHub Pages:
1. No necesitas recompilar el APK
2. Los usuarios con la app instalada verán los cambios automáticamente
3. La app siempre carga la versión más reciente de GitHub Pages

---

## 📋 Requisitos

- Android Studio 2023.1+ (para desarrollo)
- Java JDK 11+
- Android SDK 34
- Min SDK: 21 (Android 5.0)
- Target SDK: 34 (Android 14)

---

## 💡 Tips

1. **Test en tu celular** antes de subir a Amazon
2. **Usa el APK debug** para pruebas
3. **Firma siempre con el mismo keystore** para actualizaciones
4. **Guarda el keystore en lugar seguro** - si lo pierdes, no podrás actualizar la app

---

## ❓ Problemas comunes

### Error: "minSdkVersion is not set"
Agrega esto en `app/build.gradle`:
```groovy
defaultConfig {
    minSdk 21
    targetSdk 34
}
```

### Error: "Gradle sync failed"
- Asegúrate de tener Java JDK instalado
- Verifica que ANDROID_HOME esté configurado

### Amazon rechaza el APK
- Verifica que esté firmado correctamente
- Asegúrate de que la URL de la PWA sea HTTPS (no HTTP)
- Revisa las políticas de contenido de Amazon

---

**¿Necesitas ayuda con algún paso específico?**
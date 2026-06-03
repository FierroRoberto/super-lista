# 🛒 Lista del Súper — Guía de instalación en GitHub Pages

## Estructura de archivos

```
/
├── index.html                      ← App completa
├── manifest.json                   ← PWA manifest
├── sw.js                           ← Service Worker (offline)
├── _config.yml                     ← Config Jekyll para GitHub Pages
├── .nojekyll                       ← Desactiva procesamiento Jekyll
├── super_estado.json               ← Sube este archivo a Google Drive
├── icons/
│   ├── icon-72.png  … icon-512.png ← Íconos de la app
│   └── screenshot-mobile.png       ← Screenshot para el manifest
└── .github/
    └── workflows/
        └── deploy.yml              ← Deploy automático a GitHub Pages
```

---

## ① Subir a GitHub y publicar

### Opción A — GitHub Desktop (sin terminal)
1. Descarga **[GitHub Desktop](https://desktop.github.com)**
2. File → New Repository → nombre: `super-lista` → Create
3. Arrastra **todos los archivos** (incluyendo carpeta `icons/` y `.github/`) a la carpeta del repo
4. Escribe un mensaje de commit (ej. "Primera versión") → **Commit to main**
5. Repository → **Publish repository** (desactiva "Keep this code private" si quieres gratis)
6. Ve a github.com → tu repo → **Settings → Pages**
7. Source: **GitHub Actions** → Save
8. En ~2 minutos tu URL será: `https://TU-USUARIO.github.io/super-lista/`

### Opción B — Terminal (más rápido)
```bash
cd carpeta-del-proyecto
git init
git add .
git commit -m "Lista del Súper v1"
gh repo create super-lista --public --push --source=.
```
Luego en GitHub: **Settings → Pages → Source: GitHub Actions → Save**

---

## ② Instalar como app en los celulares

### Android (Chrome)
1. Abre `https://TU-USUARIO.github.io/super-lista/` en Chrome
2. Aparece automáticamente un banner "Agregar a pantalla de inicio"
   - Si no aparece: menú ⋮ → **"Instalar app"** o **"Agregar a pantalla de inicio"**
3. Confirma → ícono verde en tu pantalla de inicio ✅

### iOS (Safari — obligatorio)
1. Abre la URL en **Safari** (no Chrome ni otro navegador)
2. Toca el botón **Compartir** ↑ en la barra inferior
3. Desplázate → **"Agregar a pantalla de inicio"**
4. Edita el nombre si quieres → **Agregar** ✅

> La app funciona **offline** una vez instalada. Los cambios se guardan localmente
> y se sincronizan con Drive cuando hay conexión.

---

## ③ Configurar Google Drive (sincronización entre 2 dispositivos)

### Crear el archivo de estado en Drive
1. Ve a [drive.google.com](https://drive.google.com)
2. Sube el archivo **`super_estado.json`** incluido en este proyecto
3. Clic derecho → **"Obtener vínculo"** → cambia a **"Cualquier persona con el vínculo puede editar"**
4. Copia la URL → el **File ID** es la parte entre `/d/` y `/view`:
   ```
   https://drive.google.com/file/d/ ►ESTE_ES_EL_FILE_ID◄ /view
   ```

### Obtener el Access Token
1. Ve a [developers.google.com/oauthplayground](https://developers.google.com/oauthplayground)
2. Lado izquierdo → **Drive API v3** → marca **`drive.file`**
3. Clic **"Authorize APIs"** → inicia sesión con tu cuenta Google
4. Clic **"Exchange authorization code for tokens"**
5. Copia el **Access token** (empieza con `ya29.`)

### Conectar la app
1. Abre la app → toca **⚙️** (esquina superior derecha)
2. Toca **"Obtener token con Google"** o pega el token manualmente
3. Pega el **File ID**
4. **"Guardar y conectar"** → el punto sync se pone verde ✅
5. Repite en el segundo celular con el **mismo File ID**

> ⚠️ El token dura ~1 hora. La app te avisa cuando está por expirar.
> Toca ⚙️ → "🔄 Renovar Access Token" para renovarlo.

---

## ④ Cómo usar la app

| Acción | Cómo |
|--------|------|
| Marcar artículo comprado | Toca el artículo |
| Resetear una tienda | Botón **↺ Reset** en la cabecera de cada tienda |
| Editar piezas o precio | Toca **✏️** → usa los botones − / + y el campo de precio |
| Agregar artículo nuevo | Toca el botón verde **＋ Agregar artículo** (parte inferior) |
| Sincronizar manualmente | Toca **↻ Sync** en la barra de sincronización |
| Renovar token Drive | Toca **⚙️** → "🔄 Renovar Access Token" |
| Ver total general | Pestaña **"Todas"** → banner negro en la parte superior |

---

## ⑤ Solución de problemas

| Problema | Solución |
|----------|----------|
| La app no se instala en Android | Asegúrate de estar en HTTPS (GitHub Pages lo hace automático) |
| La app no se instala en iOS | Usa Safari, no Chrome |
| Punto sync rojo | El token expiró — toca ⚙️ para renovarlo |
| Los cambios no llegan al otro celular | Verifica que ambos usen el mismo File ID |
| La app se ve en blanco | Borra caché del navegador y recarga |
| Error 404 en GitHub Pages | Espera 2-3 minutos después del deploy |

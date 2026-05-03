# 🚀 GUÍA RÁPIDA - Halladey POS para Netlify + Firestore

## TIEMPO ESTIMADO: 5 minutos

---

## PASO 1: Crear Proyecto Firebase (2 min)

1. Ve a [console.firebase.google.com](https://console.firebase.google.com/)
2. Click **"Crear un proyecto"**
3. Nombra tu proyecto (ej: `mi-negocio-pos`)
4. **Desactiva** Google Analytics (más rápido)
5. Click **"Crear proyecto"**
6. Espera ~30 segundos

---

## PASO 2: Obtener Credenciales (1 min)

1. En el dashboard del proyecto, click el **⚙️ icono de engranaje** → "Configuración del proyecto"
2. Ve a la pestaña **"General"**
3. En "Tus apps", click **"</>"** (icono de web)
4. Registra la app con un nickname (ej: `halladey-web`)
5. **NO** habilites Firebase Hosting
6. Click **"Registrar app"**
7. Copia el objeto `firebaseConfig` que aparece

---

## PASO 3: Pegar Credenciales (1 min)

Abre `index.html` y reemplaza el bloque `firebaseConfig`:

```javascript
// ANTES (líneas ~15-22):
const firebaseConfig = {
    apiKey: "TU_API_KEY",
    authDomain: "TU_PROYECTO.firebaseapp.com",
    projectId: "TU_PROYECTO",
    storageBucket: "TU_PROYECTO.appspot.com",
    messagingSenderId: "TU_SENDER_ID",
    appId: "TU_APP_ID"
};

// DESPUÉS (pega tu configuración real):
const firebaseConfig = {
    apiKey: "AIzaSyB...",
    authDomain: "mi-negocio-pos.firebaseapp.com",
    projectId: "mi-negocio-pos",
    storageBucket: "mi-negocio-pos.appspot.com",
    messagingSenderId: "123456789",
    appId: "1:123456789:web:abcdef123456"
};
```

---

## PASO 4: Configurar Firestore (1 min)

1. En el menú lateral, click **"Firestore Database"**
2. Click **"Crear base de datos"**
3. Selecciona **"Iniciar en modo de prueba"** ✓
4. Click **"Siguiente"**
5. Selecciona la región más cercana (recomendado: `us-central` o `southamerica-east1`)
6. Click **"Habilitar"**

### Configurar Reglas de Seguridad:

1. Ve a Firestore Database → **"Reglas"**
2. Reemplaza todo con:

```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /{document=**} {
      allow read, write: if request.auth != null;
    }
  }
}
```

3. Click **"Publicar"**

---

## PASO 5: Habilitar Autenticación Anónima (30 seg)

1. Menú lateral → **"Authentication"**
2. Click **"Comenzar"**
3. Ve a la pestaña **"Método de inicio de sesión"**
4. Busca **"Anónimo"** → Click **"Habilitar"**
5. Click **"Guardar"**

---

## PASO 6: Deploy en Netlify (30 seg)

### Opción A: Drag & Drop (MÁS RÁPIDO)

1. Ve a [app.netlify.com/drop](https://app.netlify.com/drop)
2. Arrastra el archivo `halladey-pos-netlify.zip`
3. ¡Listo! Copia la URL que te dan

### Opción B: Git (RECOMENDADO)

1. Crea repo en GitHub con estos archivos
2. Ve a [app.netlify.com](https://app.netlify.com)
3. Click **"Add new site"** → **"Import an existing project"**
4. Conecta tu cuenta de GitHub
5. Selecciona el repositorio
6. Configuración:
   - **Build command**: (vacío)
   - **Publish directory**: `/` (raíz)
7. Click **"Deploy site"**

---

## ✅ VERIFICACIÓN

Abre tu URL de Netlify y deberías ver:

1. **Pantalla de login** → Ingresa nombre de vendedor
2. **Dashboard** → Con estadísticas en tiempo real
3. **Punto de Venta** → Con productos de ejemplo
4. **Datos sincronizados** entre dispositivos

---

## 🔐 PRIMER ACCESO

- **PIN de Admin**: `1234` (para acceso administrativo)
- **Vendedores**: Solo necesitan nombre (autenticación anónima)
- **Datos demo**: Se cargan automáticamente si Firestore está vacío

---

## 💰 COSTOS (Firebase Spark = GRATIS)

| Servicio | Límite Gratis |
|----------|--------------|
| Firestore | 50,000 lecturas/día |
| Auth | 10,000 usuarios/mes |
| Netlify | 100GB/mes |

---

## 🆘 SOLUCIÓN DE PROBLEMAS

### "Error: Firebase app not initialized"
→ Verifica que las credenciales estén correctas

### "Permission denied"
→ Revisa las reglas de Firestore (deben permitir `request.auth != null`)

### "No hay productos"
→ Espera 10 segundos, los datos demo se cargan automáticamente

### Pantalla en blanco
→ Abre Consola del navegador (F12) y revisa errores rojos

---

**¡Listo para vender! 🎉**

# 🛒 Halladey POS - Sistema de Gestión

Sistema completo de **Inventario + Punto de Venta** con sincronización en tiempo real vía **Firebase Firestore**.

## 🚀 Deploy en 5 minutos

### Requisitos previos
- Cuenta de Google (Gmail)
- Navegador moderno (Chrome, Firefox, Edge)

### Paso 1: Crear proyecto Firebase

1. Ve a [Firebase Console](https://console.firebase.google.com/)
2. Click **"Crear un proyecto"** [^20^]
3. Nombra tu proyecto y desactiva Google Analytics
4. Espera a que se cree

### Paso 2: Obtener credenciales

1. En el dashboard, click **⚙️ Configuración del proyecto > General**
2. En "Tus apps", click **"</>"** (icono web)
3. Registra la app con un nickname
4. Copia el objeto `firebaseConfig`

### Paso 3: Configurar Firestore

1. Menú lateral → **Firestore Database**
2. Click **"Crear base de datos"**
3. Selecciona **"Iniciar en modo de prueba"**
4. Elige tu región (recomendado: `us-central`)
5. Ve a la pestaña **"Reglas"** y pega:

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

### Paso 4: Habilitar Auth Anónima

1. Menú lateral → **Authentication**
2. Pestaña **"Método de inicio de sesión"**
3. Habilita **"Anónimo"**
4. Click **"Guardar"**

### Paso 5: Pegar credenciales en index.html

Abre `index.html` y reemplaza el bloque `firebaseConfig` (líneas ~15-22) con tus credenciales reales.

### Paso 6: Deploy en Netlify

#### Opción A: Drag & Drop (30 segundos) [^23^]
1. Ve a [app.netlify.com/drop](https://app.netlify.com/drop)
2. Arrastra el ZIP con `index.html` + `netlify.toml`
3. ¡Listo! Copia tu URL

#### Opción B: Git (recomendado para CI/CD) [^10^]
1. Sube a un repo de GitHub
2. En Netlify: **"Add new site > Import an existing project"**
3. Conecta tu repo
4. **Build command**: (vacío)
5. **Publish directory**: `/`
6. Click **"Deploy site"**

---

## 📁 Archivos incluidos

| Archivo | Propósito |
|---------|-----------|
| `index.html` | App completa (SPA) - 115KB |
| `netlify.toml` | Configuración SPA routing + headers |
| `firestore.rules` | Reglas de seguridad para copiar |
| `firebase-config.js` | Template de configuración |
| `README.md` | Esta guía |
| `GUIA_RAPIDA.md` | Pasos rápidos sin explicaciones |

---

## 🔥 Características de Firestore

- ✅ **Sincronización en tiempo real** - onSnapshot listeners [^20^]
- ✅ **Persistencia offline** automática
- ✅ **Autenticación anónima** - sin contraseñas para vendedores
- ✅ **Batch writes** - ventas atómicas seguras
- ✅ **Escalabilidad automática** - de 1 a 1000+ usuarios

---

## 🎨 Funcionalidades

### Inventario
- CRUD productos y categorías
- Alertas de stock bajo/sin stock
- Movimientos: entrada, salida, ajuste
- Reportes de valoración
- Export/Import JSON

### Punto de Venta
- Interfaz táctil optimizada
- Carrito con cantidades
- Múltiples métodos de pago (Efectivo, Tarjeta, Transferencia)
- Tickets imprimibles
- Cierre de caja por vendedor

### Dashboard
- Métricas en tiempo real
- Stock por categoría (gráfico)
- Ventas del día
- Valor del inventario

---

## 🔐 Seguridad

- **PIN Admin**: `1234` (cambiable en código)
- **Auth anónima** de Firebase para vendedores
- **Reglas Firestore** protegen datos
- **HTTPS automático** en Netlify

---

## 💰 Costos

| Servicio | Gratis hasta | Después |
|----------|-------------|---------|
| Firebase Auth | 10,000 usuarios/mes | Gratis ilimitado |
| Firestore | 50,000 lecturas/día | $0.06/100K |
| Netlify Hosting | 100GB/mes | $19/mes Pro [^19^] |

---

## 🛠️ Personalización

### Cambiar PIN de admin
Busca en `index.html`:
```javascript
isAdmin = pin === '1234';
```

### Cambiar moneda
En Configuración de la app, o editando `settingsRef` en Firestore.

### Desactivar datos demo
Comenta la llamada a `seedDemoDataIfEmpty()` en el código.

---

## 📱 Compatibilidad

- Chrome/Edge/Firefox/Safari (últimas 2 versiones)
- iOS Safari 14+
- Android Chrome 90+
- Optimizado para tablets (POS táctil)
- Responsive: mobile, tablet, desktop

---

## 🆘 Soporte

Problemas comunes:

| Problema | Solución |
|----------|----------|
| "Firebase not initialized" | Verifica credenciales |
| "Permission denied" | Revisa reglas de Firestore |
| Pantalla en blanco | F12 → Consola → revisa errores |
| Sin productos | Espera 10s, datos demo se cargan |
| No sincroniza | Verifica conexión a internet |

---

**Hecho con ❤️ para pequeños negocios**

# Guía de Despliegue en Vercel

## Opción 1: Despliegue desde GitHub (Recomendado)

### Paso 1: Subir a GitHub

1. Inicializa Git (si no lo has hecho):
   ```bash
   git init
   git add .
   git commit -m "Initial commit: Currículum web"
   ```

2. Crea un repositorio en GitHub y conéctalo:
   ```bash
   git remote add origin https://github.com/tu-usuario/tu-repositorio.git
   git branch -M main
   git push -u origin main
   ```

### Paso 2: Desplegar en Vercel

1. Ve a [vercel.com](https://vercel.com) e inicia sesión con GitHub
2. Haz clic en "Add New Project"
3. Importa tu repositorio de GitHub
4. Vercel detectará automáticamente que es un proyecto Nuxt
5. Configuración automática:
   - **Framework Preset**: Nuxt.js (detectado automáticamente)
   - **Build Command**: `npm run build` (automático)
   - **Output Directory**: `.output` (automático)
   - **Install Command**: `npm install` (automático)
6. Haz clic en "Deploy"

¡Listo! Tu sitio estará disponible en unos minutos.

---

## Opción 2: Despliegue con Vercel CLI

### Paso 1: Instalar Vercel CLI

```bash
npm install -g vercel
```

### Paso 2: Iniciar sesión

```bash
vercel login
```

### Paso 3: Desplegar

```bash
vercel
```

Sigue las instrucciones en la terminal. Para producción:

```bash
vercel --prod
```

---

## Configuración Automática

El proyecto ya incluye:
- ✅ `vercel.json` con configuración optimizada
- ✅ `.gitignore` configurado correctamente
- ✅ `nuxt.config.ts` optimizado para Vercel

Vercel detectará automáticamente:
- Framework: Nuxt.js
- Build command: `npm run build`
- Output directory: `.output`

---

## Variables de Entorno (si las necesitas)

Si necesitas variables de entorno:

1. Ve a tu proyecto en Vercel
2. Settings → Environment Variables
3. Agrega las variables necesarias

---

## Dominio Personalizado

1. Ve a tu proyecto en Vercel
2. Settings → Domains
3. Agrega tu dominio personalizado
4. Sigue las instrucciones de DNS

---

## Notas Importantes

- ✅ El proyecto está configurado para SSR (Server-Side Rendering)
- ✅ Vercel detecta automáticamente Nuxt 3
- ✅ Los archivos estáticos en `public/` se sirven automáticamente
- ✅ Cada push a la rama `main` desplegará automáticamente (si configuras GitHub integration)

---

## Solución de Problemas

### Error de build
- Verifica que todas las dependencias estén en `package.json`
- Revisa los logs en Vercel Dashboard

### Imágenes no se muestran
- Asegúrate de que las imágenes estén en la carpeta `public/`
- Usa rutas relativas desde la raíz: `/imagen.jpg`

### Rutas no funcionan
- Verifica que `nuxt.config.ts` tenga `ssr: true`
- Las rutas de Nuxt funcionan automáticamente con Vercel


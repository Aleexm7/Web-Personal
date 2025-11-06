# Instrucciones de Personalización

Este documento te guiará para personalizar tu currículum web con tu información.

## 📋 Pasos Iniciales

1. **Instalar dependencias:**
   ```bash
   npm install
   ```

2. **Iniciar el servidor de desarrollo:**
   ```bash
   npm run dev
   ```

3. **Abrir en el navegador:**
   Navega a `http://localhost:3000`

## 🖼️ Agregar Imágenes

### Foto de Perfil
1. Coloca tu foto en la carpeta `public/` con el nombre `profile.jpg`
2. Recomendado: formato JPG o PNG, tamaño mínimo 500x500px
3. La imagen debe ser cuadrada para mejor resultado

### Imágenes de Proyectos
1. Coloca las imágenes de tus proyectos en la carpeta `public/`
2. Actualiza las rutas en `pages/proyectos.vue` en el array `projects`

## ✏️ Personalizar Contenido

### 1. Página de Inicio (`pages/index.vue`)

Edita las siguientes variables en el `<script setup>`:

- **`name`**: Tu nombre completo
- **`title`**: Tu título profesional (ej: "Desarrollador Full Stack")
- **`description`**: Tu descripción profesional breve
- **`experience`**: Array con tu experiencia laboral
- **`education`**: Array con tus estudios
- **`certifications`**: Array con tus certificaciones
- **`languages`**: Array con tus idiomas y niveles

Ejemplo de estructura:
```javascript
const experience = [
  {
    position: 'Desarrollador Full Stack',
    company: 'Nombre de la Empresa',
    period: '2022 - Presente',
    description: 'Descripción de tus responsabilidades...',
    responsibilities: [
      'Responsabilidad 1',
      'Responsabilidad 2'
    ]
  }
]
```

### 2. Página de Proyectos (`pages/proyectos.vue`)

Edita el array `projects` con tus proyectos:

```javascript
const projects = [
  {
    title: 'Nombre del Proyecto',
    description: 'Descripción del proyecto',
    image: '/ruta-a-imagen.jpg',
    technologies: ['Vue.js', 'Nuxt', 'TypeScript'],
    github: 'https://github.com/tu-usuario/proyecto',
    demo: 'https://demo-proyecto.com' // o null si no hay demo
  }
]
```

### 3. Página de Contacto (`pages/contacto.vue`)

Edita el array `contacts` con tus enlaces reales:

```javascript
const contacts = [
  {
    name: 'GitHub',
    description: 'Revisa mis repositorios y proyectos',
    url: 'https://github.com/tu-usuario-real', // ⬅️ Cambia esto
    icon: GitHubIcon,
    color: '#24292e'
  },
  // ... más contactos
]
```

## 🎨 Personalizar Estilos

Los estilos principales están en `assets/css/main.css`. Puedes modificar:

- **Colores**: Variables CSS en `:root`
- **Tipografía**: Fuentes y tamaños
- **Espaciado**: Padding y margins
- **Efectos**: Sombras, transiciones, etc.

## 🚀 Desplegar

### Generar sitio estático:
```bash
npm run generate
```

Los archivos generados estarán en la carpeta `.output/public/`

### Opciones de despliegue:
- **Vercel**: Conecta tu repositorio Git
- **Netlify**: Arrastra la carpeta `.output/public/`
- **GitHub Pages**: Sube los archivos a tu repositorio
- **Cualquier hosting estático**: Sube los archivos de `.output/public/`

## 📝 Notas Adicionales

- Todas las imágenes deben estar en la carpeta `public/`
- Los enlaces externos deben incluir `target="_blank"` y `rel="noopener noreferrer"` (ya incluidos)
- El diseño es completamente responsive
- Puedes agregar más secciones editando `pages/index.vue`

## 🔧 Solución de Problemas

Si encuentras algún error:
1. Verifica que todas las rutas de imágenes sean correctas
2. Asegúrate de que los enlaces externos sean válidos
3. Revisa la consola del navegador para errores
4. Ejecuta `npm run build` para verificar errores de compilación


<template>
  <div class="projects-page">
    <section class="projects section">
      <div class="container">
        <h1 class="page-title">Mis Proyectos</h1>
        <p class="page-subtitle">Una selección de proyectos que he desarrollado</p>
        
        <div class="projects-grid">
          <div v-for="(project, index) in projects" :key="index" class="project-card card">
            <div class="project-image">
              <img :src="project.image" :alt="project.title" />
            </div>
            <div class="project-content">
              <h3 class="project-title">{{ project.title }}</h3>
              <p class="project-description">{{ project.description }}</p>
              
              <div class="project-technologies">
                <span 
                  v-for="(tech, i) in project.technologies" 
                  :key="i" 
                  class="tech-tag"
                >
                  {{ tech }}
                </span>
              </div>
              
              <div class="project-links">
                <a 
                  v-if="project.github" 
                  :href="project.github" 
                  target="_blank" 
                  rel="noopener noreferrer"
                  class="project-link"
                >
                  <svg width="20" height="20" viewBox="0 0 24 24" fill="currentColor">
                    <path d="M12 0c-6.626 0-12 5.373-12 12 0 5.302 3.438 9.8 8.207 11.387.599.111.793-.261.793-.577v-2.234c-3.338.726-4.033-1.416-4.033-1.416-.546-1.387-1.333-1.756-1.333-1.756-1.089-.745.083-.729.083-.729 1.205.084 1.839 1.237 1.839 1.237 1.07 1.834 2.807 1.304 3.492.997.107-.775.418-1.305.762-1.604-2.665-.305-5.467-1.334-5.467-5.931 0-1.311.469-2.381 1.236-3.221-.124-.303-.535-1.524.117-3.176 0 0 1.008-.322 3.301 1.23.957-.266 1.983-.399 3.003-.404 1.02.005 2.047.138 3.006.404 2.291-1.552 3.297-1.23 3.297-1.23.653 1.653.242 2.874.118 3.176.77.84 1.235 1.911 1.235 3.221 0 4.609-2.807 5.624-5.479 5.921.43.372.823 1.102.823 2.222v3.293c0 .319.192.694.801.576 4.765-1.589 8.199-6.086 8.199-11.386 0-6.627-5.373-12-12-12z"/>
                  </svg>
                  GitHub
                </a>
                <a 
                  v-if="project.demo" 
                  :href="project.demo" 
                  target="_blank" 
                  rel="noopener noreferrer"
                  class="project-link"
                >
                  <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                    <path d="M18 13v6a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2V8a2 2 0 0 1 2-2h6"></path>
                    <polyline points="15 3 21 3 21 9"></polyline>
                    <line x1="10" y1="14" x2="21" y2="3"></line>
                  </svg>
                  Demo
                </a>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>
  </div>
</template>

<script setup>
// Datos de los poyectos realizados
const projects = [
  {
    title: 'Automatizador de Búsqueda de Repuestos',
    description: 'Desarrollé una aplicación de escritorio en Python utilizando Tkinter, diseñada para automatizar la búsqueda de piezas de automóvil a partir de su referencia. Para ello, implementé técnicas de web scraping con el fin de consultar automáticamente distintos proveedores indicados por el cliente, agilizando así el proceso de búsqueda y reduciendo el tiempo de gestión manual.',
    image: '/img/logo_app_buscador.png',
    technologies: ['Python', 'Tkinter'],
    /* github: 'https://github.com/tu-usuario/proyecto1', */
    demo: null
  },
  
]
</script>

<style scoped>
.projects-page {
  padding-top: 2rem;
}

.page-title {
  font-size: 3rem;
  font-weight: 700;
  color: var(--text-color);
  margin-bottom: 1rem;
  text-align: center;
}

.page-subtitle {
  font-size: 1.25rem;
  color: var(--text-light);
  text-align: center;
  margin-bottom: 3rem;
}

.projects-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(350px, 1fr));
  gap: 2rem;
}

.project-card {
  display: flex;
  flex-direction: column;
  overflow: hidden;
  padding: 0;
}

.project-image {
  width: 100%;
  height: 200px;
  overflow: hidden;
  background: var(--bg-light);
}

.project-image img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: transform 0.3s ease;
}

.project-card:hover .project-image img {
  transform: scale(1.05);
}

.project-content {
  padding: 1.5rem;
}

.project-title {
  font-size: 1.5rem;
  font-weight: 600;
  color: var(--text-color);
  margin-bottom: 0.75rem;
}

.project-description {
  color: var(--text-light);
  margin-bottom: 1.5rem;
  line-height: 1.6;
}

.project-technologies {
  display: flex;
  flex-wrap: wrap;
  gap: 0.5rem;
  margin-bottom: 1.5rem;
}

.tech-tag {
  padding: 0.375rem 0.75rem;
  background: var(--bg-light);
  color: var(--primary-color);
  border-radius: 6px;
  font-size: 0.875rem;
  font-weight: 500;
}

.project-links {
  display: flex;
  gap: 1rem;
  margin-top: auto;
}

.project-link {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  padding: 0.5rem 1rem;
  background: var(--primary-color);
  color: white;
  text-decoration: none;
  border-radius: 6px;
  font-weight: 500;
  transition: background 0.3s ease;
  font-size: 0.875rem;
}

.project-link:hover {
  background: var(--primary-dark);
}

.project-link svg {
  flex-shrink: 0;
}

@media (max-width: 768px) {
  .page-title {
    font-size: 2rem;
  }

  .projects-grid {
    grid-template-columns: 1fr;
  }

  .project-links {
    flex-direction: column;
  }

  .project-link {
    justify-content: center;
  }
}
</style>


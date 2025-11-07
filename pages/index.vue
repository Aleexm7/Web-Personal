<template>
  <div class="home-page">
    <!-- Hero Section -->
    <section class="hero section">
      <div class="container">
        <div class="hero-content">
          <div class="hero-image">
            <img src="/img/profile.png" alt="Foto de perfil" class="profile-img" />
          </div>
          <div class="hero-text">
            <h1 class="hero-title">Hola, soy {{ name }}</h1>
            <p class="hero-subtitle">{{ title }}</p>
            <p class="hero-description">{{ description }}</p>
          </div>
        </div>
      </div>
    </section>

    <!-- Experience Section -->
    <section class="experience section">
      <div class="container">
        <h2 class="section-title">Experiencia Laboral</h2>
        <div class="experience-list">
          <div v-for="(exp, index) in experience" :key="index" class="experience-item card">
            <div class="experience-header">
              <h3 class="experience-title">{{ exp.position }}</h3>
              <span class="experience-period">{{ exp.period }}</span>
            </div>
            <p class="experience-company">{{ exp.company }}</p>
            <p class="experience-description">{{ exp.description }}</p>
            <ul v-if="exp.responsibilities" class="experience-responsibilities">
              <li v-for="(resp, i) in exp.responsibilities" :key="i">{{ resp }}</li>
            </ul>
          </div>
        </div>
      </div>
    </section>

    <!-- Education Section -->
    <section class="education section">
      <div class="container">
        <h2 class="section-title">Estudios</h2>
        <div class="education-list">
          <div v-for="(edu, index) in education" :key="index" class="education-item card">
            <h3 class="education-title">{{ edu.degree }}</h3>
            <p class="education-period">{{ edu.period }}</p>
          </div>
        </div>
      </div>
    </section>

    <!-- Certifications Section -->
    <section class="certifications section">
      <div class="container">
        <h2 class="section-title">Certificaciones</h2>
        <div class="certifications-grid">
          <div v-for="(cert, index) in certifications" :key="index" class="certification-item card">
            <h3 class="certification-title">{{ cert.name }}</h3>
            <p class="certification-issuer">{{ cert.issuer }}</p>
            <p class="certification-date">{{ cert.date }}</p>
            <a v-if="cert.link" :href="cert.link" target="_blank" class="certification-link">Ver certificado</a>
          </div>
        </div>
      </div>
    </section>

    <!-- Languages Section -->
    <section class="languages section">
      <div class="container">
        <h2 class="section-title">Idiomas</h2>
        <div class="languages-list">
          <div v-for="(lang, index) in languages" :key="index" class="language-item card">
            <div class="language-header">
              <h3 class="language-name">{{ lang.name }}</h3>
              <span class="language-level">{{ lang.level }}</span>
            </div>
            <div class="language-bar">
              <div class="language-progress" :style="{ width: lang.percentage + '%' }"></div>
            </div>
          </div>
        </div>
      </div>
    </section>
  </div>
</template>

<script setup>
// Datos personales
const name = 'Alejandro'
const title = 'Muñoz Domínguez'
const description = 'Soy desarrollador de software con más de dos años de experiencia, trabajando tanto en aplicaciones de escritorio como en aplicaciones web. Principalmente he utilizado C#, .NET y WPF, y también he trabajado con React y Vue en la parte web. Además, tengo conocimientos en Java, PHP y Laravel, así como experiencia con bases de datos Oracle y MySQL. Me gusta aplicar buenas prácticas, tengo nociones en el desarrollo de APIs, gestión de bases de datos y aspectos de seguridad. Me considero una persona que aprende rápido, que disfruta trabajar en equipo y que busca mejorar continuamente y aportar valor a los proyectos en los que participo.'
const experience = [
  {
    position: 'Desarrollador Full Stack',
    company: 'Airtificial',
    period: 'Septiembre 2024 - Septiembre 2025',
    description: 'Participé en el desarrollo de una aplicación para Airbus, utilizando C# y .NET, trabajando tanto en la parte visual de la aplicación como en la lógica de negocio y el acceso a datos. Me encargaba de implementar nuevas funcionalidades y corregir errores, organizando y registrando las tareas a través de la plataforma Microsoft ITSM. Además, brindaba soporte a los ingenieros, ayudando a resolver incidencias tanto técnicas como funcionales. ' + 'También trabajé con PL/SQL en Oracle Database, creando y optimizando procedimientos almacenados para mejorar la gestión de las herramientas utilizadas durante las pruebas de los aviones.',

    responsibilities: [
      'Desarrollo de funcionalidades y mantenimiento de la aplicación utilizando C# y .NET.',
      'Diseño y mejora de interfaces de usuario y lógica de negocio.',
      'Corrección de bugs y gestión de tareas en la plataforma Microsoft ITSM.',
      'Soporte técnico a ingenieros, resolviendo incidencias funcionales y técnicas.',
      'Creación y optimización de procedimientos almacenados en PL/SQL sobre Oracle Database para mejorar procesos internos relacionados con las pruebas de los aviones.'
    ]
  },
  {
    position: 'Desarrollador Web',
    company: 'Bidafarma',
    period: 'Marzo 2024 - Junio 2024',
    description: 'Durante mis prácticas del grado, trabajé en el desarrollo de una parte de la web de la empresa orientada a la gestión del inventario de fármacos, mejorando el control y el acceso a la información. Para ello utilicé Java con el framework Liferay, junto con Oracle Database para la gestión de datos. Además, empleé Jira para planificar y hacer seguimiento de las tareas.\n\nContribuí a implementar y mejorar funcionalidades que ayudaron a facilitar la administración y el seguimiento de los productos farmacéuticos de forma más eficiente.',

    responsibilities: [
      'Desarrollo de módulos web orientados a la gestión del inventario de fármacos.',
      'Implementación y mejora de funcionalidades utilizando Java y el framework Liferay.',
      'Gestión y consulta de datos en Oracle Database.',
      'Planificación y seguimiento de tareas mediante Jira.',
      'Optimización del acceso y control de la información para facilitar la administración del inventario.'
    ]
  },
  {
    position: 'Técnico de sistemas',
    company: 'Inerco',
    period: 'Diciembre 2021 - Diciembre 2022',
    description: 'Realicé tareas de soporte técnico, encargándome del diagnóstico y reparación de equipos informáticos tanto a nivel de hardware como de software. También gestionaba el inventario y el etiquetado de los dispositivos para asegurar su correcta identificación.\n\nAdemás, me ocupaba de organizar eventos y reuniones internas, y realizaba tareas de administración en el dominio de la empresa, como la creación de usuarios y la aplicación de políticas en el firewall para garantizar la seguridad de la red.\n\nAsimismo, brindaba atención a los usuarios resolviendo incidencias de forma remota, utilizando asistencia telefónica y sistemas de gestión de tickets.',

    responsibilities: [
      'Diagnóstico y reparación de equipos informáticos (hardware y software).',
      'Gestión y etiquetado de inventario de dispositivos.',
      'Organización de eventos y reuniones internas.',
      'Administración de usuarios en el dominio y aplicación de políticas en el firewall.',
      'Atención y soporte remoto a usuarios mediante teléfono y plataformas de tickets.'
    ]
  }
]

// Educación
const education = [
  {
    degree: 'Grado Superior Desarrollo de Aplicaciones Web',
    period: '2022 - 2024'
  },
  {
    degree: 'Grado Medio de Sistemas Microinformáticos y Redes',
    period: '2020 - 2022'
  }
]

// Certificaciones
const certifications = [
  {
    name: 'Crash Course on Python',
    issuer: 'Google',
    date: '2022',
    link: 'https://www.coursera.org/account/accomplishments/certificate/4UW9LNHH2RCP'
  },
  {
    name: 'Seguridad Informática',
    issuer: 'Google',
    date: '2022',
    link: 'https://www.coursera.org/account/accomplishments/certificate/7MY8P428SLHD'
  },
  {
    name: 'Soporte de Tecnologías de la Información de Google',
    issuer: 'Google',
    date: '2022',
    link: 'https://www.coursera.org/account/accomplishments/specialization/certificate/JXRH3J86KV95'
  },
  {
    name: 'Administración de sistemas y servicios de infraestructura de TI',
    issuer: 'Google',
    date: '2022',
    link: 'https://www.coursera.org/account/accomplishments/certificate/XUKCRYJFJ7W5'
  }
]

// Idiomas
const languages = [
  { name: 'Español', level: 'Nativo', percentage: 100 },
  { name: 'Inglés', level: 'Intermedio', percentage: 70 }
]
</script>

<style scoped>
.home-page {
  padding-top: 0;
}

.hero {
  background: linear-gradient(135deg, var(--bg-light) 0%, var(--bg-color) 100%);
  padding: 80px 0;
}

.hero-content {
  display: grid;
  grid-template-columns: 300px 1fr;
  gap: 3rem;
  align-items: center;
}

.hero-image {
  text-align: center;
}

.profile-img {
  width: 250px;
  height: 250px;
  border-radius: 50%;
  object-fit: cover;
  border: 4px solid var(--primary-color);
  box-shadow: var(--shadow-lg);
}

.hero-title {
  font-size: 3rem;
  font-weight: 700;
  color: var(--text-color);
  margin-bottom: 0.5rem;
}

.hero-subtitle {
  font-size: 1.5rem;
  color: var(--primary-color);
  margin-bottom: 1rem;
  font-weight: 600;
}

.hero-description {
  font-size: 1.1rem;
  color: var(--text-light);
  line-height: 1.8;
  max-width: 600px;
}

.experience-list,
.education-list,
.languages-list {
  display: flex;
  flex-direction: column;
  gap: 1.5rem;
}

.experience-item,
.education-item,
.language-item {
  margin-bottom: 0;
}

.experience-header {
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
  margin-bottom: 0.5rem;
  flex-wrap: wrap;
  gap: 1rem;
}

.experience-title {
  font-size: 1.5rem;
  font-weight: 600;
  color: var(--text-color);
}

.experience-period {
  color: var(--primary-color);
  font-weight: 600;
  white-space: nowrap;
}

.experience-company {
  font-size: 1.1rem;
  color: var(--primary-color);
  margin-bottom: 0.5rem;
  font-weight: 500;
}

.experience-description {
  color: var(--text-light);
  margin-bottom: 1rem;
}

.experience-responsibilities {
  list-style: none;
  padding-left: 0;
}

.experience-responsibilities li {
  color: var(--text-light);
  padding-left: 1.5rem;
  position: relative;
  margin-bottom: 0.5rem;
}

.experience-responsibilities li::before {
  content: '▸';
  position: absolute;
  left: 0;
  color: var(--primary-color);
}

.education-title {
  font-size: 1.5rem;
  font-weight: 600;
  color: var(--text-color);
  margin-bottom: 0.5rem;
}

.education-institution {
  font-size: 1.1rem;
  color: var(--primary-color);
  margin-bottom: 0.5rem;
  font-weight: 500;
}

.education-period {
  color: var(--text-light);
  margin-bottom: 0.5rem;
}

.certifications-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
  gap: 1.5rem;
}

.certification-title {
  font-size: 1.25rem;
  font-weight: 600;
  color: var(--text-color);
  margin-bottom: 0.5rem;
}

.certification-issuer {
  color: var(--primary-color);
  font-weight: 500;
  margin-bottom: 0.5rem;
}

.certification-date {
  color: var(--text-light);
  margin-bottom: 1rem;
}

.certification-link {
  color: var(--primary-color);
  text-decoration: none;
  font-weight: 500;
  transition: color 0.3s ease;
}

.certification-link:hover {
  color: var(--primary-dark);
  text-decoration: underline;
}

.language-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 0.75rem;
}

.language-name {
  font-size: 1.25rem;
  font-weight: 600;
  color: var(--text-color);
}

.language-level {
  color: var(--primary-color);
  font-weight: 500;
}

.language-bar {
  width: 100%;
  height: 8px;
  background: var(--bg-light);
  border-radius: 4px;
  overflow: hidden;
}

.language-progress {
  height: 100%;
  background: linear-gradient(90deg, var(--primary-color), var(--primary-dark));
  border-radius: 4px;
  transition: width 0.3s ease;
}

@media (max-width: 768px) {
  .hero-content {
    grid-template-columns: 1fr;
    text-align: center;
  }

  .profile-img {
    width: 200px;
    height: 200px;
  }

  .hero-title {
    font-size: 2rem;
  }

  .hero-subtitle {
    font-size: 1.25rem;
  }

  .experience-header {
    flex-direction: column;
    align-items: flex-start;
  }

  .certifications-grid {
    grid-template-columns: 1fr;
  }
}
</style>


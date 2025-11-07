<template>
  <div class="home-page">
    <!-- Hero Section -->
    <section class="hero section">
      <div class="container">
        <div class="hero-content">
          <div class="hero-image">
            <img src="/img/profile.JPG" alt="Foto de perfil" class="profile-img" />
          </div>
          <div class="hero-text">
            <h1 class="hero-title">Hola, soy {{ name }}</h1>
            <p class="hero-subtitle">{{ title }}</p>
            <p class="hero-description">{{ description }}</p>
          </div>
        </div>
      </div>
    </section>

    <!-- Technologies Section -->
    <section class="technologies section">
      <div class="container">
        <h2 class="section-title">Tecnologías</h2>
        <div class="technologies-grid">
          <div v-for="(tech, index) in technologies" :key="index" class="technology-item card">
            <div class="technology-icon" v-html="getTechIcon(tech.name)"></div>
            <div class="technology-info">
              <div class="technology-header">
                <span class="technology-name">{{ tech.name }}</span>
              </div>
            </div>
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
// Iconos SVG oficiales de cada tecnología
const techIcons = {
  'C#': '<svg xmlns="http://www.w3.org/2000/svg" width="200" height="200" viewBox="0 0 128 128"><path fill="#9B4F96" d="M115.4 30.7L67.1 2.9c-.8-.5-1.9-.7-3.1-.7c-1.2 0-2.3.3-3.1.7l-48 27.9c-1.7 1-2.9 3.5-2.9 5.4v55.7c0 1.1.2 2.4 1 3.5l106.8-62c-.6-1.2-1.5-2.1-2.4-2.7z"/><path fill="#68217A" d="M10.7 95.3c.5.8 1.2 1.5 1.9 1.9l48.2 27.9c.8.5 1.9.7 3.1.7c1.2 0 2.3-.3 3.1-.7l48-27.9c1.7-1 2.9-3.5 2.9-5.4V36.1c0-.9-.1-1.9-.6-2.8l-106.6 62z"/><path fill="#fff" d="M85.3 76.1C81.1 83.5 73.1 88.5 64 88.5c-13.5 0-24.5-11-24.5-24.5s11-24.5 24.5-24.5c9.1 0 17.1 5 21.3 12.5l13-7.5c-6.8-11.9-19.6-20-34.3-20c-21.8 0-39.5 17.7-39.5 39.5s17.7 39.5 39.5 39.5c14.6 0 27.4-8 34.2-19.8l-12.9-7.6zM97 66.2l.9-4.3h-4.2v-4.7h5.1L100 51h4.9l-1.2 6.1h3.8l1.2-6.1h4.8l-1.2 6.1h2.4v4.7h-3.3l-.9 4.3h4.2v4.7h-5.1l-1.2 6h-4.9l1.2-6h-3.8l-1.2 6h-4.8l1.2-6h-2.4v-4.7H97zm4.8 0h3.8l.9-4.3h-3.8l-.9 4.3z"/></svg>',
  '.NET': '<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 128 128"><g fill="#623697"><path d="M61.195 0h4.953c12.918.535 25.688 4.89 36.043 12.676 9.809 7.289 17.473 17.437 21.727 28.906 2.441 6.387 3.664 13.18 4.082 19.992v4.211c-.414 11.293-3.664 22.52-9.73 32.082-6.801 10.895-16.922 19.73-28.727 24.828A64.399 64.399 0 0165.082 128h-2.144c-11.735-.191-23.41-3.66-33.297-9.992-11.196-7.113-20.114-17.785-25.028-30.117C1.891 81.19.441 74.02 0 66.812v-4.957c.504-14.39 5.953-28.609 15.41-39.496C23.168 13.31 33.5 6.48 44.887 2.937 50.172 1.27 55.676.41 61.195 0M25.191 37.523c-.03 12.153-.011 24.305-.011 36.454 1.43.011 2.86.011 4.293.011-.075-10.433.101-20.863-.106-31.293.48.907.918 1.84 1.465 2.707C37.035 54.91 43.105 64.5 49.309 74c1.738-.023 3.476-.023 5.214.004-.003-12.16-.007-24.32.004-36.48a308.076 308.076 0 00-4.25-.012c.075 10.32-.136 20.64.125 30.949-6.507-10.352-13.101-20.645-19.695-30.945a370.85 370.85 0 00-5.516.007m38.844-.011c-.129 12.16-.004 24.32-.047 36.476 6.469-.015 12.938.024 19.41-.02a83.36 83.36 0 01.024-3.952c-5.012-.016-10.027.007-15.043-.02-.074-4.21-.004-8.426-.04-12.637 4.395-.078 8.79.012 13.18-.047-.011-1.277-.011-2.554-.019-3.832-4.387.141-8.773-.054-13.164.012.012-4.023.02-8.05.02-12.078 4.699 0 9.398-.02 14.093.012-.008-1.301 0-2.606.016-3.906-6.145-.016-12.29-.008-18.43-.008m22.602.054c.004 1.266.004 2.528.008 3.79 3.488-.04 6.972.109 10.46.035-.023 10.863.004 21.718-.011 32.574 1.46.043 2.93.035 4.39-.09-.12-5.992.118-11.988-.156-17.977.067-2.699-.07-5.394.117-8.09.106-2.14-.277-4.277-.035-6.417 3.516.047 7.035.015 10.55.015a59.774 59.774 0 01.075-3.832c-8.469-.105-16.937-.094-25.398-.008M13.55 69.094c-1.977.91-2.106 4.023-.149 5.027 1.72 1.18 4.305-.371 4.227-2.41.133-2.004-2.29-3.688-4.078-2.617m29.23 15.289c-4.277 3.469-4.226 11.195.5 14.25 2.668 1.695 6.102 1.344 8.922.215.012-.621.027-1.239.05-1.86-2.671 1.395-6.41 1.68-8.675-.61-2.965-3.237-2.297-9.269 1.613-11.476 2.211-1.164 4.907-.824 7.086.239-.007-.66-.004-1.32 0-1.98-3.097-1.099-6.922-1.04-9.496 1.222m17.207 2.71c-1.89.22-3.758 1.22-4.633 2.966-1.253 2.496-1.109 5.867.864 7.96 2.035 2.297 5.945 2.32 8.18.297 2.425-2.308 2.699-6.468.757-9.164-1.148-1.629-3.273-2.183-5.168-2.058m17.887 2.722c-1.66 2.883-1.332 7.25 1.598 9.211 2.183 1.22 4.933.832 7.074-.308-.004-.617.004-1.235.031-1.848-1.687 1.07-3.937 1.856-5.812.777-1.309-.722-1.704-2.257-1.914-3.625 2.875-.039 5.746-.082 8.625-.074-.075-1.828-.118-3.894-1.45-5.308-2.199-2.43-6.644-1.657-8.152 1.175m-8.414-2.336v12.008c.652 0 1.312 0 1.973.004.023-2.195-.04-4.394.023-6.594.016-1.27.527-2.558 1.484-3.414.801-.605 1.883-.27 2.801-.246-.012-.636-.02-1.27-.023-1.902-1.793-.398-3.336.652-4.242 2.117-.02-.633-.04-1.266-.051-1.894-.656-.024-1.313-.051-1.965-.079zm0 0"/><path d="M58.758 89.223c1.652-.805 4.023-.41 4.945 1.3 1.05 1.887 1.027 4.383-.137 6.211-1.52 2.286-5.527 1.786-6.523-.742-1.008-2.258-.617-5.484 1.715-6.77zm0 0M79.04 92.414c.046-1.574 1.144-3.137 2.726-3.48.976-.164 2.097.007 2.773.793.672.714.813 1.714.98 2.64-2.16.012-4.32-.031-6.48.047zm0 0"/></g></svg>',
  'Vue.js': '<svg width="40" height="40" viewBox="0 0 24 24" fill="currentColor"><path d="M24 1.61H14.06L12 5.16 9.94 1.61H0L12 22.39 24 1.61zm-8.47 4.74l-1.53 2.61-1.53-2.61h3.06zm-6.2 0l3.07 5.22 3.07-5.22H9.33zM2.36 2.95h3.24L12 13.58l6.4-10.63h3.24L12 19.24 2.36 2.95z"/></svg>',
  'Python': '<svg width="200" height="200" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24"><path fill="#0288d1" d="M9.86 2A2.86 2.86 0 0 0 7 4.86v1.68h4.29c.39 0 .71.57.71.96H4.86A2.86 2.86 0 0 0 2 10.36v3.781a2.86 2.86 0 0 0 2.86 2.86h1.18v-2.68a2.85 2.85 0 0 1 2.85-2.86h5.25c1.58 0 2.86-1.271 2.86-2.851V4.86A2.86 2.86 0 0 0 14.14 2zm-.72 1.61c.4 0 .72.12.72.71s-.32.891-.72.891c-.39 0-.71-.3-.71-.89s.32-.711.71-.711"/><path fill="#fdd835" d="M17.959 7v2.68a2.85 2.85 0 0 1-2.85 2.859H9.86A2.85 2.85 0 0 0 7 15.389v3.75a2.86 2.86 0 0 0 2.86 2.86h4.28A2.86 2.86 0 0 0 17 19.14v-1.68h-4.291c-.39 0-.709-.57-.709-.96h7.14A2.86 2.86 0 0 0 22 13.64V9.86A2.86 2.86 0 0 0 19.14 7zM8.32 11.513l-.004.004l.038-.004zm6.54 7.276c.39 0 .71.3.71.89a.71.71 0 0 1-.71.71c-.4 0-.72-.12-.72-.71s.32-.89.72-.89"/></svg>',
  'React': '<svg width="40" height="40" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5"><ellipse cx="12" cy="12" rx="11" ry="4.2" fill="none" stroke="currentColor" stroke-width="1.5"/><ellipse cx="12" cy="12" rx="11" ry="4.2" fill="none" stroke="currentColor" stroke-width="1.5" transform="rotate(60 12 12)"/><ellipse cx="12" cy="12" rx="11" ry="4.2" fill="none" stroke="currentColor" stroke-width="1.5" transform="rotate(-60 12 12)"/><circle cx="12" cy="12" r="2" fill="currentColor"/></svg>',
  'Oracle': '<svg xmlns="http://www.w3.org/2000/svg" width="200" height="200" viewBox="0 0 512 67"><path fill="#EA1B22" d="M221.034 43.303h33.832l-17.889-28.781l-32.833 52.037h-14.942l39.935-62.508c1.736-2.525 4.63-4.051 7.84-4.051c3.104 0 5.998 1.473 7.682 3.946l40.093 62.613H269.81l-7.05-11.628h-34.253l-7.472-11.628ZM376.251 54.93V.631h-12.68v59.614c0 1.631.631 3.21 1.841 4.42s2.841 1.894 4.63 1.894h57.825l7.472-11.628H376.25Zm-209.78-9.734c12.313 0 22.31-9.944 22.31-22.256c0-12.313-9.997-22.31-22.31-22.31h-55.473v65.93h12.676v-54.3h41.956c5.893 0 10.628 4.789 10.628 10.682c0 5.892-4.735 10.68-10.628 10.68l-35.747-.052l37.851 32.99h18.416l-25.466-21.362h5.788ZM32.97 66.559C14.77 66.56 0 51.827 0 33.622C0 15.416 14.77.632 32.97.632h38.32c18.204 0 32.963 14.784 32.963 32.99c0 18.205-14.759 32.937-32.964 32.937H32.97Zm37.468-11.628c11.791 0 21.341-9.524 21.341-21.31c0-11.785-9.55-21.361-21.341-21.361h-36.62c-11.787 0-21.342 9.576-21.342 21.362c0 11.785 9.555 21.309 21.341 21.309h36.62Zm240.78 11.628c-18.204 0-32.99-14.732-32.99-32.937c0-18.206 14.786-32.99 32.99-32.99h45.514l-7.42 11.628H312.06c-11.786 0-21.362 9.576-21.362 21.362c0 11.785 9.576 21.309 21.362 21.309h45.723l-7.472 11.628h-39.093Zm155.06-11.628c-9.734 0-17.995-6.524-20.52-15.522h54.194l7.471-11.628h-61.665c2.525-8.945 10.786-15.521 20.52-15.521h37.2L511 .63h-45.565c-18.205 0-32.99 14.785-32.99 32.99c0 18.206 14.785 32.938 32.99 32.938h39.094L512 54.931h-45.723Z"/></svg>',
  'MySQL': '<svg xmlns="http://www.w3.org/2000/svg" width="200" height="200" viewBox="0 0 512 349"><path fill="#00758F" d="m152.31 230.297l15.56 50.487c3.496 11.463 4.954 19.465 4.37 24.026c8.51-22.792 14.456-47.63 17.839-74.513h18.71c-8.045 43.766-18.656 75.57-31.827 95.41c-10.262 15.289-21.504 22.933-33.746 22.933c-3.264 0-7.288-.986-12.063-2.944v-10.55c2.333.342 5.07.525 8.218.525c5.711 0 10.314-1.583 13.816-4.742c4.193-3.849 6.292-8.175 6.292-12.97c0-3.274-1.637-9.993-4.896-20.157l-21.68-67.505h19.406ZM33.223 199.266l28.5 86.956h.176l28.675-86.956h23.428c5.13 43.124 8.16 82.581 9.09 118.346H103.34c-.695-33.433-2.62-64.871-5.768-94.32H97.4l-30.078 94.32H52.28l-29.896-94.32h-.176c-2.218 28.282-3.614 59.72-4.196 94.32H0c1.164-42.08 4.077-81.525 8.739-118.346h24.485Z"/><path fill="#F29111" d="M352.498 197.51c30.657 0 45.986 19.586 45.986 58.739c0 21.276-4.61 37.347-13.821 48.204c-1.66 1.984-3.495 3.698-5.427 5.286l21.695 10.727l-.021-.001l-7.703 13.302l-28.253-16.485c-4.683 1.387-9.836 2.08-15.451 2.08c-15.053 0-26.297-4.387-33.731-13.15c-8.16-9.694-12.238-24.955-12.238-45.757c0-21.156 4.602-37.166 13.816-48.037c8.392-9.944 20.11-14.909 35.148-14.909Zm-93.88.172c10.957 0 20.92 2.932 29.894 8.775l-4.558 10.157c-7.679-3.264-15.25-4.903-22.716-4.903c-6.058 0-10.726 1.458-13.98 4.392c-3.272 2.908-5.296 6.65-5.296 11.212c0 7.01 4.994 13.089 14.215 18.225a816.32 816.32 0 0 1 9.031 5.011l.688.387l.345.194l.689.387l.344.194l.688.388c6.98 3.935 13.548 7.691 13.548 7.691c9.22 6.545 13.816 13.523 13.816 25.016c0 10.037-3.678 18.276-11.01 24.723c-7.337 6.418-17.194 9.636-29.538 9.636c-11.545 0-22.734-3.704-33.572-11.05l5.07-10.166c9.327 4.675 17.767 7.01 25.346 7.01c7.108 0 12.672-1.587 16.697-4.721c4.017-3.157 6.424-7.56 6.424-13.143c0-7.027-4.888-13.034-13.855-18.073a897.982 897.982 0 0 1-8.395-4.697l-.687-.389c-1.262-.713-2.533-1.435-3.778-2.142l-.675-.384c-6.055-3.444-11.29-6.453-11.29-6.453c-8.964-6.557-13.459-13.592-13.459-25.184c0-9.587 3.352-17.336 10.046-23.231c6.71-5.908 15.367-8.862 25.968-8.862Zm175.895 1.584v103.788h37.238v14.558h-56.124V199.266h18.886Zm57.93 103.833v2.46h-4.094v12.04h-3.13v-12.04h-4.253v-2.46h11.478Zm7.56 0l3.931 9.884l3.611-9.884h4.437v14.5h-2.95v-11.035l-4.11 11.035h-2.127l-4.117-11.035h-.158v11.035h-2.791v-14.5h4.275ZM350.57 212.064c-18.066 0-27.104 14.91-27.104 44.71c0 17.07 2.395 29.448 7.176 37.163c4.428 7.14 11.363 10.703 20.806 10.703c18.066 0 27.103-15.026 27.103-45.064c0-16.831-2.395-29.103-7.17-36.822c-4.433-7.124-11.365-10.69-20.81-10.69Z"/><path fill="#00758F" d="M303.218 7.333c5.993-14.726 26.948-3.574 35.08 1.57c1.993 1.287 4.279 4.006 6.564 5.011c3.565.14 7.127.419 10.698.568c6.698 1.574 12.972 2.86 18.25 5.866c24.528 14.445 40.495 29.165 55.19 53.479c3.14 5.15 4.709 10.723 7.274 16.296c3.56 8.307 7.56 17.027 11.692 24.882c1.85 3.724 3.281 7.865 5.85 11.01c1.003 1.438 3.852 1.862 5.555 2.721c4.708 2.437 10.412 4.287 14.84 7.147c8.269 5.156 16.264 11.3 23.532 17.59c2.709 2.428 4.555 5.865 7.136 8.433v1.296c-2.291.703-4.574 1.423-6.859 2c-4.991 1.282-9.412.992-14.254 2.275c-2.992.868-6.707 2.013-9.845 2.304l.29.292c1.846 5.275 11.834 9.565 16.402 12.72c5.548 4.004 10.689 8.86 14.827 14.437c1.429 1.423 2.858 2.718 4.28 4.137c.994 1.438 1.274 3.298 2.28 4.58v.434c-1.114-.393-1.915-1.143-2.674-1.927l-.453-.473c-.453-.47-.91-.932-1.431-1.313c-3.148-2.15-6.274-4.722-9.422-6.721c-5.412-3.434-11.689-5.427-17.246-8.874c-3.142-2.001-6.137-4.28-9.132-6.57c-2.715-2.007-5.705-5.861-7.411-8.721c-1.005-1.58-1.143-3.437-2.291-4.58c.205-1.909 1.954-2.476 3.719-2.942l.406-.107c.609-.158 1.205-.316 1.725-.525c7.414-3.148 16.253-4.29 27.667-4.004c-.43-2.866-7.562-6.437-9.839-8.153c-4.57-3.294-9.409-6.731-14.257-9.729c-2.569-1.57-6.996-2.716-9.842-3.999c-3.851-1.574-12.41-3.147-14.544-6.145c-3.625-4.726-6.229-10.363-8.757-16.057l-.688-1.554a803.85 803.85 0 0 0-.69-1.553c-2.988-6.857-6.7-14.006-9.695-21.027c-1.566-3.425-2.285-6.431-4-9.716c-10.407-20.158-25.81-37.035-44.485-48.904c-6.137-3.862-12.98-7.436-20.534-9.865c-4.281-1.293-9.419-.578-13.98-1.57h-3.002c-2.562-.722-4.701-3.438-6.7-4.87c-4.415-2.998-8.837-5.011-14.117-7.15c-1.85-.858-7.133-2.856-8.977-1.283c-1.142.287-1.721.718-2.002 1.864c-1.136 1.71-.137 4.286.57 5.863c2.142 4.57 5.134 7.286 7.85 11.148c2.416 3.425 5.417 7.287 7.13 11.011c3.696 8.005 5.417 16.874 8.842 24.878c1.27 3.01 3.279 6.435 5.128 9.15c1.567 2.155 4.416 3.713 5.278 6.441c1.718 2.86-2.572 12.297-3.565 15.294c-3.715 11.727-2.995 28.028 1.283 38.193l.228.536l.228.543c1.562 3.723 3.234 7.732 7.387 8.773c.286-.284 0-.135.567-.284c1.005-7.868 1.288-15.445 4-21.601c1.567-3.849 4.696-6.57 6.841-9.712c1.43.856 1.43 3.437 2.282 5.145c1.856 4.43 3.849 9.287 6.137 13.73c4.696 9.15 9.98 18.021 15.967 26.025c2.005 2.859 4.85 6.006 7.416 8.581c1.143.997 2.423 1.573 3.282 2.856h.28v.432c-4.278-1.577-6.99-6.003-10.402-8.587c-6.424-4.857-14.117-12.151-18.545-19.15c-1.852-4.018-3.854-7.869-5.85-11.867v-.289c-.853 1.142-.567 2.276-.994 4.004c-1.852 7.145-.426 15.296-6.843 17.866c-7.274 3.01-12.7-4.857-14.977-8.432c-7.276-11.866-9.269-31.884-4.138-48.043c1.14-3.577 1.295-7.867 3.285-10.723c-.43-2.582-2.42-3.288-3.571-4.87c-1.996-2.704-3.705-5.854-5.268-8.857c-3.002-5.866-5.138-12.875-7.417-19.166c-1.002-2.569-1.289-5.148-2.288-7.58c-1.704-3.712-4.845-7.436-7.268-10.72c-3.281-4.72-12.837-13.868-8.985-23.168Zm46.772 28.015c.381.382.841.716 1.317 1.045l.574.394c.765.53 1.506 1.088 1.96 1.848c.72 1.006.854 1.999 1.716 3.007c0 3.437-.996 5.722-3.007 7.146c0 0-.137.15-.278.29c-1.14-2.291-2.139-4.57-3.287-6.859c-1.414-1.998-3.413-3.583-4.565-5.866h-.277v-.287c1.721-.425 3.428-.718 5.847-.718Z"/></svg>',
  'Java': `<svg xmlns="http://www.w3.org/2000/svg" x="0px" y="0px" width="100" height="100" viewBox="0 0 48 48">
    <path fill="#F44336" d="M23.65,24.898c-0.998-1.609-1.722-2.943-2.725-5.455C19.229,15.2,31.24,11.366,26.37,3.999c2.111,5.089-7.577,8.235-8.477,12.473C17.07,20.37,23.645,24.898,23.65,24.898z"></path>
    <path fill="#F44336" d="M23.878,17.27c-0.192,2.516,2.229,3.857,2.299,5.695c0.056,1.496-1.447,2.743-1.447,2.743s2.728-0.536,3.579-2.818c0.945-2.534-1.834-4.269-1.548-6.298c0.267-1.938,6.031-5.543,6.031-5.543S24.311,11.611,23.878,17.27z"></path>
    <g>
      <path fill="#1565C0" d="M32.084 25.055c1.754-.394 3.233.723 3.233 2.01 0 2.901-4.021 5.643-4.021 5.643s6.225-.742 6.225-5.505C37.521 24.053 34.464 23.266 32.084 25.055zM29.129 27.395c0 0 1.941-1.383 2.458-1.902-4.763 1.011-15.638 1.147-15.638.269 0-.809 3.507-1.638 3.507-1.638s-7.773-.112-7.773 2.181C11.683 28.695 21.858 28.866 29.129 27.395z"></path>
      <path fill="#1565C0" d="M27.935,29.571c-4.509,1.499-12.814,1.02-10.354-0.993c-1.198,0-2.974,0.963-2.974,1.889c0,1.857,8.982,3.291,15.63,0.572L27.935,29.571z"></path>
      <path fill="#1565C0" d="M18.686,32.739c-1.636,0-2.695,1.054-2.695,1.822c0,2.391,9.76,2.632,13.627,0.205l-2.458-1.632C24.271,34.404,17.014,34.579,18.686,32.739z"></path>
      <path fill="#1565C0" d="M36.281,36.632c0-0.936-1.055-1.377-1.433-1.588c2.228,5.373-22.317,4.956-22.317,1.784c0-0.721,1.807-1.427,3.477-1.093l-1.42-0.839C11.26,34.374,9,35.837,9,37.017C9,42.52,36.281,42.255,36.281,36.632z"></path>
      <path fill="#1565C0" d="M39,38.604c-4.146,4.095-14.659,5.587-25.231,3.057C24.341,46.164,38.95,43.628,39,38.604z"></path>
    </g>
  </svg>`,
  'Laravel': '<svg width="40" height="40" viewBox="0 0 32 32" fill="none" xmlns="http://www.w3.org/2000/svg"><path fill="#ff5252" d="M31.963 9.12c-.008-.03-.023-.056-.034-.085a1 1 0 0 0-.07-.156a2 2 0 0 0-.162-.205a1 1 0 0 0-.088-.072a1 1 0 0 0-.083-.068l-.044-.02l-.035-.024l-6-3a1 1 0 0 0-.894 0l-6 3l-.035.024l-.044.02a1 1 0 0 0-.083.068a.7.7 0 0 0-.187.191a1 1 0 0 0-.064.086a1 1 0 0 0-.069.156c-.01.029-.026.055-.034.085a1 1 0 0 0-.037.265v5.382l-4 2V5.385a1 1 0 0 0-.037-.265c-.008-.03-.023-.056-.034-.085a1 1 0 0 0-.07-.156a1 1 0 0 0-.063-.086a.7.7 0 0 0-.187-.191a1 1 0 0 0-.083-.068l-.044-.02l-.035-.024l-6-3a1 1 0 0 0-.894 0l-6 3l-.035.024l-.044.02a1 1 0 0 0-.083.068a1 1 0 0 0-.088.072a1 1 0 0 0-.1.119a1 1 0 0 0-.063.086a1 1 0 0 0-.069.156c-.01.029-.026.055-.034.085A1 1 0 0 0 0 5.385v19a1 1 0 0 0 .553.894l6 3l6 3c.014.007.03.005.046.011a.9.9 0 0 0 .802 0c.015-.006.032-.004.046-.01l12-6a1 1 0 0 0 .553-.895v-5.382l5.447-2.724a1 1 0 0 0 .553-.894v-6a1 1 0 0 0-.037-.265M9.236 21.385l4.211-2.106h.001L19 16.503l3.764 1.882L13 23.267ZM24 13.003v3.764l-4-2v-3.764Zm1-5.5l3.764 1.882L25 11.267l-3.764-1.882ZM8 19.767V9.003l4-2v10.764ZM7 3.503l3.764 1.882L7 7.267L3.236 5.385Zm-5 3.5l4 2v16.764l-4-2Zm6 16l4 2v3.764l-4-2Zm16 .764l-10 5v-3.764l10-5Zm6-9l-4 2v-3.764l4-2Z"/></svg>',
  'Docker': '<svg xmlns="http://www.w3.org/2000/svg" width="200" height="200" viewBox="0 0 256 256"><g fill="none"><rect width="256" height="256" fill="#2396ED" rx="60"/><path fill="#fff" d="M141.187 122.123h20.717v-18.744h-20.717v18.744Zm-24.662 0h20.716v-18.744h-20.716v18.744Zm-24.17 0h20.717v-18.744H92.355v18.744Zm-24.17 0H88.41v-18.744H68.186v18.744Zm-24.662 0H64.24v-18.744H43.523v18.744Zm24.663-22.69h20.223V80.69H68.186v18.743Zm24.17 0h20.716V80.69H92.355v18.743Zm24.169 0h20.716V80.69h-20.716v18.743Zm0-22.69h20.716V58h-20.716v18.744ZM228 113.739s-8.879-8.386-27.129-5.426c-1.973-14.305-17.264-22.69-17.264-22.69s-14.304 17.264-3.946 36.501c-2.959 1.48-7.892 3.453-15.291 3.453H28.726c-2.467 9.372-2.467 71.521 65.602 71.521c48.832 0 85.333-22.689 102.597-64.123C222.574 134.948 228 113.738 228 113.738Z"/></g></svg>',
  'PHP': `<svg width="40" height="40" viewBox="0 0 24 24" fill="currentColor" xmlns="http://www.w3.org/2000/svg"><path fill="#1e88e5" d="M12 18.08c-6.63 0-12-2.72-12-6.08s5.37-6.08 12-6.08S24 8.64 24 12s-5.37 6.08-12 6.08m-5.19-7.95c.54 0 .91.1 1.09.31c.18.2.22.56.13 1.03c-.1.53-.29.87-.58 1.09q-.42.33-1.29.33h-.87l.53-2.76zm-3.5 5.55h1.44l.34-1.75h1.23c.54 0 .98-.06 1.33-.17c.35-.12.67-.31.96-.58c.24-.22.43-.46.58-.73c.15-.26.26-.56.31-.88c.16-.78.05-1.39-.33-1.82c-.39-.44-.99-.65-1.82-.65H4.59zm7.25-8.33l-1.28 6.58h1.42l.74-3.77h1.14c.36 0 .6.06.71.18s.13.34.07.66l-.57 2.93h1.45l.59-3.07c.13-.62.03-1.07-.27-1.36c-.3-.27-.85-.4-1.65-.4h-1.27L12 7.35zM18 10.13c.55 0 .91.1 1.09.31c.18.2.22.56.13 1.03c-.1.53-.29.87-.57 1.09c-.29.22-.72.33-1.3.33h-.85l.5-2.76zm-3.5 5.55h1.44l.34-1.75h1.22c.55 0 1-.06 1.35-.17c.35-.12.65-.31.95-.58c.24-.22.44-.46.58-.73c.15-.26.26-.56.32-.88c.15-.78.04-1.39-.34-1.82c-.36-.44-.99-.65-1.82-.65h-2.75z"/></svg>`,
  'Javascript': '<svg xmlns="http://www.w3.org/2000/svg" width="200" height="200" viewBox="0 0 256 256"><g fill="none"><rect width="256" height="256" fill="#F0DB4F" rx="60"/><path fill="#323330" d="m67.312 213.932l19.59-11.856c3.78 6.701 7.218 12.371 15.465 12.371c7.905 0 12.889-3.092 12.889-15.12v-81.798h24.058v82.138c0 24.917-14.606 36.259-35.916 36.259c-19.245 0-30.416-9.967-36.087-21.996m85.07-2.576l19.588-11.341c5.157 8.421 11.859 14.607 23.715 14.607c9.969 0 16.325-4.984 16.325-11.858c0-8.248-6.53-11.17-17.528-15.98l-6.013-2.579c-17.357-7.388-28.871-16.668-28.871-36.258c0-18.044 13.748-31.792 35.229-31.792c15.294 0 26.292 5.328 34.196 19.247l-18.731 12.029c-4.125-7.389-8.591-10.31-15.465-10.31c-7.046 0-11.514 4.468-11.514 10.31c0 7.217 4.468 10.139 14.778 14.608l6.014 2.577c20.449 8.765 31.963 17.699 31.963 37.804c0 21.654-17.012 33.51-39.867 33.51c-22.339 0-36.774-10.654-43.819-24.574"/></g></svg>'
}

const getTechIcon = (techName) => {
  return techIcons[techName] || ''
}

// Datos personales
const name = 'Alejandro'
const title = 'Muñoz Domínguez'
const description = 'Soy desarrollador de software con más de dos años de experiencia, trabajando tanto en aplicaciones de escritorio como en aplicaciones web. Principalmente he utilizado C#, .NET y WPF, y también he trabajado con React y Vue en la parte web. Además, tengo conocimientos en Java, PHP y Laravel, así como experiencia con bases de datos Oracle y MySQL. Me gusta aplicar buenas prácticas, tengo nociones en el desarrollo de APIs, gestión de bases de datos y aspectos de seguridad. Me considero una persona que aprende rápido, que disfruta trabajar en equipo y que busca mejorar continuamente y aportar valor a los proyectos en los que participo.'

// Tecnologías
const technologies = [
  { name: 'C#'},
  { name: '.NET'},
  { name: 'Vue.js'},
  { name: 'Python'},
  { name: 'React'},
  { name: 'Oracle'},
  { name: 'MySQL'},
  { name: 'Java'},
  { name: 'Laravel'},
  { name: 'Docker'},
  { name: 'PHP'},
  { name: 'Javascript'}
]
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
  { name: 'Inglés', level: 'Intermedio'}
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

.technologies-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
  gap: 1.5rem;
}

.technology-item {
  display: flex;
  align-items: center;
  gap: 1rem;
  padding: 1.25rem;
  margin-bottom: 0;
  transition: transform 0.2s ease, box-shadow 0.2s ease;
}

.technology-item:hover {
  transform: translateY(-2px);
  box-shadow: var(--shadow-lg);
}

.technology-icon {
  flex-shrink: 0;
  width: 40px;
  height: 40px;
  display: flex;
  align-items: center;
  justify-content: center;
  color: var(--primary-color);
}

.technology-info {
  flex: 1;
  min-width: 0;
}

.technology-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 0.5rem;
}

.technology-name {
  font-size: 1rem;
  font-weight: 600;
  color: var(--text-color);
}

.technology-percentage {
  font-size: 0.9rem;
  font-weight: 600;
  color: var(--primary-color);
}

.technology-bar {
  width: 100%;
  height: 6px;
  background: var(--bg-color);
  border-radius: 3px;
  overflow: hidden;
}

.technology-progress {
  height: 100%;
  background: linear-gradient(90deg, var(--primary-color), var(--primary-dark));
  border-radius: 3px;
  transition: width 0.3s ease;
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

  .technologies-grid {
    grid-template-columns: 1fr;
  }
}
</style>


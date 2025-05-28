<template>
  <div class="min-h-screen bg-white dark-mode">
    <!-- Navbar -->
    <nav :class="'navbar ' + (scrolled ? 'navbar-scrolled' : '')">
      <div class="container">
        <div class="nav-content">
          <div class="logo">
            <a href="#home">Manogya Guragai</a>
          </div>

          <div class="nav-desktop">
            <div class="nav-links">
              <a v-for="link in navLinks" :key="link.name" :href="link.href" class="nav-link">
                {{ link.name }}
              </a>
              <button @click="toggleDarkMode" class="theme-toggle" aria-label="Toggle dark mode">
                <span v-if="darkMode">☀️</span>
                <span v-else>🌙</span>
              </button>
            </div>
          </div>

          <div class="nav-mobile">
            <button @click="toggleDarkMode" class="theme-toggle mobile-theme" aria-label="Toggle dark mode">
              <span v-if="darkMode">☀️</span>
              <span v-else>🌙</span>
            </button>
            <button @click="toggleMenu" class="menu-toggle" aria-expanded="false">
              <span class="sr-only">Open main menu</span>
              <span v-if="isOpen">✕</span>
              <span v-else>☰</span>
            </button>
          </div>
        </div>
      </div>

      <!-- Mobile menu -->
      <div v-show="isOpen" class="mobile-menu">
        <div class="mobile-menu-content">
          <a v-for="link in navLinks" :key="link.name" :href="link.href" class="mobile-link" @click="toggleMenu">
            {{ link.name }}
          </a>
        </div>
      </div>
    </nav>

    <!-- Hero Section -->
    <section id="home" class="hero">
      <div class="hero-bg"></div>
      <div class="container">
        <div class="hero-content">
          <div class="hero-text">
            <h1 class="hero-title">Manogya Guragai</h1>
            <div class="hero-subtitle">
              <h2>I'm a <span ref="typedElement" class="typed-text"></span><span class="cursor">|</span></h2>
            </div>

            <p class="hero-description">
              I transform complex data into actionable insights and build intelligent solutions
              that solve real-world problems.
            </p>

            <div class="hero-buttons">
              <button @click="scrollToSection('projects')" class="btn btn-primary">
                View My Projects
              </button>
              <button @click="scrollToSection('contact')" class="btn btn-secondary">
                Get In Touch
              </button>
            </div>
          </div>

          <div class="hero-image">
            <div class="image-container">
              <img src="./assets/edited.png" alt="Manogya Guragai" />
            </div>
          </div>
        </div>
      </div>

      <div class="scroll-indicator">
        <button @click="scrollToSection('about')" aria-label="Scroll down" class="scroll-btn">
          <span class="chevron-down">↓</span>
        </button>
      </div>
    </section>

    <!-- About Section -->
    <section id="about" class="section">
      <div class="container">
        <div class="section-header">
          <h2 class="section-title">About Me</h2>
          <div class="section-divider"></div>
        </div>

        <div class="about-content">
          <div class="about-image">
            <div class="image-frame">
              <div class="image-wrapper">
                <img
                  src="https://images.pexels.com/photos/5691621/pexels-photo-5691621.jpeg?auto=compress&cs=tinysrgb&w=800"
                  alt="Professional headshot" />
              </div>
            </div>
          </div>

          <div class="about-text">
            <h3 class="about-subtitle">Data Scientist & AI Specialist</h3>
            <p class="about-paragraph">
              I'm a passionate data scientist with expertise in machine learning, data analysis, and AI applications.
              My journey in data science began during my academic years, where I discovered my passion for extracting
              meaningful insights from complex datasets.
            </p>
            <p class="about-paragraph">
              With a background in computer science and data analytics, I specialize in developing intelligent systems
              that leverage cutting-edge AI technologies to solve real-world problems. I enjoy working on projects that
              involve natural language processing, predictive modeling, and data visualization.
            </p>
            <p class="about-paragraph">
              When I'm not coding or analyzing data, you can find me exploring new technologies,
              contributing to open-source projects, or sharing my knowledge through technical articles and tutorials.
            </p>

            <div class="about-details">
              <div class="detail-column">
                <h4>Education</h4>
                <ul>
                  <li>• Computer Science, King's College</li>
                  <li>• Data Science Specialization</li>
                </ul>
              </div>
              <div class="detail-column">
                <h4>Interests</h4>
                <ul>
                  <li>• Machine Learning</li>
                  <li>• Natural Language Processing</li>
                  <li>• Data Visualization</li>
                  <li>• AI Ethics</li>
                </ul>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Experience Section -->
    <section id="experience" class="section section-alt">
      <div class="container">
        <div class="section-header">
          <h2 class="section-title">Experience & Education</h2>
          <div class="section-divider"></div>
        </div>

        <div class="timeline">
          <div class="timeline-line"></div>

          <div class="timeline-items">
            <div v-for="(exp, index) in experiences" :key="index"
              :class="'timeline-item ' + (index % 2 === 0 ? 'timeline-left' : 'timeline-right')">
              <div class="timeline-dot"></div>

              <div class="timeline-content">
                <div class="timeline-card">
                  <div class="card-header">
                    <span class="card-icon">{{ exp.type === 'work' ? '🏢' : '🎓' }}</span>
                    <h3>{{ exp.title }}</h3>
                  </div>

                  <div class="card-meta">
                    <p class="company">{{ exp.company }}</p>
                    <div class="meta-info">
                      <span>{{ exp.location }}</span>
                      <span class="separator">•</span>
                      <span>📅 {{ exp.period }}</span>
                    </div>
                  </div>

                  <ul class="card-description">
                    <li v-for="(item, idx) in exp.description" :key="idx">
                      <span class="bullet">•</span>
                      <span>{{ item }}</span>
                    </li>
                  </ul>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Projects Section -->
    <section id="projects" class="section">
      <div class="container">
        <div class="section-header">
          <h2 class="section-title">Featured Projects</h2>
          <div class="section-divider"></div>
          <p class="section-description">
            A collection of my recent work in data science, machine learning, and AI applications.
          </p>
        </div>

        <div class="projects-grid">
          <div v-for="project in projectsData" :key="project.id" class="project-card">
            <div class="project-image">
              <img :src="project.image" :alt="project.title" />
            </div>

            <div class="project-content">
              <h3 class="project-title">{{ project.title }}</h3>
              <p class="project-description">{{ project.description }}</p>

              <div class="project-tags">
                <span v-for="tag in project.tags" :key="tag" class="tag">
                  {{ tag }}
                </span>
              </div>

              <div class="project-actions">
                <button @click="openModal(project)" class="project-details">
                  💻 View Details
                </button>

                <div class="project-links">
                  <a :href="project.github" target="_blank" rel="noopener noreferrer" aria-label="GitHub repository">
                    🔗
                  </a>
                  <a v-if="project.demo" :href="project.demo" target="_blank" rel="noopener noreferrer"
                    aria-label="Live demo">
                    🚀
                  </a>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>

      <!-- Project Modal -->
      <div v-if="selectedProject" class="modal-overlay" @click="closeModal">
        <div class="modal-content" @click.stop>
          <div class="modal-image">
            <img :src="selectedProject.image" :alt="selectedProject.title" />
          </div>

          <div class="modal-body">
            <div class="modal-header">
              <h3>{{ selectedProject.title }}</h3>
              <button @click="closeModal" class="modal-close">✕</button>
            </div>

            <div class="modal-tags">
              <span v-for="tag in selectedProject.tags" :key="tag" class="tag">
                {{ tag }}
              </span>
            </div>

            <div class="modal-description">
              <p>{{ selectedProject.details }}</p>
            </div>

            <div class="modal-actions">
              <a :href="selectedProject.github" target="_blank" rel="noopener noreferrer" class="btn btn-dark">
                🔗 View on GitHub
              </a>
              <a v-if="selectedProject.demo" :href="selectedProject.demo" target="_blank" rel="noopener noreferrer"
                class="btn btn-primary">
                🚀 Live Demo
              </a>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Skills Section -->
    <section id="skills" class="section section-alt">
      <div class="container">
        <div class="section-header">
          <h2 class="section-title">Skills & Expertise</h2>
          <div class="section-divider"></div>
          <p class="section-description">
            My technical skills and areas of expertise in data science, machine learning, and software development.
          </p>
        </div>

        <div class="skills-grid">
          <div v-for="(category, index) in skillCategories" :key="index" class="skill-category">
            <div class="category-header">
              <div class="category-icon">{{ category.icon }}</div>
              <h3>{{ category.name }}</h3>
            </div>

            <div class="skills-list">
              <div v-for="(skill, idx) in category.skills" :key="idx" class="skill-item">
                <div class="skill-info">
                  <span class="skill-name">{{ skill.name }}</span>
                  <span class="skill-level">{{ skill.level }}%</span>
                </div>
                <div class="skill-bar">
                  <div :class="'skill-progress skill-' + skill.category" :style="{ width: skill.level + '%' }"></div>
                </div>
              </div>
            </div>
          </div>
        </div>

        <div class="additional-skills">
          <h3 class="additional-title">Additional Skills & Certifications</h3>

          <div class="additional-content">
            <div class="soft-skills">
              <h4>Soft Skills</h4>
              <ul>
                <li><span class="bullet">•</span> Problem-solving and analytical thinking</li>
                <li><span class="bullet">•</span> Data-driven decision making</li>
                <li><span class="bullet">•</span> Technical communication and presentation</li>
                <li><span class="bullet">•</span> Project management and team leadership</li>
                <li><span class="bullet">•</span> Continuous learning and adaptability</li>
              </ul>
            </div>

            <div class="certifications">
              <h4>Certifications</h4>
              <ul>
                <li><span class="bullet">•</span> Machine Learning Specialization - Stanford Online</li>
                <li><span class="bullet">•</span> Deep Learning Specialization - DeepLearning.AI</li>
                <li><span class="bullet">•</span> Data Science Professional Certificate - IBM</li>
                <li><span class="bullet">•</span> AWS Certified Machine Learning - Specialty</li>
                <li><span class="bullet">•</span> TensorFlow Developer Certificate - Google</li>
              </ul>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Contact Section -->
    <section id="contact" class="section">
      <div class="container">
        <div class="section-header">
          <h2 class="section-title">Get In Touch</h2>
          <div class="section-divider"></div>
          <p class="section-description">
            Have a project in mind or want to discuss collaboration opportunities? Feel free to reach out!
          </p>
        </div>

        <div class="contact-content">
          <div class="contact-info">
            <div class="contact-card">
              <h3>Contact Information</h3>

              <div class="contact-items">
                <div class="contact-item">
                  <div class="contact-icon">📧</div>
                  <div class="contact-details">
                    <h4>Email</h4>
                    <a href="mailto:manogyaguragai2@gmail.com">manogyaguragai2@gmail.com</a>
                  </div>
                </div>

                <div class="contact-item">
                  <div class="contact-icon">📱</div>
                  <div class="contact-details">
                    <h4>Phone</h4>
                    <p>+977 98XXXXXXXX</p>
                  </div>
                </div>

                <div class="contact-item">
                  <div class="contact-icon">📍</div>
                  <div class="contact-details">
                    <h4>Location</h4>
                    <p>Sinamangal, Kathmandu</p>
                  </div>
                </div>
              </div>

              <div class="social-links">
                <h4>Connect with me</h4>
                <div class="social-icons">
                  <a href="https://linkedin.com/in/manogyaguragai" target="_blank" rel="noopener noreferrer"
                    aria-label="LinkedIn">
                    💼
                  </a>
                  <a href="https://github.com/manogyaguragai" target="_blank" rel="noopener noreferrer"
                    aria-label="GitHub">
                    🔗
                  </a>
                  <a href="https://twitter.com/manogyaguragai" target="_blank" rel="noopener noreferrer"
                    aria-label="Twitter">
                    🐦
                  </a>
                </div>
              </div>
            </div>
          </div>

          <div class="contact-form-container">
            <form @submit.prevent="handleSubmit" class="contact-form">
              <h3>Send a Message</h3>

              <div v-if="submitSuccess" class="alert alert-success">
                Your message has been sent successfully! I'll get back to you soon.
              </div>

              <div v-if="submitError" class="alert alert-error">
                {{ submitError }}
              </div>

              <div class="form-fields">
                <div class="form-group">
                  <label for="name">Name</label>
                  <input type="text" id="name" v-model="formData.name" required placeholder="Your name" />
                </div>

                <div class="form-group">
                  <label for="email">Email</label>
                  <input type="email" id="email" v-model="formData.email" required placeholder="Your email" />
                </div>

                <div class="form-group">
                  <label for="subject">Subject</label>
                  <input type="text" id="subject" v-model="formData.subject" required
                    placeholder="Subject of your message" />
                </div>

                <div class="form-group">
                  <label for="message">Message</label>
                  <textarea id="message" v-model="formData.message" required rows="5"
                    placeholder="Your message..."></textarea>
                </div>

                <button type="submit" :disabled="isSubmitting"
                  :class="'btn btn-primary btn-full ' + (isSubmitting ? 'btn-disabled' : '')">
                  {{ isSubmitting ? 'Sending...' : 'Send Message' }}
                </button>
              </div>
            </form>
          </div>
        </div>
      </div>
    </section>

    <!-- Footer -->
    <footer class="footer">
      <div class="container">
        <div class="footer-content">
          <p>© {{ currentYear }} Manogya Guragai. All rights reserved.</p>
        </div>
      </div>
    </footer>
  </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted, computed } from 'vue'

// Reactive state
const isOpen = ref(false)
const darkMode = ref(false)
const scrolled = ref(false)
const selectedProject = ref(null)
const typedElement = ref(null)
const isSubmitting = ref(false)
const submitSuccess = ref(false)
const submitError = ref('')

const formData = ref({
  name: '',
  email: '',
  subject: '',
  message: ''
})

// Navigation links
const navLinks = [
  { name: 'Home', href: '#home' },
  { name: 'About', href: '#about' },
  { name: 'Experience', href: '#experience' },
  { name: 'Projects', href: '#projects' },
  { name: 'Skills', href: '#skills' },
  { name: 'Contact', href: '#contact' },
]

// Experience data
const experiences = [
  {
    title: "Data Scientist",
    company: "Data Analytics Corp",
    location: "Kathmandu, Nepal",
    period: "2022 - Present",
    description: [
      "Developed and implemented advanced machine learning models for predictive analytics",
      "Led a team of data analysts on multiple client projects",
      "Improved data processing efficiency by 35% through innovative ETL pipelines",
      "Created interactive dashboards for real-time data visualization"
    ],
    type: 'work'
  },
  {
    title: "Machine Learning Engineer",
    company: "AI Innovations",
    location: "Remote",
    period: "2020 - 2022",
    description: [
      "Designed and deployed NLP models for text classification and sentiment analysis",
      "Collaborated with cross-functional teams to integrate AI solutions",
      "Optimized deep learning models for production environments",
      "Implemented computer vision algorithms for image recognition systems"
    ],
    type: 'work'
  },
  {
    title: "Data Analytics Intern",
    company: "Tech Solutions Nepal",
    location: "Kathmandu, Nepal",
    period: "2019 - 2020",
    description: [
      "Assisted in data cleaning and preparation for analysis",
      "Conducted exploratory data analysis to identify patterns and trends",
      "Developed automated reports using Python and SQL",
      "Participated in client meetings and presentations"
    ],
    type: 'work'
  },
  {
    title: "Bachelor of Computer Science",
    company: "King's College",
    location: "Kathmandu, Nepal",
    period: "2016 - 2020",
    description: [
      "Specialized in Data Science and Artificial Intelligence",
      "Completed thesis on 'Machine Learning Applications in Healthcare'",
      "Participated in multiple hackathons and coding competitions",
      "Graduated with honors"
    ],
    type: 'education'
  }
]

// Projects data
const projectsData = [
  {
    id: 1,
    title: "Skill Gap Finder",
    description: "AI-driven tool that analyzes job descriptions and resumes to identify skill gaps and recommend training resources.",
    image: "https://images.pexels.com/photos/7242762/pexels-photo-7242762.jpeg?auto=compress&cs=tinysrgb&w=800",
    tags: ["Python", "NLP", "Machine Learning", "Flask"],
    github: "https://github.com/manogyaguragai/SkillGapFinder",
    demo: "https://skillgapfinder.demo.com",
    details: "This project uses natural language processing to analyze job descriptions and compare them with user resumes. It identifies missing skills and provides personalized recommendations for courses and resources to help bridge the gap. The application was built with Python, NLTK, and scikit-learn for the backend, with a Flask API and React frontend."
  },
  {
    id: 2,
    title: "Vehicle Safety System",
    description: "An IoT and ML-based system for monitoring driver behavior and detecting potential safety hazards in real-time.",
    image: "https://images.pexels.com/photos/3593922/pexels-photo-3593922.jpeg?auto=compress&cs=tinysrgb&w=800",
    tags: ["IoT", "Python", "TensorFlow", "Computer Vision"],
    github: "https://github.com/manogyaguragai/vehicle_safety_system",
    details: "The Vehicle Safety System combines IoT sensors and machine learning to monitor driver behavior and detect potential safety issues in real-time. It uses computer vision to detect driver drowsiness and distraction, while additional sensors monitor vehicle parameters. The system provides audio alerts and logs incidents for later review. Built with Python, TensorFlow, and OpenCV, with a React Native mobile app for notifications and monitoring."
  },
  {
    id: 3,
    title: "Talk to PDF",
    description: "An AI-powered document assistant that allows users to have conversations with PDF documents using natural language.",
    image: "https://images.pexels.com/photos/9793535/pexels-photo-9793535.jpeg?auto=compress&cs=tinysrgb&w=800",
    tags: ["Python", "NLP", "LangChain", "React"],
    github: "https://github.com/manogyaguragai/Talk-to-PDF",
    demo: "https://talktopdf.demo.com",
    details: "Talk to PDF is an intelligent document assistant that enables users to have natural language conversations with their PDF documents. The system extracts text from PDFs, processes it using advanced NLP techniques, and allows users to ask questions about the content. It uses vector embeddings for semantic search and retrieval, with a conversational interface powered by LangChain. The frontend is built with React and Tailwind CSS."
  },
  {
    id: 4,
    title: "Random Password Package",
    description: "A secure and customizable random password generator package for Node.js applications.",
    image: "https://images.pexels.com/photos/5380642/pexels-photo-5380642.jpeg?auto=compress&cs=tinysrgb&w=800",
    tags: ["JavaScript", "Node.js", "Cryptography", "NPM Package"],
    github: "https://github.com/manogyaguragai/RandomPasswordPackage",
    demo: "https://www.npmjs.com/package/random-password-gen",
    details: "This NPM package provides a robust solution for generating secure, random passwords in Node.js applications. It offers various customization options including password length, character sets, and special requirements. The package uses cryptographically secure random number generation to ensure password strength and unpredictability. It includes comprehensive documentation and example implementations."
  }
]

// Skills data
const skillCategories = [
  {
    name: "Programming Languages",
    icon: "💻",
    skills: [
      { name: "Python", level: 90, category: "language" },
      { name: "JavaScript", level: 85, category: "language" },
      { name: "R", level: 80, category: "language" },
      { name: "SQL", level: 85, category: "language" },
      { name: "Java", level: 70, category: "language" }
    ]
  },
  {
    name: "Machine Learning & AI",
    icon: "🧠",
    skills: [
      { name: "TensorFlow", level: 85, category: "ml" },
      { name: "PyTorch", level: 80, category: "ml" },
      { name: "scikit-learn", level: 90, category: "ml" },
      { name: "NLP", level: 85, category: "ml" },
      { name: "Computer Vision", level: 75, category: "ml" }
    ]
  },
  {
    name: "Data Analysis & Visualization",
    icon: "📊",
    skills: [
      { name: "Pandas", level: 95, category: "data" },
      { name: "NumPy", level: 90, category: "data" },
      { name: "Matplotlib", level: 85, category: "data" },
      { name: "Tableau", level: 80, category: "data" },
      { name: "Power BI", level: 75, category: "data" }
    ]
  },
  {
    name: "Databases & Big Data",
    icon: "🗄️",
    skills: [
      { name: "PostgreSQL", level: 85, category: "db" },
      { name: "MongoDB", level: 80, category: "db" },
      { name: "Hadoop", level: 70, category: "db" },
      { name: "Spark", level: 75, category: "db" },
      { name: "Redis", level: 65, category: "db" }
    ]
  },
  {
    name: "DevOps & Cloud",
    icon: "☁️",
    skills: [
      { name: "Docker", level: 80, category: "devops" },
      { name: "AWS", level: 75, category: "devops" },
      { name: "Git", level: 90, category: "devops" },
      { name: "CI/CD", level: 70, category: "devops" },
      { name: "Kubernetes", level: 65, category: "devops" }
    ]
  },
  {
    name: "Web Development",
    icon: "🌐",
    skills: [
      { name: "React", level: 85, category: "web" },
      { name: "Flask", level: 80, category: "web" },
      { name: "FastAPI", level: 75, category: "web" },
      { name: "HTML/CSS", level: 85, category: "web" },
      { name: "Node.js", level: 70, category: "web" }
    ]
  }
]

// Computed properties
const currentYear = computed(() => new Date().getFullYear())

// Methods
const toggleMenu = () => {
  isOpen.value = !isOpen.value
}

const toggleDarkMode = () => {
  darkMode.value = !darkMode.value
  const root = document.documentElement
  if (darkMode.value) {
    root.classList.add('dark-mode')
  } else {
    root.classList.remove('dark-mode')
  }
}

const scrollToSection = (id) => {
  const element = document.getElementById(id)
  element?.scrollIntoView({ behavior: 'smooth' })
}

const openModal = (project) => {
  selectedProject.value = project
  document.body.style.overflow = 'hidden'
}

const closeModal = () => {
  selectedProject.value = null
  document.body.style.overflow = 'auto'
}

const handleSubmit = async () => {
  isSubmitting.value = true
  submitError.value = ''

  try {
    // Simulate form submission
    await new Promise(resolve => setTimeout(resolve, 1000))

    submitSuccess.value = true
    formData.value = { name: '', email: '', subject: '', message: '' }

    setTimeout(() => {
      submitSuccess.value = false
    }, 5000)
  } catch (error) {
    submitError.value = 'Failed to send message. Please try again.'
  } finally {
    isSubmitting.value = false
  }
}

const handleScroll = () => {
  scrolled.value = window.scrollY > 10
}

// Lifecycle hooks
onMounted(() => {
  window.addEventListener('scroll', handleScroll)

  // Initialize typing animation
  if (typedElement.value) {
    let currentIndex = 0
    const strings = ['Data Scientist', 'AI Specialist', 'Machine Learning Engineer']
    let currentString = ''
    let isDeleting = false

    const type = () => {
      const fullString = strings[currentIndex]

      if (isDeleting) {
        currentString = fullString.substring(0, currentString.length - 1)
      } else {
        currentString = fullString.substring(0, currentString.length + 1)
      }

      typedElement.value.textContent = currentString

      let typeSpeed = isDeleting ? 30 : 50

      if (!isDeleting && currentString === fullString) {
        typeSpeed = 2000
        isDeleting = true
      } else if (isDeleting && currentString === '') {
        isDeleting = false
        currentIndex = (currentIndex + 1) % strings.length
        typeSpeed = 500
      }

      setTimeout(type, typeSpeed)
    }

    type()
  }
})

onUnmounted(() => {
  window.removeEventListener('scroll', handleScroll)
})
</script>

<style>
/* CSS Reset and Base Styles */
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

:root {
  --primary-color: #3b82f6;
  --secondary-color: #10b981;
  --accent-color: #06b6d4;
  --text-primary: #1f2937;
  --text-secondary: #6b7280;
  --bg-primary: #ffffff;
  --bg-secondary: #f9fafb;
  --bg-tertiary: #f3f4f6;
  --border-color: #e5e7eb;
  --shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1);
  --shadow-lg: 0 10px 15px -3px rgba(0, 0, 0, 0.1);
  --transition: all 0.3s ease;
}

.dark-mode {
  --text-primary: #f9fafb;
  --text-secondary: #d1d5db;
  --bg-primary: #111827;
  --bg-secondary: #1f2937;
  --bg-tertiary: #374151;
  --border-color: #4b5563;
  --shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.3);
  --shadow-lg: 0 10px 15px -3px rgba(0, 0, 0, 0.3);
}

html {
  scroll-behavior: smooth;
}

body {
  font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
  line-height: 1.6;
  color: var(--text-primary);
  background-color: var(--bg-primary);
  transition: var(--transition);
}

.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 1rem;
}

.sr-only {
  position: absolute;
  width: 1px;
  height: 1px;
  padding: 0;
  margin: -1px;
  overflow: hidden;
  clip: rect(0, 0, 0, 0);
  white-space: nowrap;
  border: 0;
}

/* Navbar Styles */
.navbar {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  z-index: 1000;
  transition: var(--transition);
  background-color: transparent;
}

.navbar-scrolled {
  background-color: rgba(255, 255, 255, 0.9);
  backdrop-filter: blur(10px);
  box-shadow: var(--shadow);
}

.dark-mode .navbar-scrolled {
  background-color: rgba(17, 24, 39, 0.9);
}

.nav-content {
  display: flex;
  align-items: center;
  justify-content: space-between;
  height: 4rem;
}

.logo a {
  font-size: 1.25rem;
  font-weight: 700;
  color: var(--primary-color);
  text-decoration: none;
}

.nav-desktop {
  display: none;
}

.nav-links {
  display: flex;
  align-items: center;
  gap: 1rem;
}

.nav-link {
  padding: 0.5rem 0.75rem;
  color: var(--text-secondary);
  text-decoration: none;
  border-radius: 0.375rem;
  transition: var(--transition);
  font-weight: 500;
}

.nav-link:hover {
  color: var(--primary-color);
}

.theme-toggle {
  padding: 0.5rem;
  background: none;
  border: none;
  border-radius: 50%;
  cursor: pointer;
  font-size: 1.25rem;
  transition: var(--transition);
}

.theme-toggle:hover {
  background-color: var(--bg-tertiary);
}

.nav-mobile {
  display: flex;
  align-items: center;
  gap: 0.5rem;
}

.mobile-theme {
  margin-right: 0.5rem;
}

.menu-toggle {
  padding: 0.5rem;
  background: none;
  border: none;
  cursor: pointer;
  font-size: 1.5rem;
  color: var(--text-primary);
}

.mobile-menu {
  background-color: var(--bg-primary);
  box-shadow: var(--shadow-lg);
}

.mobile-menu-content {
  padding: 1rem;
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
}

.mobile-link {
  padding: 0.75rem;
  color: var(--text-secondary);
  text-decoration: none;
  border-radius: 0.375rem;
  transition: var(--transition);
  font-weight: 500;
}

.mobile-link:hover {
  color: var(--primary-color);
  background-color: var(--bg-tertiary);
}

@media (min-width: 768px) {
  .nav-desktop {
    display: block;
  }

  .nav-mobile {
    display: none;
  }
}

/* Hero Section */
.hero {
  min-height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
  position: relative;
  background: linear-gradient(135deg, var(--bg-primary) 0%, var(--bg-secondary) 100%);
  padding: 6rem 0 4rem;
}

.hero-bg {
  position: absolute;
  inset: 0;
  background-image:
    linear-gradient(to right, rgba(59, 130, 246, 0.05) 1px, transparent 1px),
    linear-gradient(to bottom, rgba(59, 130, 246, 0.05) 1px, transparent 1px);
  background-size: 40px 40px;
  opacity: 0.5;
}

.hero-content {
  display: grid;
  grid-template-columns: 1fr;
  gap: 3rem;
  align-items: center;
}

.hero-title {
  font-size: 3rem;
  font-weight: 700;
  margin-bottom: 1.5rem;
  background: linear-gradient(135deg, var(--primary-color) 0%, var(--accent-color) 100%);
  -webkit-background-clip: text;
  background-clip: text;
  -webkit-text-fill-color: transparent;
  line-height: 1.1;
}

.hero-subtitle {
  height: 4rem;
  margin-bottom: 2rem;
}

.hero-subtitle h2 {
  font-size: 1.5rem;
  color: var(--text-secondary);
  font-weight: 500;
}

.typed-text {
  color: var(--primary-color);
  font-weight: 600;
}

.cursor {
  animation: blink 1s infinite;
  color: var(--primary-color);
}

@keyframes blink {

  0%,
  50% {
    opacity: 1;
  }

  51%,
  100% {
    opacity: 0;
  }
}

.hero-description {
  font-size: 1.125rem;
  color: var(--text-secondary);
  margin-bottom: 2.5rem;
  max-width: 32rem;
}

.hero-buttons {
  display: flex;
  flex-direction: column;
  gap: 1rem;
}

.hero-image {
  display: flex;
  justify-content: center;
}

.image-container {
  position: relative;
  max-width: 500px;
  width: 100%;
}

.image-container img {
  width: 100%;
  height: auto;
  object-fit: contain;
  transition: var(--transition);
}

.scroll-indicator {
  position: absolute;
  bottom: 2rem;
  left: 50%;
  transform: translateX(-50%);
  animation: bounce 2s infinite;
}

.scroll-btn {
  padding: 0.75rem;
  background-color: var(--bg-tertiary);
  border: none;
  border-radius: 50%;
  cursor: pointer;
  box-shadow: var(--shadow);
  color: var(--primary-color);
  font-size: 1.5rem;
}

@keyframes bounce {

  0%,
  20%,
  53%,
  80%,
  100% {
    transform: translateX(-50%) translateY(0);
  }

  40%,
  43% {
    transform: translateX(-50%) translateY(-10px);
  }

  70% {
    transform: translateX(-50%) translateY(-5px);
  }

  90% {
    transform: translateX(-50%) translateY(-2px);
  }
}

@media (min-width: 768px) {
  .hero-content {
    grid-template-columns: 1fr 1fr;
  }

  .hero-title {
    font-size: 4.5rem;
  }

  .hero-subtitle h2 {
    font-size: 2rem;
  }

  .hero-buttons {
    flex-direction: row;
  }
}

/* Button Styles */
.btn {
  padding: 0.75rem 2rem;
  border: none;
  border-radius: 9999px;
  font-weight: 600;
  text-decoration: none;
  display: inline-flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
  transition: var(--transition);
  font-size: 1rem;
}

.btn-primary {
  background-color: var(--primary-color);
  color: white;
}

.btn-primary:hover {
  background-color: #2563eb;
  transform: translateY(-1px);
}

.btn-secondary {
  background-color: var(--bg-tertiary);
  color: var(--text-primary);
}

.btn-secondary:hover {
  background-color: var(--border-color);
  transform: translateY(-1px);
}

.btn-dark {
  background-color: var(--text-primary);
  color: var(--bg-primary);
}

.btn-dark:hover {
  opacity: 0.9;
  transform: translateY(-1px);
}

.btn-full {
  width: 100%;
}

.btn-disabled {
  opacity: 0.6;
  cursor: not-allowed;
}

.btn-disabled:hover {
  transform: none;
}

/* Section Styles */
.section {
  padding: 5rem 0;
  background-color: var(--bg-primary);
}

.section-alt {
  background-color: var(--bg-secondary);
}

.section-header {
  text-align: center;
  margin-bottom: 4rem;
}

.section-title {
  font-size: 2.5rem;
  font-weight: 700;
  margin-bottom: 1rem;
  color: var(--text-primary);
}

.section-divider {
  width: 4rem;
  height: 0.25rem;
  background-color: var(--primary-color);
  margin: 0 auto 1rem;
  border-radius: 9999px;
}

.section-description {
  font-size: 1.125rem;
  color: var(--text-secondary);
  max-width: 32rem;
  margin: 0 auto;
}

/* About Section */
.about-content {
  display: grid;
  grid-template-columns: 1fr;
  gap: 2.5rem;
  align-items: center;
}

.about-image {
  display: flex;
  justify-content: center;
}

.image-frame {
  background: linear-gradient(135deg, var(--primary-color), var(--accent-color));
  border-radius: 1rem;
  padding: 0.25rem;
  max-width: 400px;
  width: 100%;
}

.image-wrapper {
  background-color: var(--bg-primary);
  border-radius: 0.75rem;
  overflow: hidden;
  padding: 1rem;
  display: flex;
  align-items: center;
  justify-content: center;
}

.image-wrapper img {
  width: 100%;
  height: auto;
  border-radius: 0.5rem;
  box-shadow: var(--shadow-lg);
}

.about-subtitle {
  font-size: 1.5rem;
  font-weight: 600;
  margin-bottom: 1rem;
  color: var(--text-primary);
}

.about-paragraph {
  color: var(--text-secondary);
  margin-bottom: 1.5rem;
  line-height: 1.7;
}

.about-details {
  display: grid;
  grid-template-columns: 1fr;
  gap: 1.5rem;
}

.detail-column h4 {
  font-weight: 600;
  color: var(--text-primary);
  margin-bottom: 0.5rem;
}

.detail-column ul {
  list-style: none;
}

.detail-column li {
  color: var(--text-secondary);
  margin-bottom: 0.5rem;
}

@media (min-width: 768px) {
  .about-content {
    grid-template-columns: 1fr 1fr;
  }

  .about-details {
    grid-template-columns: 1fr 1fr;
  }
}

/* Timeline Styles */
.timeline {
  position: relative;
  max-width: 1000px;
  margin: 0 auto;
}

.timeline-line {
  position: absolute;
  left: 50%;
  transform: translateX(-50%);
  width: 2px;
  height: 100%;
  background-color: var(--border-color);
  display: none;
}

.timeline-items {
  display: flex;
  flex-direction: column;
  gap: 3rem;
}

.timeline-item {
  position: relative;
  display: flex;
  align-items: flex-start;
}

.timeline-dot {
  position: absolute;
  left: 50%;
  transform: translateX(-50%);
  width: 1.5rem;
  height: 1.5rem;
  background-color: var(--primary-color);
  border-radius: 50%;
  z-index: 10;
  margin-top: 1.5rem;
  display: none;
}

.timeline-content {
  width: 100%;
}

.timeline-card {
  background-color: var(--bg-primary);
  padding: 1.5rem;
  border-radius: 0.75rem;
  box-shadow: var(--shadow-lg);
  transition: var(--transition);
}

.timeline-card:hover {
  transform: translateY(-2px);
  box-shadow: 0 20px 25px -5px rgba(0, 0, 0, 0.1);
}

.card-header {
  display: flex;
  align-items: center;
  margin-bottom: 1rem;
}

.card-icon {
  font-size: 1.25rem;
  margin-right: 0.75rem;
}

.card-header h3 {
  font-size: 1.25rem;
  font-weight: 700;
  color: var(--text-primary);
}

.company {
  font-weight: 600;
  color: var(--text-secondary);
  margin-bottom: 0.25rem;
}

.meta-info {
  display: flex;
  align-items: center;
  font-size: 0.875rem;
  color: var(--text-secondary);
  margin-bottom: 1rem;
}

.separator {
  margin: 0 0.5rem;
}

.card-description {
  list-style: none;
}

.card-description li {
  display: flex;
  align-items: flex-start;
  color: var(--text-secondary);
  margin-bottom: 0.5rem;
}

.bullet {
  color: var(--primary-color);
  margin-right: 0.5rem;
  margin-top: 0.125rem;
}

@media (min-width: 768px) {
  .timeline-line {
    display: block;
  }

  .timeline-dot {
    display: block;
  }

  .timeline-left .timeline-content {
    margin-right: 3rem;
  }

  .timeline-right .timeline-content {
    margin-left: 3rem;
  }

  .timeline-left {
    flex-direction: row;
  }

  .timeline-right {
    flex-direction: row-reverse;
  }

  .timeline-content {
    width: calc(50% - 1rem);
  }
}

/* Projects Section */
.projects-grid {
  display: grid;
  grid-template-columns: 1fr;
  gap: 2rem;
}

.project-card {
  background-color: var(--bg-secondary);
  border-radius: 0.75rem;
  overflow: hidden;
  box-shadow: var(--shadow-lg);
  transition: var(--transition);
}

.project-card:hover {
  transform: translateY(-4px);
  box-shadow: 0 20px 25px -5px rgba(0, 0, 0, 0.1);
}

.project-image {
  height: 15rem;
  overflow: hidden;
}

.project-image img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: var(--transition);
}

.project-card:hover .project-image img {
  transform: scale(1.05);
}

.project-content {
  padding: 1.5rem;
}

.project-title {
  font-size: 1.25rem;
  font-weight: 700;
  margin-bottom: 0.5rem;
  color: var(--text-primary);
}

.project-description {
  color: var(--text-secondary);
  margin-bottom: 1rem;
}

.project-tags {
  display: flex;
  flex-wrap: wrap;
  gap: 0.5rem;
  margin-bottom: 1rem;
}

.tag {
  padding: 0.25rem 0.75rem;
  font-size: 0.75rem;
  font-weight: 500;
  border-radius: 9999px;
  background-color: rgba(59, 130, 246, 0.1);
  color: var(--primary-color);
}

.project-actions {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.project-details {
  background: none;
  border: none;
  color: var(--primary-color);
  font-weight: 600;
  cursor: pointer;
  display: flex;
  align-items: center;
  transition: var(--transition);
}

.project-details:hover {
  color: #2563eb;
}

.project-links {
  display: flex;
  gap: 0.75rem;
}

.project-links a {
  color: var(--text-secondary);
  font-size: 1.25rem;
  transition: var(--transition);
  text-decoration: none;
}

.project-links a:hover {
  color: var(--text-primary);
}

@media (min-width: 768px) {
  .projects-grid {
    grid-template-columns: repeat(2, 1fr);
  }
}

/* Modal Styles */
.modal-overlay {
  position: fixed;
  inset: 0;
  z-index: 1000;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 1rem;
  background-color: rgba(0, 0, 0, 0.5);
}

.modal-content {
  background-color: var(--bg-primary);
  border-radius: 0.75rem;
  box-shadow: var(--shadow-lg);
  max-width: 64rem;
  width: 100%;
  max-height: 90vh;
  overflow-y: auto;
}

.modal-image {
  height: 18rem;
  overflow: hidden;
}

.modal-image img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.modal-body {
  padding: 2rem;
}

.modal-header {
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
  margin-bottom: 1.5rem;
}

.modal-header h3 {
  font-size: 1.5rem;
  font-weight: 700;
  color: var(--text-primary);
}

.modal-close {
  background: none;
  border: none;
  font-size: 1.5rem;
  cursor: pointer;
  color: var(--text-secondary);
  transition: var(--transition);
}

.modal-close:hover {
  color: var(--text-primary);
}

.modal-tags {
  display: flex;
  flex-wrap: wrap;
  gap: 0.5rem;
  margin-bottom: 1.5rem;
}

.modal-description {
  margin-bottom: 1.5rem;
}

.modal-description p {
  color: var(--text-secondary);
  line-height: 1.7;
}

.modal-actions {
  display: flex;
  gap: 1rem;
}

/* Skills Section */
.skills-grid {
  display: grid;
  grid-template-columns: 1fr;
  gap: 2rem;
  margin-bottom: 4rem;
}

.skill-category {
  background-color: var(--bg-primary);
  border-radius: 0.75rem;
  padding: 1.5rem;
  box-shadow: var(--shadow-lg);
  transition: var(--transition);
}

.skill-category:hover {
  transform: translateY(-2px);
  box-shadow: 0 20px 25px -5px rgba(0, 0, 0, 0.1);
}

.category-header {
  display: flex;
  align-items: center;
  margin-bottom: 1.5rem;
}

.category-icon {
  padding: 0.75rem;
  border-radius: 0.5rem;
  background-color: rgba(59, 130, 246, 0.1);
  margin-right: 1rem;
  font-size: 1.5rem;
}

.category-header h3 {
  font-size: 1.25rem;
  font-weight: 700;
  color: var(--text-primary);
}

.skill-item {
  margin-bottom: 0.75rem;
}

.skill-info {
  display: flex;
  justify-content: space-between;
  margin-bottom: 0.25rem;
}

.skill-name {
  font-weight: 500;
  color: var(--text-secondary);
}

.skill-level {
  font-size: 0.875rem;
  color: var(--text-secondary);
}

.skill-bar {
  width: 100%;
  height: 0.625rem;
  background-color: var(--bg-tertiary);
  border-radius: 9999px;
  overflow: hidden;
}

.skill-progress {
  height: 100%;
  border-radius: 9999px;
  transition: width 1s ease-in-out;
}

.skill-language {
  background-color: var(--primary-color);
}

.skill-ml {
  background-color: #8b5cf6;
}

.skill-data {
  background-color: var(--secondary-color);
}

.skill-db {
  background-color: #f59e0b;
}

.skill-devops {
  background-color: #ef4444;
}

.skill-web {
  background-color: var(--accent-color);
}

.additional-skills {
  background-color: var(--bg-primary);
  border-radius: 0.75rem;
  padding: 2rem;
  box-shadow: var(--shadow-lg);
}

.additional-title {
  font-size: 1.5rem;
  font-weight: 700;
  margin-bottom: 1.5rem;
  text-align: center;
  color: var(--text-primary);
}

.additional-content {
  display: grid;
  grid-template-columns: 1fr;
  gap: 2rem;
}

.soft-skills h4,
.certifications h4 {
  font-size: 1.125rem;
  font-weight: 600;
  margin-bottom: 1rem;
  color: var(--text-primary);
}

.soft-skills ul,
.certifications ul {
  list-style: none;
}

.soft-skills li,
.certifications li {
  display: flex;
  align-items: flex-start;
  color: var(--text-secondary);
  margin-bottom: 0.5rem;
}

@media (min-width: 768px) {
  .skills-grid {
    grid-template-columns: repeat(2, 1fr);
  }

  .additional-content {
    grid-template-columns: repeat(2, 1fr);
  }
}

@media (min-width: 1024px) {
  .skills-grid {
    grid-template-columns: repeat(3, 1fr);
  }
}

/* Contact Section */
.contact-content {
  display: grid;
  grid-template-columns: 1fr;
  gap: 2.5rem;
}

.contact-card {
  background-color: var(--bg-secondary);
  border-radius: 0.75rem;
  padding: 2rem;
  box-shadow: var(--shadow-lg);
  height: fit-content;
}

.contact-card h3 {
  font-size: 1.5rem;
  font-weight: 700;
  margin-bottom: 1.5rem;
  color: var(--text-primary);
}

.contact-items {
  margin-bottom: 2.5rem;
}

.contact-item {
  display: flex;
  align-items: flex-start;
  margin-bottom: 1.5rem;
}

.contact-icon {
  padding: 0.75rem;
  border-radius: 0.5rem;
  background-color: rgba(59, 130, 246, 0.1);
  margin-right: 1rem;
  font-size: 1.25rem;
}

.contact-details h4 {
  font-weight: 600;
  color: var(--text-primary);
  margin-bottom: 0.25rem;
}

.contact-details p,
.contact-details a {
  color: var(--text-secondary);
  text-decoration: none;
  transition: var(--transition);
}

.contact-details a:hover {
  color: var(--primary-color);
}

.social-links h4 {
  font-weight: 600;
  color: var(--text-primary);
  margin-bottom: 1rem;
}

.social-icons {
  display: flex;
  gap: 1rem;
}

.social-icons a {
  padding: 0.75rem;
  border-radius: 0.5rem;
  background-color: var(--bg-tertiary);
  color: var(--text-secondary);
  text-decoration: none;
  font-size: 1.25rem;
  transition: var(--transition);
}

.social-icons a:hover {
  background-color: rgba(59, 130, 246, 0.1);
  color: var(--primary-color);
}

/* Form Styles */
.contact-form {
  background-color: var(--bg-secondary);
  border-radius: 0.75rem;
  padding: 2rem;
  box-shadow: var(--shadow-lg);
}

.contact-form h3 {
  font-size: 1.5rem;
  font-weight: 700;
  margin-bottom: 1.5rem;
  color: var(--text-primary);
}

.alert {
  padding: 1rem;
  border-radius: 0.5rem;
  margin-bottom: 1.5rem;
}

.alert-success {
  background-color: rgba(16, 185, 129, 0.1);
  color: var(--secondary-color);
}

.alert-error {
  background-color: rgba(239, 68, 68, 0.1);
  color: #ef4444;
}

.form-fields {
  display: flex;
  flex-direction: column;
  gap: 1rem;
}

.form-group {
  display: flex;
  flex-direction: column;
}

.form-group label {
  font-weight: 500;
  color: var(--text-secondary);
  margin-bottom: 0.25rem;
}

.form-group input,
.form-group textarea {
  padding: 0.75rem 1rem;
  border: 1px solid var(--border-color);
  border-radius: 0.5rem;
  background-color: var(--bg-primary);
  color: var(--text-primary);
  transition: var(--transition);
}

.form-group input:focus,
.form-group textarea:focus {
  outline: none;
  border-color: var(--primary-color);
  box-shadow: 0 0 0 3px rgba(59, 130, 246, 0.1);
}

.form-group textarea {
  resize: vertical;
  min-height: 120px;
}

@media (min-width: 768px) {
  .contact-content {
    grid-template-columns: 1fr 1fr;
  }
}

/* Footer */
.footer {
  background-color: var(--text-primary);
  color: var(--bg-primary);
  padding: 2rem 0;
}

.footer-content {
  text-align: center;
}

.footer-content p {
  color: var(--text-secondary);
}

/* Animations */
@keyframes fadeIn {
  from {
    opacity: 0;
    transform: translateY(20px);
  }

  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.fade-in {
  animation: fadeIn 0.6s ease-out forwards;
}

/* Responsive Design */
@media (max-width: 640px) {
  .container {
    padding: 0 0.75rem;
  }

  .hero-title {
    font-size: 2.5rem;
  }

  .section-title {
    font-size: 2rem;
  }

  .hero-buttons {
    gap: 0.75rem;
  }

  .btn {
    padding: 0.625rem 1.5rem;
    font-size: 0.875rem;
  }
}

/* Print Styles */
@media print {

  .navbar,
  .scroll-indicator,
  .modal-overlay {
    display: none;
  }

  .section {
    page-break-inside: avoid;
  }

  body {
    font-size: 12pt;
    line-height: 1.4;
  }
}

/* Accessibility */
@media (prefers-reduced-motion: reduce) {
  * {
    animation-duration: 0.01ms !important;
    animation-iteration-count: 1 !important;
    transition-duration: 0.01ms !important;
  }

  .scroll-indicator {
    animation: none;
  }

  .cursor {
    animation: none;
  }
}

/* Focus styles for keyboard navigation */
button:focus,
a:focus,
input:focus,
textarea:focus {
  outline: 2px solid var(--primary-color);
  outline-offset: 2px;
}

/* High contrast mode support */
@media (prefers-contrast: high) {
  :root {
    --shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.3);
    --shadow-lg: 0 10px 15px -3px rgba(0, 0, 0, 0.3);
  }

  .btn {
    border: 2px solid currentColor;
  }

  .skill-bar {
    border: 1px solid var(--text-primary);
  }
}

/* Loading states */
.loading {
  opacity: 0.6;
  pointer-events: none;
}

.loading::after {
  content: '';
  position: absolute;
  top: 50%;
  left: 50%;
  width: 20px;
  height: 20px;
  margin: -10px 0 0 -10px;
  border: 2px solid var(--primary-color);
  border-radius: 50%;
  border-top-color: transparent;
  animation: spin 1s linear infinite;
}

@keyframes spin {
  to {
    transform: rotate(360deg);
  }
}

/* Utility classes */
.text-center {
  text-align: center;
}

.text-left {
  text-align: left;
}

.text-right {
  text-align: right;
}

.mb-1 {
  margin-bottom: 0.25rem;
}

.mb-2 {
  margin-bottom: 0.5rem;
}

.mb-3 {
  margin-bottom: 0.75rem;
}

.mb-4 {
  margin-bottom: 1rem;
}

.mt-1 {
  margin-top: 0.25rem;
}

.mt-2 {
  margin-top: 0.5rem;
}

.mt-3 {
  margin-top: 0.75rem;
}

.mt-4 {
  margin-top: 1rem;
}

.hidden {
  display: none;
}

.block {
  display: block;
}

.flex {
  display: flex;
}

.grid {
  display: grid;
}

.w-full {
  width: 100%;
}

.h-full {
  height: 100%;
}

.relative {
  position: relative;
}

.absolute {
  position: absolute;
}

.fixed {
  position: fixed;
}

.z-10 {
  z-index: 10;
}

.z-20 {
  z-index: 20;
}

.z-50 {
  z-index: 50;
}
</style>
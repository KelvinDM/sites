<template>
  <div class="site">
    <header :class="['header', { 'header-scrolled': isScrolled }]">
      <div class="container header-inner">
        <div class="brand">
          <span class="brand-title">Thays Andrade</span>
          <span class="brand-subtitle">Advocacia &amp; Consultoria</span>
        </div>

        <nav class="desktop-nav">
          <a
            v-for="item in menuItems"
            :key="item.id"
            :href="item.href"
            class="nav-link"
          >
            {{ item.label }}
          </a>
        </nav>

        <div class="header-actions">
          <button
            class="theme-toggle"
            type="button"
            :aria-label="isDarkMode ? 'Ativar tema claro' : 'Ativar tema escuro'"
            @click="toggleTheme"
          >
            <Sun v-if="isDarkMode" :size="20" weight="bold" />
            <Moon v-else :size="20" weight="bold" />
          </button>

          <button class="menu-button" @click="mobileMenuOpen = true" aria-label="Abrir menu" type="button">
            <List :size="28" weight="bold" />
          </button>
        </div>
      </div>
    </header>

    <transition name="fade">
      <div v-if="mobileMenuOpen" class="mobile-overlay">
        <button class="close-button" @click="mobileMenuOpen = false" aria-label="Fechar menu" type="button">
          <X :size="34" weight="bold" />
        </button>

        <nav class="mobile-nav">
          <a
            v-for="item in menuItems"
            :key="item.id"
            :href="item.href"
            @click="mobileMenuOpen = false"
          >
            {{ item.label }}
          </a>
        </nav>
      </div>
    </transition>

    <main>
      <section id="inicio" class="hero">
        <div class="hero-bg-shape"></div>

        <div class="container hero-grid">
          <div class="hero-content">
            <p class="eyebrow">Excelência e Dedicação</p>

            <h1 class="hero-title">
              Soluções Jurídicas
              <span>Personalizadas</span>
            </h1>

            <p class="hero-text">
              Proteção jurídica especializada com foco na resolução estratégica
              e no atendimento humanizado.
            </p>

            <div class="hero-actions">
              <a href="#contato" class="button button-primary">Agendar Consultoria</a>
              <a href="#atuacao" class="button button-outline">Áreas de Atuação</a>
            </div>
          </div>

          <div class="hero-image-wrap">
            <div class="hero-frame"></div>
            <img
              class="hero-image"
              src="/src/assets/images/IMAGE_PERFIL.png"
              alt="Advogada em ambiente profissional"
            />
          </div>
        </div>
      </section>

      <section class="stats">
        <div class="container stats-grid">
          <div v-for="stat in stats" :key="stat.label" class="stat-item">
            <strong>{{ stat.value }}</strong>
            <span>{{ stat.label }}</span>
          </div>
        </div>
      </section>

      <section id="sobre" class="about section">
        <div class="container about-grid">
          <div class="about-text">
            <p class="eyebrow">A Advogada</p>
            <h2 class="section-title">Dra. Thays Andrade</h2>

            <p>
              Dra. Thays Andrade é reconhecida pela sua abordagem técnica rigorosa
              e pelo compromisso com os interesses dos seus clientes.
            </p>

            <p>
              Com atendimento direto e acompanhamento próximo, cada caso recebe
              análise individualizada, trazendo mais segurança, clareza e confiança.
            </p>

            <ul class="highlights">
              <li v-for="item in highlights" :key="item">
                <span class="check">
                  <CheckCircle :size="18" weight="fill" />
                </span>
                <span>{{ item }}</span>
              </li>
            </ul>
          </div>

          <div class="about-images">
            <img
              src="https://images.unsplash.com/photo-1505664194779-8beaceb93744?auto=format&fit=crop&q=80&w=500"
              alt="Ambiente jurídico"
              class="about-image image-one"
            />
            <img
              src="https://images.unsplash.com/photo-1453723490680-d29a5624dd85?auto=format&fit=crop&q=80&w=500"
              alt="Símbolo de justiça"
              class="about-image image-two"
            />
          </div>
        </div>
      </section>

      <section id="atuacao" class="services section services-section">
        <div class="container">
          <div class="section-header">
            <p class="eyebrow">Expertise</p>
            <h2 class="section-title">Áreas de Atuação Especializada</h2>
            <p class="section-text">
              Soluções jurídicas preventivas e contenciosas voltadas à eficiência,
              segurança e proteção de direitos.
            </p>
          </div>

          <div class="services-grid">
            <article v-for="service in services" :key="service.title" class="service-card">
              <div class="service-icon">
                <component :is="service.icon" :size="30" weight="duotone" />
              </div>
              <h3>{{ service.title }}</h3>
              <p>{{ service.description }}</p>
            </article>
          </div>
        </div>
      </section>

      <section id="contato" class="contact section">
        <div class="container contact-grid">
          <div class="contact-info">
            <p class="eyebrow light">Agendamento</p>
            <h2 class="section-title light">Solicite uma Consultoria</h2>
            <p class="contact-text">
              Entre em contato para uma análise detalhada do seu caso, com
              atendimento ágil e confidencial.
            </p>

            <div class="contact-list">
              <div v-for="info in contactInfo" :key="info.label" class="contact-item">
                <span class="contact-icon">
                  <component :is="info.icon" :size="18" weight="fill" />
                </span>
                <div class="contact-item-content">
                  <span class="contact-label">{{ info.label }}</span>
                  <span class="contact-value">{{ info.value }}</span>
                </div>
              </div>
            </div>
          </div>

          <div class="contact-card">
            <form class="contact-form" @submit.prevent="handleSubmit">
              <div class="form-group">
                <label for="name">Nome</label>
                <input id="name" v-model="form.name" type="text" required />
              </div>

              <div class="form-group">
                <label for="phone">Telefone</label>
                <input id="phone" v-model="form.phone" type="tel" required />
              </div>

              <div class="form-group">
                <label for="message">Mensagem</label>
                <textarea id="message" v-model="form.message" rows="4" required></textarea>
              </div>

              <button type="submit" class="button button-primary full-width" :disabled="isSending">
                {{ isSending ? 'Enviando...' : 'Enviar Solicitação' }}
              </button>

              <transition name="fade">
                <p v-if="showSuccess" class="success-message">
                  Mensagem enviada com sucesso!
                </p>
              </transition>
            </form>
          </div>
        </div>
      </section>
    </main>

    <footer class="footer">
      <div class="container footer-inner">
        <div class="brand footer-brand">
          <span class="brand-title">Thays Andrade</span>
          <span class="brand-subtitle">Advocacia Especializada</span>
        </div>

        <p class="footer-oab">OAB/SP 000.000</p>
        <p class="footer-copy">© 2026 Dra. Thays Andrade. Todos os direitos reservados.</p>
      </div>
    </footer>

    <a
      href="https://wa.me/5511987654321"
      target="_blank"
      rel="noopener noreferrer"
      class="whatsapp-button"
      aria-label="WhatsApp"
    >
      <WhatsappLogo :size="30" weight="fill" />
      <span class="sr-only">WhatsApp</span>
    </a>
  </div>
</template>

<script setup>
import { reactive, ref, onMounted, onUnmounted } from 'vue'
import {
  PhCheckCircle as CheckCircle,
  PhEnvelopeSimple as EnvelopeSimple,
  PhHandshake as Handshake,
  PhHeartStraight as HeartStraight,
  PhList as List,
  PhMapPin as MapPin,
  PhMoon as Moon,
  PhPhone as Phone,
  PhScales as Scales,
  PhSun as Sun,
  PhWhatsappLogo as WhatsappLogo,
  PhX as X
} from '@phosphor-icons/vue'

const isScrolled = ref(false)
const mobileMenuOpen = ref(false)
const showSuccess = ref(false)
const isSending = ref(false)
const isDarkMode = ref(false)

const form = reactive({
  name: '',
  phone: '',
  message: ''
})

const menuItems = [
  { id: 1, label: 'Início', href: '#inicio' },
  { id: 2, label: 'Sobre', href: '#sobre' },
  { id: 3, label: 'Atuação', href: '#atuacao' },
  { id: 4, label: 'Contato', href: '#contato' }
]

const stats = [
  { label: 'Anos de Prática', value: '10+' },
  { label: 'Casos Resolvidos', value: '500+' },
  { label: 'Taxa de Sucesso', value: '98%' },
  { label: 'Atendimento Ágil', value: '24h' }
]

const highlights = [
  'Especialista em Direito Civil e Família',
  'Pós-graduada em Processo Civil',
  'Foco em Resolução Extrajudicial'
]

const services = [
  {
    title: 'Direito de Família',
    description: 'Divórcios, pensão alimentícia, guarda e inventários tratados com sensibilidade, estratégia e sigilo.',
    icon: HeartStraight
  },
  {
    title: 'Direito Civil',
    description: 'Contratos, cobranças, indenizações, responsabilidade civil e proteção patrimonial.',
    icon: Scales
  },
  {
    title: 'Direito do Consumidor',
    description: 'Defesa contra abusos, cobranças indevidas, cancelamentos e falhas na prestação de serviço.',
    icon: Handshake
  }
]

const contactInfo = [
  { label: 'Telefone', value: '(11) 98765-4321', icon: Phone },
  { label: 'E-mail', value: 'contato@thaysandrade.adv.br', icon: EnvelopeSimple },
  { label: 'Endereço', value: 'Av. Paulista, 1000 - São Paulo/SP', icon: MapPin }
]

function handleScroll() {
  isScrolled.value = window.scrollY > 20
}

function applyTheme() {
  document.documentElement.setAttribute('data-theme', isDarkMode.value ? 'dark' : 'light')
}

function toggleTheme() {
  isDarkMode.value = !isDarkMode.value
  applyTheme()
  localStorage.setItem('theme', isDarkMode.value ? 'dark' : 'light')
}

function handleSubmit() {
  isSending.value = true

  setTimeout(() => {
    isSending.value = false
    showSuccess.value = true

    form.name = ''
    form.phone = ''
    form.message = ''

    setTimeout(() => {
      showSuccess.value = false
    }, 4000)
  }, 1200)
}

onMounted(() => {
  window.addEventListener('scroll', handleScroll)
  handleScroll()

  const savedTheme = localStorage.getItem('theme')
  isDarkMode.value = savedTheme === 'dark'
  applyTheme()
})

onUnmounted(() => {
  window.removeEventListener('scroll', handleScroll)
})
</script>

<style scoped>
:global(html) {
  scroll-behavior: smooth;
}

:global(body) {
  margin: 0;
  font-family: Arial, Helvetica, sans-serif;
  background: #fdfafb;
  color: #2f2f2f;
  transition: background 0.3s ease, color 0.3s ease;
}

:global(*) {
  box-sizing: border-box;
}

.site {
  min-height: 100vh;
}

.container {
  width: min(1180px, calc(100% - 40px));
  margin: 0 auto;
}

.header {
  position: fixed;
  inset: 0 0 auto 0;
  z-index: 50;
  background: rgba(255, 255, 255, 0.88);
  transition: all 0.3s ease;
  padding: 18px 0;
  backdrop-filter: blur(10px);
}

.header-scrolled {
  background: rgba(255, 255, 255, 0.96);
  box-shadow: 0 6px 24px rgba(0, 0, 0, 0.08);
  padding: 12px 0;
}

.header-inner {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 16px;
}

.header-actions {
  display: flex;
  align-items: center;
  gap: 10px;
}

.theme-toggle,
.menu-button,
.close-button {
  border: 0;
  background: transparent;
  cursor: pointer;
  color: #4a1d24;
  display: inline-flex;
  align-items: center;
  justify-content: center;
}

.theme-toggle {
  width: 42px;
  height: 42px;
  border-radius: 50%;
  background: #f4ecec;
  transition: all 0.25s ease;
}

.theme-toggle:hover {
  transform: translateY(-2px);
}

.brand {
  display: flex;
  flex-direction: column;
}

.brand-title {
  font-family: Georgia, 'Times New Roman', serif;
  font-size: 2rem;
  font-weight: 700;
  letter-spacing: -0.03em;
  color: #4a1d24;
  text-transform: uppercase;
}

.brand-subtitle {
  font-size: 0.7rem;
  letter-spacing: 0.22em;
  text-transform: uppercase;
  color: #9d5c63;
  font-weight: 700;
}

.desktop-nav {
  display: flex;
  gap: 32px;
}

.nav-link {
  position: relative;
  color: #444;
  text-decoration: none;
  text-transform: uppercase;
  font-size: 0.92rem;
  letter-spacing: 0.08em;
  font-weight: 600;
}

.nav-link::after {
  content: '';
  position: absolute;
  left: 0;
  bottom: -6px;
  width: 0;
  height: 2px;
  background: #9d5c63;
  transition: width 0.3s ease;
}

.nav-link:hover::after {
  width: 100%;
}

.menu-button {
  display: none;
}

.mobile-overlay {
  position: fixed;
  inset: 0;
  background: #4a1d24;
  z-index: 60;
  display: flex;
  align-items: center;
  justify-content: center;
}

.close-button {
  position: absolute;
  top: 24px;
  right: 24px;
  color: white;
}

.mobile-nav {
  display: flex;
  flex-direction: column;
  gap: 28px;
  text-align: center;
}

.mobile-nav a {
  color: white;
  text-decoration: none;
  text-transform: uppercase;
  letter-spacing: 0.12em;
  font-size: 1.2rem;
}

.hero {
  position: relative;
  min-height: 100vh;
  display: flex;
  align-items: center;
  overflow: hidden;
  padding: 120px 0 60px;
  background: #fff;
}

.hero-bg-shape {
  position: absolute;
  right: 0;
  top: 0;
  width: 48%;
  height: 100%;
  background: #f4ecec;
  clip-path: polygon(20% 0, 100% 0, 100% 100%, 0% 100%);
}

.hero-grid {
  position: relative;
  z-index: 1;
  display: grid;
  grid-template-columns: 1.1fr 0.9fr;
  gap: 56px;
  align-items: center;
}

.eyebrow {
  color: #9d5c63;
  text-transform: uppercase;
  letter-spacing: 0.18em;
  font-weight: 700;
  margin: 0 0 18px;
}

.eyebrow.light {
  color: #e5c2c7;
}

.hero-title,
.section-title {
  font-family: Georgia, 'Times New Roman', serif;
  color: #4a1d24;
  line-height: 1.08;
  margin: 0 0 24px;
}

.hero-title {
  font-size: clamp(2.8rem, 6vw, 5.2rem);
}

.hero-title span {
  display: block;
  color: #9d5c63;
  font-style: italic;
}

.hero-text,
.section-text,
.contact-text,
.about-text p,
.service-card p,
.contact-value,
.footer-copy,
.footer-oab {
  line-height: 1.7;
}

.hero-text {
  max-width: 620px;
  font-size: 1.1rem;
  margin-bottom: 32px;
}

.hero-actions {
  display: flex;
  flex-wrap: wrap;
  gap: 14px;
}

.button {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  min-height: 54px;
  padding: 0 28px;
  border-radius: 4px;
  text-decoration: none;
  font-weight: 700;
  transition: all 0.25s ease;
}

.button-primary {
  background: #9d5c63;
  color: white;
  border: 1px solid #9d5c63;
}

.button-primary:hover {
  background: #4a1d24;
  border-color: #4a1d24;
  transform: translateY(-2px);
}

.button-outline {
  border: 1px solid #4a1d24;
  color: #4a1d24;
  background: transparent;
}

.button-outline:hover {
  background: #4a1d24;
  color: white;
}

.hero-image-wrap {
  position: relative;
  display: flex;
  justify-content: center;
}

.hero-frame {
  position: absolute;
  width: 450px;
  height: 550px;
  right: 10px;
  bottom: -24px;
  border: 4px solid #9d5c63;
  opacity: 0.45;
}

.hero-image {
  position: relative;
  width: 450px;
  height: 550px;
  object-fit: cover;
  display: block;
  box-shadow: 0 20px 60px rgba(0, 0, 0, 0.18);
  filter: grayscale(100%);
  transition: filter 0.4s ease, transform 0.4s ease;
}

.hero-image-wrap:hover .hero-image {
  filter: grayscale(0%);
  transform: scale(1.01);
}

.stats {
  background: #4a1d24;
  color: white;
  padding: 42px 0;
}

.stats-grid {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 20px;
  text-align: center;
}

.stat-item strong {
  display: block;
  color: #d49aa1;
  font-size: 2rem;
  margin-bottom: 8px;
}

.stat-item span {
  font-size: 0.78rem;
  text-transform: uppercase;
  letter-spacing: 0.16em;
  opacity: 0.8;
}

.section {
  padding: 110px 0;
}

.about {
  background: white;
}

.about-grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 64px;
  align-items: center;
}

.highlights {
  list-style: none;
  padding: 12px 0 0;
  margin: 0;
}

.highlights li {
  display: flex;
  align-items: center;
  gap: 12px;
  margin-bottom: 14px;
}

.check {
  width: 26px;
  height: 26px;
  border-radius: 50%;
  background: #f4ecec;
  color: #9d5c63;
  display: inline-flex;
  align-items: center;
  justify-content: center;
  flex-shrink: 0;
}

.about-images {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 18px;
}

.about-image {
  width: 100%;
  display: block;
  object-fit: cover;
  box-shadow: 0 12px 32px rgba(0, 0, 0, 0.12);
}

.image-one {
  margin-top: 42px;
  border-bottom: 8px solid #9d5c63;
}

.image-two {
  border-top: 8px solid #4a1d24;
}

.services-section {
  background: #fdfafb;
}

.section-header {
  text-align: center;
  max-width: 760px;
  margin: 0 auto 54px;
}

.services-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 28px;
}

.service-card {
  background: white;
  padding: 36px;
  border-bottom: 4px solid transparent;
  box-shadow: 0 6px 22px rgba(0, 0, 0, 0.05);
  transition: all 0.28s ease;
}

.service-card:hover {
  transform: translateY(-6px);
  border-bottom-color: #9d5c63;
  box-shadow: 0 16px 40px rgba(157, 92, 99, 0.14);
}

.service-icon {
  width: 62px;
  height: 62px;
  border-radius: 50%;
  background: #f4ecec;
  color: #9d5c63;
  display: flex;
  align-items: center;
  justify-content: center;
  margin-bottom: 20px;
}

.service-card h3 {
  margin: 0 0 14px;
  color: #4a1d24;
  font-family: Georgia, 'Times New Roman', serif;
  font-size: 1.4rem;
}

.contact {
  background: #4a1d24;
  color: white;
}

.contact-grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 56px;
  align-items: start;
}

.section-title.light {
  color: white;
}

.contact-list {
  display: flex;
  flex-direction: column;
  gap: 20px;
  margin-top: 28px;
}

.contact-item {
  display: flex;
  align-items: flex-start;
  gap: 12px;
}

.contact-icon {
  width: 32px;
  height: 32px;
  border-radius: 50%;
  background: rgba(255, 255, 255, 0.12);
  color: #e5c2c7;
  display: inline-flex;
  align-items: center;
  justify-content: center;
  flex-shrink: 0;
}

.contact-item-content {
  display: flex;
  flex-direction: column;
  gap: 4px;
}

.contact-label {
  color: #e5c2c7;
  font-size: 0.8rem;
  text-transform: uppercase;
  letter-spacing: 0.14em;
  font-weight: 700;
}

.contact-card {
  background: white;
  color: #4a1d24;
  padding: 36px;
  box-shadow: 0 20px 50px rgba(0, 0, 0, 0.18);
}

.contact-form {
  display: flex;
  flex-direction: column;
  gap: 18px;
}

.form-group {
  display: flex;
  flex-direction: column;
  gap: 8px;
}

.form-group label {
  color: #9d5c63;
  font-size: 0.78rem;
  text-transform: uppercase;
  letter-spacing: 0.14em;
  font-weight: 700;
}

.form-group input,
.form-group textarea {
  border: 0;
  border-bottom: 1px solid #d7d7d7;
  padding: 12px 0;
  font-size: 1rem;
  outline: none;
  background: transparent;
  color: #333;
}

.form-group input:focus,
.form-group textarea:focus {
  border-bottom-color: #9d5c63;
}

.full-width {
  width: 100%;
}

.success-message {
  color: #128a47;
  text-align: center;
  font-weight: 700;
  font-style: italic;
  margin: 6px 0 0;
}

.footer {
  background: white;
  border-top: 1px solid #ececec;
  padding: 48px 0;
  text-align: center;
}

.footer-inner {
  display: flex;
  flex-direction: column;
  gap: 12px;
  align-items: center;
}

.footer-brand .brand-title {
  font-size: 1.5rem;
}

.footer-brand .brand-subtitle {
  font-size: 0.55rem;
}

.whatsapp-button {
  position: fixed;
  right: 26px;
  bottom: 26px;
  z-index: 40;
  background: #25d366;
  color: white;
  text-decoration: none;
  width: 64px;
  height: 64px;
  border-radius: 50%;
  display: inline-flex;
  align-items: center;
  justify-content: center;
  box-shadow: 0 14px 28px rgba(0, 0, 0, 0.18);
  transition: transform 0.25s ease;
}

.whatsapp-button:hover {
  transform: translateY(-3px);
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

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.3s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}

:global([data-theme='dark']) body {
  background: #101014;
  color: #ececf2;
}

:global([data-theme='dark']) .header {
  background: rgba(16, 16, 20, 0.88);
}

:global([data-theme='dark']) .header-scrolled {
  background: rgba(16, 16, 20, 0.96);
  box-shadow: 0 6px 24px rgba(0, 0, 0, 0.35);
}

:global([data-theme='dark']) .brand-title,
:global([data-theme='dark']) .hero-title,
:global([data-theme='dark']) .section-title,
:global([data-theme='dark']) .service-card h3,
:global([data-theme='dark']) .button-outline {
  color: #f4dce0;
}

:global([data-theme='dark']) .brand-subtitle,
:global([data-theme='dark']) .eyebrow,
:global([data-theme='dark']) .hero-title span,
:global([data-theme='dark']) .contact-label,
:global([data-theme='dark']) .contact-icon {
  color: #d69da4;
}

:global([data-theme='dark']) .theme-toggle {
  background: #30252a;
  color: #f1d8dc;
}

:global([data-theme='dark']) .nav-link,
:global([data-theme='dark']) .hero-text,
:global([data-theme='dark']) .section-text,
:global([data-theme='dark']) .about-text p,
:global([data-theme='dark']) .service-card p,
:global([data-theme='dark']) .contact-value,
:global([data-theme='dark']) .footer-copy,
:global([data-theme='dark']) .footer-oab {
  color: #d9d9df;
}

:global([data-theme='dark']) .hero,
:global([data-theme='dark']) .about,
:global([data-theme='dark']) .footer {
  background: #17171c;
}

:global([data-theme='dark']) .hero-bg-shape,
:global([data-theme='dark']) .service-icon,
:global([data-theme='dark']) .check {
  background: #30252a;
}

:global([data-theme='dark']) .stats,
:global([data-theme='dark']) .contact {
  background: #221218;
}

:global([data-theme='dark']) .services-section {
  background: #121216;
}

:global([data-theme='dark']) .service-card,
:global([data-theme='dark']) .contact-card {
  background: #1f1f25;
  color: #ececf2;
  box-shadow: 0 16px 40px rgba(0, 0, 0, 0.35);
}

:global([data-theme='dark']) .contact-card .form-group label {
  color: #d69da4;
}

:global([data-theme='dark']) .form-group input,
:global([data-theme='dark']) .form-group textarea {
  border-bottom-color: #4a4a55;
  color: #ececf2;
}

:global([data-theme='dark']) .form-group input:focus,
:global([data-theme='dark']) .form-group textarea:focus {
  border-bottom-color: #d69da4;
}

:global([data-theme='dark']) .button-outline {
  border-color: #f4dce0;
}

:global([data-theme='dark']) .button-outline:hover {
  background: #f4dce0;
  color: #1f1f25;
}

:global([data-theme='dark']) .footer {
  border-top-color: #2c2c35;
}

@media (max-width: 1024px) {
  .hero-grid,
  .about-grid,
  .contact-grid,
  .services-grid {
    grid-template-columns: 1fr;
  }

  .hero-image-wrap {
    margin-top: 10px;
  }

  .hero-bg-shape {
    display: none;
  }

  .stats-grid {
    grid-template-columns: repeat(2, 1fr);
  }
}

@media (max-width: 768px) {
  .desktop-nav {
    display: none;
  }

  .menu-button {
    display: inline-flex;
  }

  .brand-title {
    font-size: 1.4rem;
  }

  .hero {
    padding-top: 120px;
  }

  .hero-title {
    font-size: 2.5rem;
  }

  .hero-frame,
  .hero-image {
    width: 100%;
    max-width: 380px;
    height: auto;
  }

  .hero-frame {
    display: none;
  }

  .about-images {
    grid-template-columns: 1fr;
  }

  .image-one {
    margin-top: 0;
  }

  .section,
  .contact,
  .about,
  .services-section {
    padding-top: 80px;
    padding-bottom: 80px;
  }

  .contact-card {
    padding: 24px;
  }
}

@media (max-width: 520px) {
  .container {
    width: min(100% - 24px, 1180px);
  }

  .stats-grid {
    grid-template-columns: 1fr;
  }

  .hero-actions {
    flex-direction: column;
  }

  .button {
    width: 100%;
  }

  .whatsapp-button {
    right: 16px;
    bottom: 16px;
    width: 58px;
    height: 58px;
  }
}
</style>

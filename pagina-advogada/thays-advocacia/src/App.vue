<template>
  <div class="app" :class="`theme-${theme}`">
    <div class="topbar">
      <div class="container topbar__inner">
        <!--<span>Atendimento com agendamento • OAB/MS 00.000</span>
        <button class="themeBtn" type="button" @click="toggleTheme">
          {{ theme === 'dark' ? 'Modo claro' : 'Modo escuro' }}
        </button>
        -->
      </div>
    </div>

    <header class="header">
      <div class="container header__inner">
        <a class="brand" href="#inicio" aria-label="Ir para o inicio">
          <LogoMark class="logo" />
          <div class="brand__text">
            <div class="brand__name">Thays Andrade</div>
            <div class="brand__sub">Advogada</div>
          </div>
        </a>

        <nav class="nav" aria-label="Navegacao principal">
          <a href="#inicio">Inicio</a>
          <a href="#filosofia">Filosofia</a>
          <a href="#atuacao">Areas de atuacao</a>
          <a href="#informativos">Informativos</a>
          <a href="#contato">Contato</a>
          <a class="social" href="#" aria-label="Instagram">IG</a>
          <a class="social" href="#" aria-label="Facebook">FB</a>
          <a class="social" href="#" aria-label="LinkedIn">IN</a>
          <button class="themeBtn" type="button" @click="toggleTheme">
            {{ theme === 'dark' ? 'Modo claro' : 'Modo escuro' }}
          </button>
        </nav>

        <button class="menuBtn" @click="menuOpen = !menuOpen" aria-label="Abrir menu">
          <span></span><span></span><span></span>
        </button>
      </div>

      <div class="mobileNav" v-if="menuOpen">
        <div class="container mobileNav__inner">
          <a href="#inicio" @click="menuOpen=false">Inicio</a>
          <a href="#filosofia" @click="menuOpen=false">Filosofia</a>
          <a href="#atuacao" @click="menuOpen=false">Areas de atuacao</a>
          <a href="#informativos" @click="menuOpen=false">Informativos</a>
          <a href="#contato" @click="menuOpen=false">Contato</a>
          <button class="themeBtn" type="button" @click="toggleTheme">
            {{ theme === 'dark' ? 'Modo claro' : 'Modo escuro' }}
          </button>
        </div>
      </div>
    </header>

    <main id="inicio" class="hero">
      <div class="hero__overlay"></div>
      <div class="container hero__inner">
        <div class="hero__content" style="color: white;">
          <p class="hero__date">8 de fevereiro de 2026</p>
          <h1>
            Orientacao juridica clara, tecnica e informativa para apoiar decisoes com seguranca.
          </h1>
          <a class="btn btn--outline" href="#informativos">Ler mais</a>
          <div class="hero__dots">
            <span class="dot active"></span>
            <span class="dot"></span>
            <span class="dot"></span>
            <span class="dot"></span>
          </div>
        </div>
      </div>
    </main>

    <div class="infoStrip">
      <div class="container infoStrip__inner">
        <strong>Atendimento juridico com discricao e sobriedade | OAB/MS 00.000</strong>
        <div class="offices">
          <span>Presente em atendimento presencial e online</span>
          <select>
            <option>Escritorio</option>
            <option>Campo Grande/MS</option>
            <option>Atendimento online</option>
          </select>
        </div>
      </div>
    </div>

    <section id="filosofia" class="section section--deep">
      <div class="container sectionHead">
        <h2>Filosofia</h2>
        <p class="muted">
          Atuação centrada em etica, tecnica e comunicacao objetiva em todas as etapas do atendimento.
        </p>
      </div>
    </section>

    <section id="atuacao" class="section section--deep pt0">
      <div class="container">
        <div class="sectionHead center">
          <h2>Áreas de Atuação</h2>
          <p class="muted">Confira as frentes juridicas com atendimento personalizado.</p>
        </div>

        <div class="areaGrid">
          <article class="areaCard" v-for="p in practices" :key="p.title">
            <div class="areaCard__icon">⚖</div>
            <h3>{{ p.title }}</h3>
            <p>{{ p.short }}</p>
          </article>
        </div>
      </div>
    </section>

    <section id="informativos" class="section section--light">
      <div class="container">
        <div class="sectionHead center">
          <h2>Destaques</h2>
          <p class="muted">Conteudo juridico de carater informativo.</p>
        </div>

        <div class="newsGrid">
          <article class="newsCard" v-for="n in highlights" :key="n.title">
            <h3>{{ n.title }}</h3>
            <p>{{ n.text }}</p>
            <a href="#contato">Saiba mais</a>
          </article>
        </div>
      </div>
    </section>

    <section id="contato" class="contactHero">
      <div class="contactHero__overlay"></div>
      <div class="container contactHero__inner">
        <div class="contactBox">
          <p class="kicker">Contato</p>
          <h2>Entre em contato</h2>

          <form name="contato" method="POST" data-netlify="true" netlify-honeypot="bot-field" @submit.prevent="onSubmit">
            <input type="hidden" name="form-name" value="contato" />
            <p class="hidden">
              <label>Nao preencher: <input name="bot-field" /></label>
            </p>

            <div class="fieldRow">
              <input v-model.trim="form.nome" name="nome" type="text" placeholder="Nome" required />
              <input v-model.trim="form.email" name="email" type="email" placeholder="E-mail" required />
            </div>
            <div class="fieldRow">
              <input v-model.trim="form.telefone" name="telefone" type="text" placeholder="Telefone" />
              <input v-model.trim="form.cidade" name="cidade" type="text" placeholder="Cidade" />
            </div>
            <textarea v-model.trim="form.mensagem" name="mensagem" rows="7" placeholder="Mensagem" required></textarea>
            <button class="btn btn--outline" type="submit">Enviar</button>
          </form>

          <p class="feedback" v-if="submitMsg">{{ submitMsg }}</p>
          <p class="muted small">*Publicidade de carater informativo, nos termos do Provimento 205/2021 do CFOAB.</p>
        </div>
      </div>
    </section>

    <footer class="footer">
      <div class="container footer__grid">
        <div>
          <h4>Inicio</h4>
          <a href="#inicio">Home</a>
          <a href="#filosofia">Filosofia</a>
          <a href="#contato">Escritorio</a>
        </div>
        <div>
          <h4>Areas de atuacao</h4>
          <a href="#atuacao">Direito Civil</a>
          <a href="#atuacao">Direito de Familia</a>
          <a href="#atuacao">Direito do Trabalho</a>
          <a href="#atuacao">Direito do Consumidor</a>
        </div>
        <div>
          <h4>Informativos</h4>
          <a href="#informativos">Videos</a>
          <a href="#informativos">Destaques</a>
          <a href="#informativos">Leis e noticias</a>
          <a href="#informativos">Juridico</a>
        </div>
        <div>
          <h4>Contato</h4>
          <a href="#contato">Links uteis</a>
          <a :href="whatsHref" target="_blank" rel="noreferrer">WhatsApp</a>
        </div>
        <div>
          <h4>Newsletter</h4>
          <input type="text" placeholder="Nome" />
          <input type="email" placeholder="E-mail" />
          <button class="btn btn--solid">Cadastrar</button>
          <p class="small">Assine e fique informado sobre novidades.</p>
        </div>
      </div>

      <div class="container footer__phones">
        <span>Santa Maria: (55) 3026-3206</span>
        <span>Recife: (81) 3032-4183</span>
        <span>Brasilia: (61) 3226-6937</span>
        <span>Joao Pessoa: (83) 3021-5737</span>
      </div>

      <div class="footer__bottom">
        <div class="container footer__bottomInner">
          <span>© {{ new Date().getFullYear() }} Thays Advocacia - OAB/MS 00.000</span>
          <span>Politica de privacidade</span>
        </div>
      </div>
    </footer>

    <a class="waFloat" :href="whatsHref" target="_blank" rel="noreferrer" aria-label="Abrir WhatsApp">WhatsApp</a>
  </div>
</template>

<script setup>
import { computed, onMounted, ref, watch } from 'vue'

const menuOpen = ref(false)
const theme = ref('dark')

const WHATS_NUMBER = '5567991037665'

const whatsHref = computed(() => {
  const text = encodeURIComponent('Ola, Dra. Thays! Gostaria de agendar uma consulta. Meu caso e sobre: ')
  return `https://wa.me/${WHATS_NUMBER}?text=${text}`
})

const practices = [
  { title: 'Direito Civil', short: 'Contratos, cobrancas, responsabilidade civil e indenizacoes.' },
  { title: 'Direito de Familia', short: 'Divorcio, guarda, pensao e regulamentacao de convivencia.' },
  { title: 'Direito do Trabalho', short: 'Rescisoes, verbas trabalhistas e orientacoes preventivas.' },
  { title: 'Direito do Consumidor', short: 'Cobrancas indevidas, negativacao e vicios de produto.' },
]

const highlights = [
  { title: 'Documentacao em contratos', text: 'Pontos essenciais para reduzir riscos em acordos civis e comerciais.' },
  { title: 'Prazos processuais', text: 'Organizacao de etapas e prazos para acompanhamento do caso.' },
  { title: 'Direitos do consumidor', text: 'Como agir em cobrancas indevidas e falhas na prestacao de servico.' },
  { title: 'Atendimento juridico', text: 'Como funciona a consulta inicial e quais documentos separar.' },
]

const form = ref({
  nome: '',
  email: '',
  telefone: '',
  cidade: '',
  mensagem: '',
})

const submitMsg = ref('')

function toggleTheme() {
  theme.value = theme.value === 'dark' ? 'light' : 'dark'
}

onMounted(() => {
  const savedTheme = localStorage.getItem('site-theme')
  if (savedTheme === 'dark' || savedTheme === 'light') {
    theme.value = savedTheme
    return
  }
  const prefersLight = window.matchMedia('(prefers-color-scheme: light)').matches
  theme.value = prefersLight ? 'light' : 'dark'
})

watch(theme, (value) => {
  localStorage.setItem('site-theme', value)
})

function onSubmit() {
  submitMsg.value = 'Agradecemos sua mensagem.'
}
</script>

<script>
export default {
  components: {
    LogoMark: {
      name: 'LogoMark',
      props: { class: { type: String, default: '' } },
      template: `
        <svg :class="class" viewBox="0 0 64 64" role="img" aria-label="Logo" xmlns="http://www.w3.org/2000/svg">
          <defs>
            <linearGradient id="g" x1="0" y1="0" x2="1" y2="1">
              <stop offset="0" stop-color="#c12767"/>
              <stop offset="1" stop-color="#6d1437"/>
            </linearGradient>
          </defs>
          <rect x="6" y="6" width="52" height="52" rx="14" fill="#12070d" stroke="url(#g)" stroke-width="2"/>
          <path d="M20 22h24v5H35v19h-6V27h-9z" fill="url(#g)"/>
          <circle cx="46.5" cy="23.5" r="2.5" fill="url(#g)"/>
        </svg>
      `,
    },
  },
}
</script>

<style>
html, body, #app {
  margin: 0;
  padding: 0;
  width: 100%;
  min-height: 100%;
}

html {
  scroll-behavior: smooth;
}

body {
  font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif;
  overflow-x: hidden;
}
</style>

<style scoped>
*{box-sizing:border-box}
a{color:inherit; text-decoration:none}
.container{max-width:1160px; margin:0 auto; padding:0 20px}

.app{
  --bg:#13070d;
  --bg-soft:#1a0c14;
  --surface:#201018;
  --surface-2:#281520;
  --text:#fff5fa;
  --muted:#d9becc;
  --line:rgba(255,255,255,.14);
  --accent:#c12767;
  --accent-2:#74173a;
  --accent-soft:rgba(193,39,103,.2);
  background:var(--bg);
  color:var(--text);
  min-height:100vh;
}

.app.theme-light{
  --bg:#fff8fc;
  --bg-soft:#ffeef6;
  --surface:#ffffff;
  --surface-2:#fff5f9;
  --text:#331022;
  --muted:#6d4a5d;
  --line:rgba(51,16,34,.18);
  --accent:#b81f5f;
  --accent-2:#7c1b44;
  --accent-soft:rgba(184,31,95,.12);
}

.topbar{background:var(--surface); border-bottom:1px solid var(--line)}
.topbar__inner{height:44px; display:flex; align-items:center; justify-content:space-between; color:var(--muted); font-size:13px}

.themeBtn{
  border:1px solid var(--line);
  background:transparent;
  color:var(--text);
  border-radius:999px;
  padding:7px 12px;
  font-size:12px;
  font-weight:700;
  cursor:pointer;
}

.header{position:sticky; top:0; z-index:50; background:rgba(19,7,13,.92); border-bottom:1px solid var(--line); backdrop-filter:blur(8px)}
.app.theme-light .header{background:rgba(255,248,252,.9)}
.header__inner{height:84px; display:flex; align-items:center; justify-content:space-between; gap:16px}

.brand{display:flex; align-items:center; gap:12px}
.logo{width:44px; height:44px}
.brand__name{font-size:28px; line-height:1; font-weight:800}
.brand__sub{font-size:12px; color:var(--accent); font-weight:700; letter-spacing:.06em; text-transform:uppercase}

.nav{display:flex; align-items:center; gap:22px}
.nav a{font-size:14px; font-weight:700; text-transform:uppercase; letter-spacing:.03em}
.nav a:hover{color:var(--accent)}
.nav .social{
  width:26px; height:26px; border-radius:50%;
  border:1px solid var(--line);
  display:inline-flex; align-items:center; justify-content:center;
  font-size:11px;
}

.menuBtn{display:none; background:transparent; border:0; padding:8px; cursor:pointer}
.menuBtn span{display:block; width:24px; height:2px; background:var(--text); margin:5px 0}

.mobileNav{border-top:1px solid var(--line); background:var(--surface)}
.mobileNav__inner{padding:16px 20px; display:flex; flex-direction:column; gap:12px}
.mobileNav__inner a{font-weight:700}
.mobileNav__inner .themeBtn{width:fit-content}

.hero{
  min-height:72vh;
  position:relative;
  background-image:url('https://images.unsplash.com/photo-1450101499163-c8848c66ca85?auto=format&fit=crop&w=1600&q=80');
  background-size:cover;
  background-position:center;
}
.hero__overlay{position:absolute; inset:0; background:linear-gradient(90deg, rgba(10,4,7,.78), rgba(10,4,7,.45))}
.hero__inner{position:relative; z-index:2; min-height:72vh; display:flex; align-items:center}
.hero__content{max-width:760px}
.hero__date{font-size:24px; font-weight:800; margin:0 0 14px}
h1{font-size:56px; line-height:1.08; margin:0 0 20px}

.hero__dots{display:flex; gap:8px; margin-top:20px}
.hero__dots .dot{
  width:12px; height:12px; border-radius:999px;
  border:1px solid rgba(255,255,255,.8);
  background:transparent;
}
.hero__dots .dot.active{background:var(--accent); border-color:var(--accent)}

.infoStrip{background:linear-gradient(90deg, var(--accent), var(--accent-2))}
.infoStrip__inner{
  min-height:54px;
  display:flex;
  align-items:center;
  justify-content:space-between;
  gap:16px;
  flex-wrap:wrap;
  color:#fff;
  font-size:15px;
}
.offices{display:flex; align-items:center; gap:12px}
.offices select{
  height:38px;
  border:1px solid rgba(255,255,255,.55);
  background:rgba(255,255,255,.12);
  color:#fff;
  padding:0 10px;
}
.app.theme-light .offices select{color:#2d0e1f; background:#fff}

.section{padding:72px 0}
.section--deep{background:linear-gradient(90deg, #0f0612, #1a0d15)}
.app.theme-light .section--deep{background:linear-gradient(90deg, #fff7fb, #ffeef6)}
.section--light{background:var(--bg-soft)}
.pt0{padding-top:0}

.sectionHead h2{font-size:56px; margin:0 0 10px}
.sectionHead .muted{margin:0; color:var(--muted); font-size:21px}
.center{text-align:center}

.areaGrid{
  margin-top:28px;
  display:grid;
  grid-template-columns:repeat(4,1fr);
  gap:16px;
}
.areaCard{
  background:var(--surface-2);
  border:1px solid var(--line);
  padding:26px;
  min-height:220px;
}
.areaCard__icon{font-size:28px; color:var(--accent)}
.areaCard h3{font-size:32px; margin:10px 0 8px}
.areaCard p{margin:0; line-height:1.6; color:var(--muted)}

.newsGrid{
  margin-top:28px;
  display:grid;
  grid-template-columns:repeat(4,1fr);
  gap:16px;
}
.newsCard{
  background:var(--surface);
  border:1px solid var(--line);
  padding:22px;
  min-height:220px;
  display:flex;
  flex-direction:column;
  gap:10px;
}
.newsCard h3{font-size:28px; margin:0}
.newsCard p{margin:0; color:var(--muted); line-height:1.5}
.newsCard a{margin-top:auto; color:var(--accent); font-weight:700}

.contactHero{
  position:relative;
  background-image:url('https://images.unsplash.com/photo-1589829545856-d10d557cf95f?auto=format&fit=crop&w=1600&q=80');
  background-size:cover;
  background-position:center;
}
.contactHero__overlay{position:absolute; inset:0; background:rgba(10,4,7,.7)}
.contactHero__inner{position:relative; z-index:2; padding:84px 20px}
.contactBox{max-width:640px}
.kicker{margin:0 0 10px; font-size:20px; font-weight:700}

.contactBox h2{font-size:58px; margin:0 0 20px}
.fieldRow{display:grid; grid-template-columns:1fr 1fr; gap:12px; margin-bottom:12px}
input, textarea{
  width:100%;
  border:1px solid rgba(255,255,255,.55);
  background:rgba(255,255,255,.93);
  color:#1f0a14;
  padding:13px 14px;
  font-size:16px;
}
textarea{resize:vertical; min-height:180px; margin-bottom:14px}

.btn{
  display:inline-flex; align-items:center; justify-content:center;
  min-width:150px; height:50px;
  border-radius:2px;
  font-size:24px;
  font-weight:700;
  text-transform:uppercase;
  letter-spacing:.06em;
  cursor:pointer;
}
.btn--outline{
  background:transparent;
  color:#fff;
  border:1px solid rgba(255,255,255,.72);
}
.btn--outline:hover{border-color:var(--accent)}
.btn--solid{
  border:0;
  color:#fff;
  background:linear-gradient(90deg, var(--accent), var(--accent-2));
}

.feedback{
  margin-top:14px;
  border:2px solid var(--accent);
  background:#fff;
  color:#2d0e1f;
  padding:8px 12px;
  max-width:520px;
  font-size:15px;
}
.muted{color:var(--muted)}
.small{font-size:13px}
.hidden{display:none}

.footer{background:linear-gradient(90deg, #0f0612, #13070d)}
.app.theme-light .footer{background:linear-gradient(90deg, #fff7fb, #ffeef6)}
.footer__grid{
  display:grid;
  grid-template-columns:1.2fr 1.2fr 1.2fr 1fr 1.4fr;
  gap:24px;
  padding:54px 20px 24px;
}
.footer__grid h4{
  margin:0 0 14px;
  font-size:20px;
  text-transform:uppercase;
}
.footer__grid a{
  display:block;
  margin-bottom:10px;
  color:var(--muted);
}
.footer__grid a:hover{color:var(--accent)}
.footer__grid input{
  margin-bottom:8px;
  height:44px;
  border:1px solid var(--line);
  background:var(--surface);
  color:var(--text);
}
.footer__grid .btn{height:46px; min-width:0; width:130px; font-size:16px}
.footer__grid p{color:var(--muted)}

.footer__phones{
  border-top:1px solid var(--line);
  border-bottom:1px solid var(--line);
  padding:16px 20px;
  display:flex;
  gap:20px;
  justify-content:space-between;
  flex-wrap:wrap;
  color:var(--muted);
  font-size:13px;
  text-transform:uppercase;
}
.footer__bottom{background:linear-gradient(90deg, var(--accent), var(--accent-2))}
.footer__bottomInner{
  min-height:54px;
  display:flex;
  align-items:center;
  justify-content:space-between;
  gap:12px;
  color:#fff;
  font-size:14px;
}

.waFloat{
  position:fixed;
  right:18px;
  bottom:18px;
  z-index:70;
  padding:12px 15px;
  border-radius:999px;
  color:#fff;
  font-weight:800;
  background:linear-gradient(90deg, var(--accent), var(--accent-2));
  box-shadow:0 12px 24px rgba(0,0,0,.32);
}

@media (max-width: 1200px){
  .areaGrid,.newsGrid{grid-template-columns:repeat(2,1fr)}
  .footer__grid{grid-template-columns:repeat(3,1fr)}
}
@media (max-width: 920px){
  .nav{display:none}
  .menuBtn{display:block}
  h1{font-size:42px}
  .sectionHead h2{font-size:44px}
  .contactBox h2{font-size:42px}
  .fieldRow{grid-template-columns:1fr}
  .footer__grid{grid-template-columns:repeat(2,1fr)}
}
@media (max-width: 640px){
  .hero,.hero__inner{min-height:64vh}
  h1{font-size:34px}
  .sectionHead h2{font-size:36px}
  .areaGrid,.newsGrid,.footer__grid{grid-template-columns:1fr}
  .footer__bottomInner{flex-direction:column; justify-content:center}
  .topbar__inner{height:auto; padding:8px 0}
}
</style>

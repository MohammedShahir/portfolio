<template>
  <section id="contact" class="section">
    <div class="orb" style="width:600px;height:600px;top:50%;left:50%;transform:translate(-50%,-50%);background:radial-gradient(circle,rgba(108,99,255,0.08),transparent 70%);"></div>
    <div class="container">
      <div class="section-header reveal" style="text-align:center;">
        <div class="section-tag" style="margin:0 auto 20px;"><span>✦</span> {{ isRtl ? 'ابقَ على تواصل' : 'Stay Connected' }}</div>
        <h2 class="section-title">{{ isRtl ? 'تواصل معي' : "Let's Work Together" }}</h2>
        <p class="section-sub" style="margin:0 auto;">{{ isRtl ? 'أنا دائماً مستعد للفرص الجديدة والتعاون. تواصل معي!' : "I'm always open to new opportunities and collaborations. Reach out!" }}</p>
      </div>

      <div class="contact-layout">
        <!-- Contact Cards -->
        <div class="contact-cards reveal">
          <a :href="`mailto:${d.email}`" class="contact-card card">
            <div class="cc-icon" style="background:rgba(108,99,255,0.1);color:var(--accent-1);">📧</div>
            <div>
              <div class="cc-label">{{ isRtl ? 'البريد الإلكتروني' : 'Email' }}</div>
              <div class="cc-value">{{ d.email }}</div>
            </div>
            <svg class="cc-arrow" width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M5 12h14M12 5l7 7-7 7"/></svg>
          </a>

          <a :href="`tel:${d.phone}`" class="contact-card card">
            <div class="cc-icon" style="background:rgba(67,233,123,0.1);color:#43e97b;">📱</div>
            <div>
              <div class="cc-label">{{ isRtl ? 'الهاتف' : 'Phone' }}</div>
              <div class="cc-value">{{ d.phone }}</div>
            </div>
            <svg class="cc-arrow" width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M5 12h14M12 5l7 7-7 7"/></svg>
          </a>

          <a :href="d.github" target="_blank" class="contact-card card">
            <div class="cc-icon" style="background:rgba(255,255,255,0.06);color:var(--text-primary);">
              <svg width="20" height="20" viewBox="0 0 24 24" fill="currentColor"><path d="M12 0C5.37 0 0 5.37 0 12c0 5.31 3.435 9.795 8.205 11.385.6.105.825-.255.825-.57 0-.285-.015-1.23-.015-2.235-3.015.555-3.795-.735-4.035-1.41-.135-.345-.72-1.41-1.23-1.695-.42-.225-1.02-.78-.015-.795.945-.015 1.62.87 1.845 1.23 1.08 1.815 2.805 1.305 3.495.99.105-.78.42-1.305.765-1.605-2.67-.3-5.46-1.335-5.46-5.925 0-1.305.465-2.385 1.23-3.225-.12-.3-.54-1.53.12-3.18 0 0 1.005-.315 3.3 1.23.96-.27 1.98-.405 3-.405s2.04.135 3 .405c2.295-1.56 3.3-1.23 3.3-1.23.66 1.65.24 2.88.12 3.18.765.84 1.23 1.905 1.23 3.225 0 4.605-2.805 5.625-5.475 5.925.435.375.81 1.095.81 2.22 0 1.605-.015 2.895-.015 3.3 0 .315.225.69.825.57A12.02 12.02 0 0024 12c0-6.63-5.37-12-12-12z"/></svg>
            </div>
            <div>
              <div class="cc-label">GitHub</div>
              <div class="cc-value">MohammedShahir</div>
            </div>
            <svg class="cc-arrow" width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M5 12h14M12 5l7 7-7 7"/></svg>
          </a>

          <div class="contact-card card no-link">
            <div class="cc-icon" style="background:rgba(255,101,132,0.1);color:var(--accent-2);">📍</div>
            <div>
              <div class="cc-label">{{ isRtl ? 'الموقع' : 'Location' }}</div>
              <div class="cc-value">{{ d.location }}</div>
            </div>
          </div>
        </div>

        <!-- Contact Form -->
        <form class="contact-form card" @submit.prevent="handleSubmit">
          <h3 class="form-title">{{ isRtl ? 'أرسل رسالة' : 'Send a Message' }}</h3>

          <!-- Web3Forms setup notice -->
          <div v-if="!web3formsConfigured" class="setup-notice">
            <span>⚙️</span>
            <div>
              <strong>{{ isRtl ? 'خطوة واحدة للتفعيل:' : 'One step to activate:' }}</strong>
              {{ isRtl ? 'اذهب إلى' : 'Go to' }}
              <a href="https://web3forms.com" target="_blank" style="color:var(--accent-1)">web3forms.com</a>
              {{ isRtl ? 'وأدخل إيميلك للحصول على المفتاح' : 'and enter your email to get the Access Key' }}
            </div>
          </div>

          <div class="form-row">
            <div class="form-group">
              <label>{{ isRtl ? 'الاسم' : 'Name' }}</label>
              <input v-model="form.name" type="text" :placeholder="isRtl ? 'اسمك الكامل' : 'Your full name'" required />
            </div>
            <div class="form-group">
              <label>{{ isRtl ? 'البريد الإلكتروني' : 'Email' }}</label>
              <input v-model="form.email" type="email" :placeholder="isRtl ? 'بريدك الإلكتروني' : 'your@email.com'" required />
            </div>
          </div>

          <div class="form-group">
            <label>{{ isRtl ? 'الموضوع' : 'Subject' }}</label>
            <input v-model="form.subject" type="text" :placeholder="isRtl ? 'موضوع الرسالة' : 'What is this about?'" required />
          </div>

          <div class="form-group">
            <label>{{ isRtl ? 'الرسالة' : 'Message' }}</label>
            <textarea v-model="form.message" rows="5" :placeholder="isRtl ? 'اكتب رسالتك هنا...' : 'Tell me about your project or idea...'" required></textarea>
          </div>

          <button type="submit" class="btn btn-primary submit-btn" :class="{ sent: status === 'sent', error: status === 'error' }" :disabled="loading">
            <span v-if="loading" class="spinner"></span>
            <span v-else-if="status === 'sent'">
              ✅ {{ isRtl ? 'تم إرسال الرسالة!' : 'Message Sent!' }}
            </span>
            <span v-else-if="status === 'error'">
              ❌ {{ isRtl ? 'فشل الإرسال، حاول مجدداً' : 'Failed, try again' }}
            </span>
            <span v-else>
              {{ isRtl ? 'إرسال الرسالة' : 'Send Message' }}
              <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M22 2L11 13M22 2l-7 20-4-9-9-4 20-7z"/></svg>
            </span>
          </button>
        </form>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref, computed } from 'vue'
import { WEB3FORMS_ACCESS_KEY } from '../config/emailjs.js'

defineProps({ d: Object, isRtl: Boolean })

const form = ref({ name: '', email: '', subject: '', message: '' })
const loading = ref(false)
const status = ref('') // '', 'sent', 'error'

const web3formsConfigured = computed(() => WEB3FORMS_ACCESS_KEY !== 'YOUR_ACCESS_KEY')

async function handleSubmit() {
  if (loading.value) return
  loading.value = true
  status.value = ''

  try {
    if (web3formsConfigured.value) {
      // ── Web3Forms: إرسال مباشر بدون npm ──
      const res = await fetch('https://api.web3forms.com/submit', {
        method: 'POST',
        headers: { 'Content-Type': 'application/json', Accept: 'application/json' },
        body: JSON.stringify({
          access_key: WEB3FORMS_ACCESS_KEY,
          name: form.value.name,
          email: form.value.email,
          subject: form.value.subject,
          message: form.value.message,
          replyto: form.value.email,
        }),
      })
      const data = await res.json()
      if (!data.success) throw new Error(data.message || 'Failed')
    } else {
      // Fallback: يفتح Outlook بالرسالة جاهزة
      const { name, email, subject, message } = form.value
      const body = `From: ${name} (${email})\n\n${message}`
      window.open(`mailto:mohammed.shaheer.shawqi@outlook.com?subject=${encodeURIComponent(subject)}&body=${encodeURIComponent(body)}`)
    }

    status.value = 'sent'
    form.value = { name: '', email: '', subject: '', message: '' }
    setTimeout(() => { status.value = '' }, 5000)
  } catch (e) {
    console.error('Web3Forms error:', e)
    status.value = 'error'
    setTimeout(() => { status.value = '' }, 4000)
  } finally {
    loading.value = false
  }
}
</script>

<style scoped>
.section-header { margin-bottom: 60px; }

.contact-layout {
  display: grid;
  grid-template-columns: 1fr 1.3fr;
  gap: 32px;
  align-items: start;
}

.contact-cards { display: flex; flex-direction: column; gap: 16px; }

.contact-card {
  display: flex;
  align-items: center;
  gap: 16px;
  text-decoration: none;
  color: inherit;
  transition: var(--transition);
}
.contact-card:hover { border-color: var(--border-hover); transform: translateX(4px); }
.contact-card.no-link { cursor: default; }
.contact-card.no-link:hover { transform: none; }

.cc-icon {
  width: 46px; height: 46px;
  border-radius: 12px;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 1.2rem;
  flex-shrink: 0;
}
.cc-label { font-size: 0.75rem; color: var(--text-muted); text-transform: uppercase; letter-spacing: 0.1em; margin-bottom: 2px; }
.cc-value { font-size: 0.9rem; font-weight: 600; color: var(--text-primary); }
.cc-arrow { margin-left: auto; color: var(--text-muted); transition: transform 0.3s; flex-shrink: 0; }
.contact-card:hover .cc-arrow { transform: translateX(4px); color: var(--accent-1); }

/* ─── Setup Notice ─── */
.setup-notice {
  display: flex;
  gap: 10px;
  padding: 12px 16px;
  border-radius: var(--radius-sm);
  background: rgba(255,193,7,0.08);
  border: 1px solid rgba(255,193,7,0.2);
  font-size: 0.83rem;
  color: var(--text-secondary);
  line-height: 1.6;
}
.setup-notice code {
  font-family: monospace;
  background: rgba(255,255,255,0.08);
  padding: 1px 6px;
  border-radius: 4px;
  font-size: 0.8rem;
  color: var(--accent-1);
}

/* ─── Form ─── */
.contact-form {
  display: flex;
  flex-direction: column;
  gap: 20px;
  position: relative;
  z-index: 1;
  animation: fadeSlideUp 0.6s ease both;
}
@keyframes fadeSlideUp {
  from { opacity: 0; transform: translateY(30px); }
  to   { opacity: 1; transform: translateY(0); }
}
.form-title { font-size: 1.2rem; font-weight: 700; color: var(--text-primary); }

.form-row { display: grid; grid-template-columns: 1fr 1fr; gap: 16px; }
.form-group { display: flex; flex-direction: column; gap: 8px; }

label { font-size: 0.82rem; font-weight: 600; color: var(--text-secondary); letter-spacing: 0.05em; }

input, textarea {
  background: rgba(255,255,255,0.03);
  border: 1px solid var(--border);
  border-radius: var(--radius-sm);
  padding: 12px 16px;
  color: var(--text-primary);
  font-size: 0.93rem;
  font-family: inherit;
  transition: border-color 0.3s, background 0.3s, box-shadow 0.3s;
  outline: none;
  resize: vertical;
  position: relative;
  z-index: 2;
  pointer-events: auto;
  -webkit-appearance: none;
}
input:focus, textarea:focus {
  border-color: var(--accent-1);
  background: rgba(108,99,255,0.04);
  box-shadow: 0 0 0 3px rgba(108,99,255,0.1);
}
input::placeholder, textarea::placeholder { color: var(--text-muted); }

.submit-btn { width: 100%; justify-content: center; position: relative; }
.submit-btn:disabled { opacity: 0.7; cursor: not-allowed; transform: none !important; }
.submit-btn.sent { background: linear-gradient(135deg, #43e97b, #38f9d7); }
.submit-btn.error { background: linear-gradient(135deg, #ff4757, #ff6b81); }

/* Spinner */
.spinner {
  width: 18px; height: 18px;
  border: 2px solid rgba(255,255,255,0.3);
  border-top-color: #fff;
  border-radius: 50%;
  animation: spin 0.7s linear infinite;
  display: inline-block;
}
@keyframes spin { to { transform: rotate(360deg); } }

.rtl .contact-card:hover { transform: translateX(-4px); }
.rtl .cc-arrow { margin-left: 0; margin-right: auto; }
.rtl .contact-card:hover .cc-arrow { transform: translateX(-4px); }

@media (max-width: 900px) {
  .contact-layout { grid-template-columns: 1fr; }
  .form-row { grid-template-columns: 1fr; }
}
</style>

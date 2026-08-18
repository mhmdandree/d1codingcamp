# Implementation Plan: Personal Portfolio Web

## Overview

Implementasi single-page portfolio menggunakan HTML, CSS, dan JavaScript vanilla — tanpa build tool atau package manager. File produksi terdiri dari `index.html`, `style.css`, dan `script.js`. Vitest + fast-check diinstal sebagai dev dependency khusus untuk pengujian.

---

## Tasks

- [-] 1. Setup project structure dan CSS foundation
  - Buat file `index.html` dengan boilerplate HTML5 lengkap: `<!DOCTYPE html>`, `<meta charset>`, `<meta name="viewport" content="width=device-width, initial-scale=1">`, `<title>`, link ke `style.css`, link ke `script.js`
  - Buat file `style.css` dan definisikan semua CSS custom properties di selector `:root` sesuai design: `--bg-primary`, `--bg-secondary`, `--bg-card`, `--text-primary`, `--text-secondary`, `--neon-accent`, `--neon-accent-dim`, `--border-color`, `--font-heading`, `--font-body`, `--font-mono`, semua spacing dan radius variables
  - Tambahkan CDN links di `<head>`: Google Fonts (Space Grotesk, Inter, JetBrains Mono) dan Font Awesome untuk social icons
  - Tambahkan CSS reset/base styles: `box-sizing: border-box`, `margin: 0`, `padding: 0`, `font-family: var(--font-body)`, `background: var(--bg-primary)`, `color: var(--text-primary)`
  - Buat file `script.js` kosong dan file `package.json` dengan `devDependencies` untuk vitest dan fast-check; buat `vitest.config.js` dengan environment jsdom
  - _Requirements: 7.5, 8.3, 8.4, 8.5, 9.1_

- [ ] 2. Implementasi Navigation component
  - [~] 2.1 Buat markup HTML untuk navigation di `index.html`
    - Tulis elemen `<header>` dengan `<nav>` berisi `.nav-brand`, `.nav-links` (ul > li > a untuk 5 section: Hero, Experience, Projects, Certifications, Contact), dan `.nav-hamburger` (button dengan `aria-label="Open navigation menu"`)
    - Tambahkan atribut `id` pada setiap `<section>`: `id="hero"`, `id="experience"`, `id="projects"`, `id="certifications"`, `id="contact"`
    - Tambahkan `<main>` yang membungkus semua section, gunakan `<header>`, `<nav>`, `<section>`, `<footer>` sebagai semantic HTML5 elements
    - _Requirements: 1.1, 1.2, 1.3, 1.6, 9.3, 9.4_

  - [~] 2.2 Buat CSS untuk navigation
    - Style `header`/`.nav-container` sebagai sticky (`position: sticky; top: 0; z-index: 100`)
    - Style nav links dengan hover state menggunakan `var(--neon-accent)` dan transition
    - Tambahkan style untuk class `.active` pada nav link (warna `var(--neon-accent)`)
    - Style `.nav-hamburger` sebagai tersembunyi di desktop (`display: none`) dan visible di mobile (`< 768px`)
    - Style `.nav-mobile-overlay` sebagai fullscreen overlay tersembunyi by default, visible saat class `.open` ditambahkan
    - Tambahkan CSS `@media (max-width: 767px)` untuk collapse nav ke hamburger
    - _Requirements: 1.2, 1.3, 1.7, 1.8, 7.2_

  - [~] 2.3 Implementasi JavaScript navigation di `script.js`
    - Tulis fungsi `smoothScrollTo(sectionId)` menggunakan `document.getElementById(sectionId).scrollIntoView({ behavior: 'smooth' })`
    - Tulis fungsi `initScrollSpy(sectionIds)` menggunakan `IntersectionObserver` — saat section masuk viewport, tambahkan class `.active` ke nav link yang sesuai dan hapus dari yang lain; guard dengan `if ('IntersectionObserver' in window)`
    - Tulis fungsi `initHamburgerMenu()` — toggle class `.open` pada overlay saat button hamburger diklik; tutup overlay saat nav link mobile diklik
    - Panggil ketiga fungsi ini di akhir `script.js` (atau dalam `DOMContentLoaded` listener)
    - _Requirements: 1.4, 1.5, 1.7, 1.8_

  - [ ]* 2.4 Tulis unit tests untuk navigation
    - Test `nav-links.test.js`: verifikasi 5 nav link ada di DOM dan setiap `href` cocok dengan section ID (`#hero`, `#experience`, `#projects`, `#certifications`, `#contact`)
    - Test `hamburger.test.js`: simulasi klik hamburger button, verifikasi class `.open` ditambahkan ke overlay; klik kedua menghapus class `.open`
    - Test `section-order.test.js`: verifikasi urutan section di DOM sesuai spec (hero → experience → projects → certifications → contact)
    - _Requirements: 1.3, 1.7, 1.8_

  - [ ]* 2.5 Tulis property test untuk active nav link (Property 1)
    - **Property 1: Active Navigation Link Matches Current Section**
    - **Validates: Requirements 1.5**
    - Implementasikan test sesuai contoh di design.md menggunakan `fc.constantFrom` untuk section IDs dan `fc.integer` untuk scroll position; mock section bounds sehingga scroll position jatuh di dalam section tertentu

- [ ] 3. Implementasi Hero Section
  - [~] 3.1 Buat markup HTML untuk Hero Section
    - Tulis `<section id="hero">` berisi: `<img class="hero-photo">` dengan `alt` deskriptif dan `onerror` fallback, `<h1 class="hero-name">` nama engineer, `<p class="hero-title">` subtitle "Software Engineer — Cloud & Fintech", `<p class="hero-bio">` bio 3 kalimat, dan dua CTA buttons: `<a class="btn-primary" href="#projects">View My Work</a>` dan `<a class="btn-secondary" href="#contact">Contact Me</a>`
    - Pastikan foto profil menggunakan `onerror="this.src='fallback-avatar.svg'"` dan sertakan `fallback-avatar.svg` sebagai inline SVG atau file terpisah
    - _Requirements: 2.1, 2.2, 2.3, 2.4, 2.5, 2.6, 9.2_

  - [~] 3.2 Buat CSS untuk Hero Section
    - Style `.hero-photo` dengan border-radius untuk tampilan circular atau rounded-square
    - Style `.btn-primary` dengan `border: 2px solid var(--neon-accent)` atau `background: var(--neon-accent)` untuk neon accent
    - Style `.btn-secondary` dengan styling berbeda dari primary
    - Tulis CSS keyframes `fadeInUp` atau `slideUp` dan terapkan pada `.hero-name` dan `.hero-title` dengan `animation-duration` antara 500ms–700ms
    - Tambahkan hover styles untuk kedua buttons dengan `var(--transition-normal)`
    - _Requirements: 2.4, 2.7, 2.8, 7.1, 7.2_

  - [ ]* 3.3 Tulis unit test untuk Hero Section
    - Test `hero-cta.test.js`: verifikasi button "View My Work" memiliki `href="#projects"` dan button "Contact Me" memiliki `href="#contact"`
    - Verifikasi `.hero-photo` memiliki atribut `alt` yang tidak kosong
    - _Requirements: 2.5, 2.6, 9.2_

- [~] 4. Checkpoint — Verifikasi struktur dasar dan navigasi
  - Ensure all tests pass, ask the user if questions arise.

- [ ] 5. Implementasi Experience Section
  - [~] 5.1 Definisikan data experience dan fungsi render di `script.js`
    - Definisikan array `const experiences` berisi minimal 2 `ExperienceEntry` objects sesuai interface di design.md (id, company, title, startDate "YYYY-MM", endDate nullable, responsibilities array)
    - Tulis fungsi `sortExperienceEntries(entries)` yang mengurutkan array berdasarkan `startDate` secara descending (newest first) — gunakan string comparison `"YYYY-MM"` yang konsisten
    - Tulis fungsi `formatPeriod(startDate, endDate)` yang mengkonversi "2022-01" ke "Jan 2022" dan null ke "Present"
    - Tulis fungsi `renderExperienceEntry(entry)` yang mengembalikan string HTML untuk satu entry dengan semua required fields
    - Panggil `renderExperienceSection()` yang merender semua entries ke `.experience-timeline`
    - _Requirements: 3.2, 3.3, 3.4_

  - [~] 5.2 Buat markup HTML placeholder dan CSS untuk Experience Section
    - Tulis `<section id="experience">` dengan `<h2>Experience</h2>` dan `<div class="experience-timeline"></div>` sebagai container
    - Style `.experience-timeline` sebagai vertical timeline layout
    - Style `.experience-entry` dengan padding, border-left transparent by default
    - Tambahkan `@media (pointer: fine)` hover rule: `.experience-entry:hover { border-left: 3px solid var(--neon-accent); }`
    - Pastikan layout readable di mobile dan desktop
    - _Requirements: 3.1, 3.5, 3.6_

  - [ ]* 5.3 Tulis property tests untuk Experience Section (Property 2 dan 3)
    - **Property 2: Experience Entries Are Reverse Chronological**
    - **Validates: Requirements 3.2**
    - **Property 3: Experience Entry Renders All Required Fields**
    - **Validates: Requirements 3.3**
    - Implementasikan kedua tests menggunakan `fc.array` dan `fc.record` sesuai contoh di design.md
    - _Requirements: 3.2, 3.3_

  - [ ]* 5.4 Tulis unit tests untuk Experience Section
    - Test `experience-count.test.js`: query DOM setelah render dan verifikasi minimal 2 `.experience-entry` elements ada
    - Verifikasi setiap entry menampilkan company name, job title, dan employment period
    - _Requirements: 3.4_

- [ ] 6. Implementasi Projects Section
  - [~] 6.1 Definisikan data projects dan fungsi render di `script.js`
    - Definisikan array `const projects` berisi minimal 3 `ProjectItem` objects sesuai interface (id, name, description ≤2 kalimat, techTags array, githubUrl)
    - Tulis fungsi `renderProjectCard(project)` yang mengembalikan string HTML untuk satu card dengan: `.card-name`, `.card-description`, `.card-tags` (span.tag per tag), dan `<a class="card-github" href="${githubUrl}" target="_blank" rel="noopener noreferrer">GitHub</a>`
    - Panggil `renderProjectsSection()` yang merender semua cards ke `.projects-grid`
    - _Requirements: 4.1, 4.2, 4.3, 4.4_

  - [~] 6.2 Buat markup HTML placeholder dan CSS untuk Projects Section
    - Tulis `<section id="projects">` dengan `<h2>Projects</h2>` dan `<div class="projects-grid"></div>`
    - Style `.projects-grid` menggunakan CSS Grid: `grid-template-columns: repeat(2, 1fr)` untuk `≥768px` dan `grid-template-columns: 1fr` untuk `<768px`
    - Style `.project-card` dengan `background: var(--bg-card)`, `border-radius: var(--radius-card)`, dan hover effect: `box-shadow: 0 0 20px var(--neon-accent)` dengan `@media (pointer: fine)`
    - Style `.card-tags span.tag` dengan warna `var(--neon-accent)` atau border neon untuk visual distinction
    - _Requirements: 4.2, 4.5, 4.6, 4.7_

  - [ ]* 6.3 Tulis property test untuk Project Card (Property 4)
    - **Property 4: Project Card Renders All Required Fields**
    - **Validates: Requirements 4.3, 4.4**
    - Implementasikan test menggunakan `fc.record` dengan `fc.webUrl()` untuk githubUrl sesuai contoh di design.md
    - _Requirements: 4.3, 4.4_

  - [ ]* 6.4 Tulis unit test untuk Projects Section
    - Test `projects-count.test.js`: verifikasi minimal 3 `.project-card` elements ada di DOM setelah render
    - Verifikasi setiap card memiliki elemen anchor dengan `target="_blank"` untuk GitHub link
    - _Requirements: 4.2, 4.4_

- [ ] 7. Implementasi Certifications Section
  - [~] 7.1 Definisikan data certifications dan fungsi render di `script.js`
    - Definisikan array `const certifications` berisi minimal 2 `CertificationItem` objects (id, name, issuer, year, verifyUrl opsional)
    - Tulis fungsi `renderCertificationBadge(cert)` yang mengembalikan string HTML untuk satu badge dengan `.badge-name`, `.badge-issuer`, `.badge-year`, dan anchor `.badge-verify` yang hanya dirender jika `cert.verifyUrl` ada dan tidak kosong (dengan `target="_blank"`)
    - Panggil `renderCertificationsSection()` yang merender semua badges ke `.certifications-grid`
    - _Requirements: 5.1, 5.2, 5.3, 5.4_

  - [~] 7.2 Buat markup HTML placeholder dan CSS untuk Certifications Section
    - Tulis `<section id="certifications">` dengan `<h2>Certifications</h2>` dan `<div class="certifications-grid"></div>`
    - Style `.certifications-grid` menggunakan CSS Flexbox dengan `flex-wrap: wrap` agar wraps di viewport kecil
    - Style `.certification-badge` dengan `background: var(--bg-card)`, `border-radius: var(--radius-badge)`
    - Tambahkan hover effect dengan `@media (pointer: fine)`: `transform: scale(1.03)` dan `box-shadow: 0 0 12px var(--neon-accent)`
    - _Requirements: 5.5, 5.6_

  - [ ]* 7.3 Tulis property tests untuk Certifications Section (Property 5 dan 6)
    - **Property 5: Certification Badge Renders All Required Fields**
    - **Validates: Requirements 5.3**
    - **Property 6: Certification Verify Link Is Conditional**
    - **Validates: Requirements 5.4**
    - Implementasikan kedua tests menggunakan `fc.record` dan `fc.option(fc.webUrl(), { nil: undefined })` sesuai contoh di design.md
    - _Requirements: 5.3, 5.4_

  - [ ]* 7.4 Tulis unit test untuk Certifications Section
    - Test `certifications-count.test.js`: verifikasi minimal 2 `.certification-badge` elements ada di DOM setelah render
    - _Requirements: 5.2_

- [~] 8. Checkpoint — Verifikasi semua content sections
  - Ensure all tests pass, ask the user if questions arise.

- [ ] 9. Implementasi Contact Section dan Form Validation
  - [~] 9.1 Buat markup HTML untuk Contact Section
    - Tulis `<section id="contact">` dengan `<h2>Contact</h2>`
    - Buat `.contact-form` dengan tiga `.form-group`: masing-masing berisi `<label>`, `<input>` atau `<textarea>` dengan atribut `required`, dan `<span class="error-message">` (tersembunyi by default)
    - Input name: `type="text"`, `id="name"`, `required`; input email: `type="email"`, `id="email"`, `required`; textarea: `id="message"`, `required`
    - Tambahkan `<button type="submit">Send Message</button>` dan `<div class="success-message">` (tersembunyi by default)
    - Buat `.social-links` dengan tiga anchor elements: LinkedIn, X (Twitter), DEV Community — masing-masing dengan `target="_blank"`, `rel="noopener noreferrer"`, dan `aria-label` yang deskriptif
    - Gunakan Font Awesome icon classes untuk social icons (fa-linkedin, fa-x-twitter, fa-dev)
    - _Requirements: 6.1, 6.2, 6.3, 6.7, 6.8, 9.3_

  - [~] 9.2 Implementasi form validation di `script.js`
    - Tulis fungsi `isValidEmail(value)` menggunakan regex pattern untuk validasi format email
    - Tulis fungsi `validateForm(data)` yang mengembalikan `{ valid: boolean, errors: FieldError[] }` — cek field kosong dan format email; jangan return error untuk field yang terisi benar
    - Tulis fungsi `showFieldError(fieldId, message)` yang menambahkan class `.error-active` ke `.form-group` parent dan mengisi teks `.error-message`
    - Tulis fungsi `showSuccessMessage()` yang menyembunyikan form dan menampilkan `.success-message`
    - Tulis fungsi `clearErrors()` yang menghapus semua `.error-active` classes dan mengosongkan error messages
    - Attach event listener `submit` ke form; panggil `clearErrors()`, lalu `validateForm()`, tampilkan errors atau sukses sesuai hasil — **jangan submit ke server** (`event.preventDefault()`)
    - _Requirements: 6.3, 6.4, 6.5, 6.6_

  - [~] 9.3 Buat CSS untuk Contact Section
    - Style `.contact-form` dengan layout yang bersih, input/textarea full-width dengan `background: var(--bg-secondary)`, `border: 1px solid var(--border-color)`, `color: var(--text-primary)`
    - Style `.error-message` sebagai `display: none` by default; style `.form-group.error-active .error-message` sebagai `display: block` dengan warna merah/orange
    - Style `.success-message` sebagai tersembunyi by default, tampil dengan warna `var(--neon-accent)` saat class `.visible` ditambahkan
    - Style `.social-links` dengan flex layout dan gap; social icon anchor dengan hover state menggunakan `@media (pointer: fine)` dan `color: var(--neon-accent)`
    - Style focus indicator untuk semua input/textarea/button menggunakan `outline: 2px solid var(--neon-accent)`
    - _Requirements: 6.9, 7.2, 9.5_

  - [ ]* 9.4 Tulis property tests untuk form validation (Property 7 dan 8)
    - **Property 7: Form Validation Flags All Empty Required Fields**
    - **Validates: Requirements 6.5**
    - **Property 8: Email Validation Rejects All Invalid Formats**
    - **Validates: Requirements 6.6**
    - Implementasikan test Property 7 menggunakan `fc.record` dengan kombinasi string kosong dan terisi; verifikasi bahwa hanya field yang kosong yang mendapat error
    - Implementasikan test Property 8 dengan dua `fc.assert` terpisah: satu untuk invalid emails (string tanpa `@` valid), satu untuk valid emails menggunakan `fc.emailAddress()`
    - _Requirements: 6.5, 6.6_

  - [ ]* 9.5 Tulis unit tests untuk Contact Section
    - Test `form-submit-success.test.js`: isi semua field dengan nilai valid, submit form, verifikasi `.success-message` visible
    - Test `form-submit-empty.test.js`: submit form kosong, verifikasi error messages muncul pada ketiga field
    - Test `social-links.test.js`: verifikasi tiga social link elements ada, semuanya memiliki `target="_blank"` dan `aria-label`
    - _Requirements: 6.4, 6.5, 6.7, 6.8_

- [ ] 10. Implementasi global accessibility dan finishing touches
  - [~] 10.1 Audit dan perbaiki accessibility di seluruh `index.html` dan `style.css`
    - Pastikan semua `<img>` memiliki `alt` attribute non-kosong (termasuk fallback avatar)
    - Pastikan semua icon-only elements (social links, hamburger button) memiliki `aria-label`
    - Verifikasi heading hierarchy: `<h1>` hanya di Hero, `<h2>` di setiap section heading, `<h3>` untuk sub-items jika ada — tidak ada level skipping
    - Tambahkan visible focus indicator CSS untuk semua interactive elements: `button:focus-visible, a:focus-visible, input:focus-visible, textarea:focus-visible { outline: 2px solid var(--neon-accent); outline-offset: 2px; }`
    - Pastikan `<meta name="viewport" content="width=device-width, initial-scale=1">` ada di `<head>`
    - _Requirements: 9.2, 9.3, 9.4, 9.5, 9.6, 8.4_

  - [~] 10.2 Responsivitas dan visual polish di `style.css`
    - Tambahkan `min-width: 320px` handling dan pastikan tidak ada horizontal scroll di viewport 320px–2560px
    - Pastikan semua section memiliki `padding: 0 max(16px, ...)` di viewport `< 768px` sesuai requirement 7.4
    - Verifikasi Projects grid: 2–3 kolom di `≥768px`, 1 kolom di `<768px`
    - Verifikasi font stacks dengan system fallback untuk CDN failure (Space Grotesk, Inter, JetBrains Mono)
    - Tambahkan `overflow-x: hidden` pada `body` sebagai safety net
    - _Requirements: 7.3, 7.4, 8.1, 8.3_

  - [ ]* 10.3 Tulis property tests untuk DOM structure (Property 9 dan 10)
    - **Property 9: All Image Elements Have Non-Empty Alt Attributes**
    - **Validates: Requirements 9.2**
    - **Property 10: Heading Hierarchy Is Sequential Without Skipping Levels**
    - **Validates: Requirements 9.6**
    - Implementasikan kedua tests menggunakan `JSDOM` dengan `fs.readFileSync('index.html')` sesuai contoh di design.md — test ini bersifat structural/snapshot bukan PBT murni, tetapi ikuti format yang sama

- [~] 11. Final checkpoint — Semua tests pass dan halaman siap
  - Ensure all tests pass, ask the user if questions arise.

---

## Notes

- Tasks bertanda `*` adalah opsional dan dapat dilewati untuk MVP yang lebih cepat
- Setiap task mereferensikan requirement spesifik untuk traceability
- Checkpoint di Task 4, 8, dan 11 memastikan validasi incremental
- Form validation adalah client-side only — tidak ada backend submit
- CDN fallback fonts dan icon sudah didefinisikan di design.md dan harus diimplementasikan sesuai spec
- Vitest + fast-check hanya sebagai `devDependencies`; tidak mempengaruhi output produksi
- Jalankan tests dengan `npx vitest --run` dari root project

---

## Task Dependency Graph

```json
{
  "waves": [
    { "id": 0, "tasks": ["1"] },
    { "id": 1, "tasks": ["2.1", "2.2"] },
    { "id": 2, "tasks": ["2.3", "3.1", "3.2"] },
    { "id": 3, "tasks": ["2.4", "2.5", "3.3", "5.1", "6.1", "7.1"] },
    { "id": 4, "tasks": ["5.2", "6.2", "7.2", "9.1"] },
    { "id": 5, "tasks": ["5.3", "5.4", "6.3", "6.4", "7.3", "7.4", "9.2", "9.3"] },
    { "id": 6, "tasks": ["9.4", "9.5", "10.1", "10.2"] },
    { "id": 7, "tasks": ["10.3"] }
  ]
}
```

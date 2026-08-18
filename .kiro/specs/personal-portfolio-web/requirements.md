# Requirements Document

## Introduction

Fitur ini mendefinisikan sebuah halaman web portofolio pribadi satu halaman (*single-page*) yang bersih dan modern untuk seorang Software Engineer berpengalaman 5 tahun di bidang cloud dan fintech. Halaman dibangun menggunakan HTML, CSS, dan JavaScript vanilla dengan tampilan minimalis, tema gelap (*dark theme*), dan aksen warna neon. Halaman mencakup lima bagian utama: Hero/Perkenalan, Pengalaman Kerja, Proyek Pilihan, Lencana Sertifikasi, dan Kontak/Media Sosial.

---

## Glossary

- **Page**: Halaman web portofolio tunggal yang dimuat di browser
- **Hero_Section**: Bagian paling atas halaman yang menampilkan identitas dan perkenalan singkat
- **Experience_Section**: Bagian yang menampilkan riwayat pengalaman kerja utama
- **Projects_Section**: Bagian yang menampilkan daftar proyek pilihan beserta tautan GitHub
- **Certifications_Section**: Bagian yang menampilkan lencana sertifikasi profesional
- **Contact_Section**: Bagian yang menampilkan formulir kontak dan tautan media sosial
- **Navigation**: Bilah navigasi tetap (*sticky*) yang memungkinkan pengguna berpindah antar bagian
- **Theme**: Skema warna dark (latar belakang gelap) dengan aksen neon
- **Neon_Accent**: Warna aksen cerah bernuansa neon (hijau, cyan, atau ungu) yang digunakan untuk elemen interaktif dan sorotan
- **Visitor**: Pengguna yang mengakses halaman portofolio melalui browser
- **Project_Card**: Komponen UI yang menampilkan informasi satu proyek beserta tautan GitHub
- **Certification_Badge**: Komponen UI yang menampilkan satu lencana sertifikasi profesional
- **Contact_Form**: Formulir HTML yang memungkinkan Visitor mengirim pesan langsung dari halaman
- **Social_Link**: Tautan yang mengarah ke profil media sosial (LinkedIn, X, DEV Community)
- **Smooth_Scroll**: Animasi perpindahan halaman secara mulus saat navigasi diklik
- **Viewport**: Area tampilan browser yang terlihat oleh Visitor

---

## Requirements

### Requirement 1: Struktur dan Navigasi Halaman

**User Story:** As a Visitor, I want to navigate the portfolio page easily, so that I can quickly find the information I am looking for.

#### Acceptance Criteria

1. THE Page SHALL contain exactly five sections in this order: Hero_Section, Experience_Section, Projects_Section, Certifications_Section, and Contact_Section.
2. THE Navigation SHALL remain fixed at the top of the Viewport at all times while the Visitor scrolls.
3. THE Navigation SHALL contain links corresponding to each of the five sections.
4. WHEN a Visitor clicks a Navigation link, THE Page SHALL scroll to the corresponding section using Smooth_Scroll animation.
5. WHEN the Visitor's current scroll position enters a section, THE Navigation SHALL highlight the active link for that section.
6. THE Page SHALL be structured using a single HTML file with semantic HTML5 elements (`<header>`, `<nav>`, `<section>`, `<main>`, `<footer>`).
7. WHERE a Visitor accesses the Page on a mobile device with a viewport width less than 768px, THE Navigation SHALL collapse into a hamburger menu icon.
8. WHEN a Visitor taps the hamburger menu icon, THE Navigation SHALL expand to display all section links in a vertical dropdown overlay.

---

### Requirement 2: Hero / Perkenalan Singkat

**User Story:** As a Visitor, I want to see a clear and compelling introduction at the top of the page, so that I immediately understand who the person is and what they do.

#### Acceptance Criteria

1. THE Hero_Section SHALL display the engineer's full name as the primary heading (`<h1>`).
2. THE Hero_Section SHALL display a professional title (e.g., "Software Engineer — Cloud & Fintech") as a subtitle.
3. THE Hero_Section SHALL display a short bio of no more than three sentences summarizing the engineer's 5-year background in cloud and fintech.
4. THE Hero_Section SHALL display a professional profile photo or avatar with a circular or rounded-square shape.
5. THE Hero_Section SHALL display a primary call-to-action button labeled "View My Work" that scrolls to Projects_Section when clicked.
6. THE Hero_Section SHALL display a secondary call-to-action button labeled "Contact Me" that scrolls to Contact_Section when clicked.
7. THE Hero_Section SHALL display the Neon_Accent color on at least the primary call-to-action button border or background to draw visual attention.
8. WHEN the Page first loads, THE Hero_Section SHALL animate the heading and subtitle into view using a fade-in or slide-up CSS animation with a duration between 400ms and 800ms.

---

### Requirement 3: Pengalaman Kerja Utama

**User Story:** As a Visitor, I want to see the engineer's work history, so that I can evaluate their professional background and career progression.

#### Acceptance Criteria

1. THE Experience_Section SHALL display a section heading labeled "Experience".
2. THE Experience_Section SHALL list each work experience entry in reverse chronological order (most recent first).
3. FOR EACH work experience entry, THE Experience_Section SHALL display: company name, job title, employment period (start month/year – end month/year or "Present"), and a list of key responsibilities or achievements.
4. THE Experience_Section SHALL display at least two work experience entries.
5. WHEN a Visitor hovers over a work experience entry on a device with a pointer (non-touch device), THE Experience_Section SHALL apply a left-border highlight using the Neon_Accent color to indicate focus.
6. THE Experience_Section SHALL use a vertical timeline or card layout that is readable on both desktop and mobile viewports.

---

### Requirement 4: Daftar Proyek Pilihan

**User Story:** As a Visitor, I want to browse the engineer's selected projects with links to their code, so that I can assess their technical skills and areas of expertise.

#### Acceptance Criteria

1. THE Projects_Section SHALL display a section heading labeled "Projects".
2. THE Projects_Section SHALL display at least three Project_Cards in a responsive grid layout.
3. FOR EACH Project_Card, THE Projects_Section SHALL display: project name, a short description of no more than two sentences, a list of technology tags (e.g., "Go", "AWS", "React"), and a clickable GitHub link.
4. WHEN a Visitor clicks the GitHub link on a Project_Card, THE Page SHALL open the corresponding GitHub repository URL in a new browser tab.
5. WHEN a Visitor hovers over a Project_Card on a device with a pointer, THE Project_Card SHALL apply a box-shadow or border effect using the Neon_Accent color.
6. WHERE a Visitor accesses the Page on a viewport width of 768px or wider, THE Projects_Section SHALL display Project_Cards in a two- or three-column grid.
7. WHERE a Visitor accesses the Page on a viewport width less than 768px, THE Projects_Section SHALL display Project_Cards in a single-column layout.

---

### Requirement 5: Lencana Sertifikasi

**User Story:** As a Visitor, I want to see the engineer's professional certifications, so that I can verify their validated technical expertise.

#### Acceptance Criteria

1. THE Certifications_Section SHALL display a section heading labeled "Certifications".
2. THE Certifications_Section SHALL display at least two Certification_Badges.
3. FOR EACH Certification_Badge, THE Certifications_Section SHALL display: certification name, issuing organization name, and the year the certification was issued or last renewed.
4. WHERE a certification has a publicly verifiable URL, THE Certification_Badge SHALL include a clickable "Verify" link that opens the verification page in a new browser tab.
5. THE Certifications_Section SHALL display Certification_Badges in a responsive flex or grid layout that wraps on smaller viewports.
6. WHEN a Visitor hovers over a Certification_Badge on a device with a pointer, THE Certification_Badge SHALL display a subtle scale transform or glow effect using the Neon_Accent color.

---

### Requirement 6: Kontak dan Media Sosial

**User Story:** As a Visitor, I want to contact the engineer or visit their social profiles, so that I can reach out for professional opportunities or collaboration.

#### Acceptance Criteria

1. THE Contact_Section SHALL display a section heading labeled "Contact".
2. THE Contact_Section SHALL display a Contact_Form with the following fields: name (text input), email address (email input), and message (textarea).
3. THE Contact_Form SHALL mark the name, email, and message fields as required.
4. WHEN a Visitor submits the Contact_Form with all required fields filled, THE Contact_Form SHALL display a success confirmation message below the form indicating the message has been sent.
5. WHEN a Visitor submits the Contact_Form with one or more required fields empty, THE Contact_Form SHALL display an inline validation error message adjacent to each empty required field without refreshing the Page.
6. WHEN a Visitor submits the Contact_Form with an email field value that does not match a valid email format, THE Contact_Form SHALL display an inline validation error message on the email field.
7. THE Contact_Section SHALL display Social_Link icons for LinkedIn, X (formerly Twitter), and DEV Community, each opening the corresponding profile URL in a new browser tab.
8. THE Contact_Section SHALL display Social_Link icons using recognizable SVG icons or an icon font (e.g., Font Awesome) for LinkedIn, X, and DEV Community.
9. WHEN a Visitor hovers over a Social_Link icon on a device with a pointer, THE Social_Link SHALL change color to the Neon_Accent color.

---

### Requirement 7: Visual Design dan Tema

**User Story:** As a Visitor, I want the portfolio to have a professional and visually consistent dark minimalist aesthetic, so that it reflects the engineer's modern technical identity.

#### Acceptance Criteria

1. THE Page SHALL use a dark background color with a luminance value below 15% (e.g., `#0a0a0a`, `#0d1117`, or equivalent) as the primary page background.
2. THE Page SHALL use the Neon_Accent color consistently for interactive elements, hover states, active navigation links, and section dividers.
3. THE Page SHALL use no more than three typefaces: one for headings, one for body text, and optionally one for code or monospace labels.
4. THE Page SHALL apply consistent horizontal padding of at least 16px on all sections on viewports narrower than 768px to prevent content from touching screen edges.
5. THE Page SHALL define all colors and spacing values as CSS custom properties (variables) in the `:root` selector to allow easy theme adjustments.
6. THE Page SHALL achieve a Lighthouse Performance score of 80 or above when tested on a standard desktop connection.
7. THE Page SHALL achieve a Lighthouse Accessibility score of 90 or above, including sufficient color contrast ratios for all text elements as defined by WCAG 2.1 AA.

---

### Requirement 8: Responsivitas dan Kompatibilitas Browser

**User Story:** As a Visitor, I want the portfolio to display correctly on any device and modern browser, so that I can view it regardless of my preferred platform.

#### Acceptance Criteria

1. THE Page SHALL use a responsive layout that adapts to viewport widths from 320px to 2560px without horizontal scroll overflow.
2. THE Page SHALL render correctly on the latest stable versions of Chrome, Firefox, Safari, and Edge browsers.
3. THE Page SHALL use CSS Flexbox or CSS Grid as the primary layout mechanism for all multi-column sections.
4. THE Page SHALL include a `<meta name="viewport" content="width=device-width, initial-scale=1">` tag to ensure correct scaling on mobile devices.
5. THE Page SHALL load all required assets (fonts, icons, images) without dependency on a build tool or package manager, using CDN links or self-hosted files.

---

### Requirement 9: Performa dan Aksesibilitas

**User Story:** As a Visitor, I want the portfolio page to load quickly and be accessible to assistive technologies, so that everyone can access the content efficiently.

#### Acceptance Criteria

1. THE Page SHALL have a total initial page load size of no more than 2MB on a cold load (excluding externally cached CDN assets).
2. THE Page SHALL include `alt` attributes on all `<img>` elements with descriptive text.
3. THE Page SHALL include `aria-label` attributes on all icon-only interactive elements (Social_Link icons, hamburger menu button).
4. THE Page SHALL ensure all interactive elements (buttons, links, form inputs) are reachable and operable via keyboard navigation using Tab and Enter/Space keys.
5. WHEN a keyboard Visitor navigates to an interactive element using Tab, THE Page SHALL display a visible focus indicator styled with the Neon_Accent color.
6. THE Page SHALL use heading elements (`<h1>` through `<h4>`) in a logical, hierarchical order without skipping levels.

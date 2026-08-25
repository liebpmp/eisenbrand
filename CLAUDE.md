# CLAUDE.md — Eisenbrand Ästhetik Landing Pages

## Projekt-Übersicht
3 Landing Pages für eisenbrand ästhetik (Plastische Chirurgie, Schweinfurt/Würzburg):
1. **Operative Bauchdeckenstraffung** → `/bauchdeckenstraffung.html`
2. **Brustverkleinerung/-straffung** → `/brustverkleinerung.html` (ggf. Split in 2 Seiten)
3. **Lipödem** → `/lipoedem.html`

Plus **Hub-Page** → `/index.html` (Übersicht aller Behandlungen, wie bei Villa Bella)

## Design-Richtlinien

### Brand — eisenbrand ästhetik
Lies `BRAND-GUIDE.md` für alle Details. Kurzfassung:
- **Primärfarbe:** `#a19364` (Gold/Bronze) — für Buttons, Akzente, Hover-States
- **Hintergrund:** Weiß (`#fff`) mit Gold-Akzenten
- **Text:** Dunkelgrau `#333` / Schwarz `#000`
- **Heading-Font:** Julius Sans One (Google Fonts) — elegant, dünn, Uppercase für Hauptüberschriften
- **Body-Font:** Open Sans (Google Fonts) — clean, modern
- **Akzent-Font:** Montserrat oder Raleway für Subheadings
- **Charakter:** Elegant-medizinisch, warm-premium, NICHT klinisch-kalt

### Referenz-Design: Bestehende Eisenbrand LPs
Die bestehenden Eisenbrand-LPs (brust.eisenbrand-aesthetik.de, liposuktion.eisenbrand-aesthetik.de) nutzen einen **modernen Funnel-Stil** mit:
- Full-width Hero mit CTA
- Trust-Badges (Jameda Note 1,0, 5.000+ Patienten)
- Sections mit Icons + kurzen Benefit-Texten
- Testimonials mit Jameda-Referenz
- Mehrstufiger Ablauf (nummeriert 1-6)
- FAQ-Akkordeon
- Kontaktformular am Ende
- Rückrufservice-Formular

### Struktur-Referenz: Villa Bella München LPs
Orientiere dich an der Section-Struktur unserer Villa Bella LPs (villa-bella-muenchen.de):
1. **Hero** — Headline + Sub + Vorteile-Bullets + CTA + Trust-Badges
2. **Emotionaler Hook** — "Kennen Sie dieses Gefühl?" (Pain Points ansprechen)
3. **Methoden-Überblick** — Welche Verfahren, kurz erklärt
4. **Ablauf** — Nummerierte Steps (Beratung → Planung → OP → Nachsorge → Ergebnis)
5. **Vergleichstabelle** — "Warum Eisenbrand Ästhetik?" vs. generische Anbieter
6. **Testimonials** — Echte Bewertungen (von Jameda, siehe Content-Files)
7. **FAQ** — Häufigste Fragen (Kosten, Schmerzen, Narben, Ergebnis)
8. **CTA / Kontaktformular** — Beratungstermin vereinbaren

### Technische Anforderungen
- **Einzelne HTML-Dateien** (kein React/Vite — plain HTML + CSS + minimal JS)
- **Responsive** — Mobile-first, perfekt auf Smartphone
- **Inline CSS** oder `<style>` im `<head>` (alles in einer Datei pro LP)
- **Google Fonts:** Julius Sans One, Open Sans, Montserrat (via `<link>`)
- **Formular:** Name, E-Mail, Telefon, Nachricht — action wird später ergänzt (Zapier Webhook)
- **GTM:** Platzhalter `<!-- GTM -->` im Head + Body (wird später ergänzt)
- **Bilder:** Platzhalter mit passenden alt-Texten (werden später durch echte Bilder ersetzt)
- **Max. 800 Zeilen pro HTML-Datei** (Section-by-Section aufbauen)

### CSS-Stil-Vorlage (aus bestehenden Eisenbrand/Villa Bella LPs)
```css
/* Hero */
.hero { background: linear-gradient(135deg, #1a1a2e 0%, #16213e 50%, #0f3460 100%); color: #fff; padding: 80px 20px; text-align: center; }
.hero h1 { font-family: 'Julius Sans One', sans-serif; font-size: 2.8rem; letter-spacing: 2px; }

/* Gold Accent */
.gold { color: #a19364; }
.btn-gold { background: #a19364; color: #fff; border: none; padding: 16px 32px; border-radius: 8px; font-size: 1.1rem; cursor: pointer; }
.btn-gold:hover { background: #8a7d56; }

/* Trust Badges */
.trust-bar { display: flex; justify-content: center; gap: 40px; padding: 20px; }
.trust-item { text-align: center; font-size: 0.9rem; }

/* Sections */
.section { padding: 80px 20px; max-width: 1100px; margin: 0 auto; }
.section-dark { background: #f8f7f4; }

/* Testimonials */
.testimonial { background: #fff; border-left: 4px solid #a19364; padding: 24px; margin: 20px 0; border-radius: 8px; box-shadow: 0 2px 8px rgba(0,0,0,0.05); }

/* FAQ */
.faq-item { border-bottom: 1px solid #eee; padding: 16px 0; cursor: pointer; }
```

## Content pro LP
- **Bauchdeckenstraffung:** Lies `CONTENT-BAUCHDECKENSTRAFFUNG.md` — Methoden, WAL-Kombi, Ablauf
- **Brustverkleinerung/-straffung:** Lies `CONTENT-BRUSTVERKLEINERUNG-STRAFFUNG.md` — 3 Schnitttechniken, Drainagen-frei
- **Lipödem:** Lies `CONTENT-LIPOEDEM.md` — WAL-Methode, Problemzonen, Stadien, Patientenstimmen

## Arzt-Info für alle LPs
- **Alexander Eisenbrand** — Facharzt für Plastische und Ästhetische Chirurgie
- **Dr. Kara Kazarian** — Spezialist (primär Liposuktion + Brustvergrößerung)
- Standort: Schweinfurt (nahe Würzburg), auch Patienten aus Nürnberg, Frankfurt
- Jameda Bestnote 1,0
- Über 5.000 zufriedene Patienten / 15+ Jahre Erfahrung

## Formular-Logik (KRITISCH — exakt so implementieren!)

### Hidden Fields (auf JEDER LP)
```html
<input type="text" id="utm_source" name="utm_source" style="display:none;" />
<input type="text" id="utm_campaign" name="utm_campaign" style="display:none;"/>
<input type="text" id="utm_term" name="utm_term" style="display:none;"/>
<input type="text" id="lp_url" name="lp_url" style="display:none;"/>
<input type="text" id="utm_content" name="utm_content" style="display:none;"/>
<input type="text" id="utm_medium" name="utm_medium" style="display:none;"/>
<input type="text" id="gclid" name="gclid" style="display:none;"/>
<input type="text" id="ad_id" name="ad_id" style="display:none;"/>
<input type="text" id="keyword" name="keyword" style="display:none;"/>
<input type="text" id="placement" name="placement" style="display:none;"/>
<input type="text" id="matchtype" name="matchtype" style="display:none;"/>
<input type="text" id="behandlung_id" name="behandlung_id" style="display:none;"/>
<input type="text" id="behandlung_subkategorie" name="behandlung_subkategorie" style="display:none;"/>
```

### Meta-Tag pro LP (im `<head>`)
Jede LP braucht einen eigenen Meta-Tag:
```html
<!-- Bauchdeckenstraffung: -->
<meta name="page-specific-behandlung" data-behandlung-id="542" data-behandlung_subkategorie="Bauchdeckenstraffung">
<!-- Brustverkleinerung: -->
<meta name="page-specific-behandlung" data-behandlung-id="534" data-behandlung_subkategorie="Brustverkleinerung">
<!-- Bruststraffung: -->
<meta name="page-specific-behandlung" data-behandlung-id="535" data-behandlung_subkategorie="Bruststraffung">
<!-- Lipödem: -->
<meta name="page-specific-behandlung" data-behandlung-id="543" data-behandlung_subkategorie="Lipödem">
```

### Submit-Logik (JS — auf JEDER LP identisch)
```javascript
document.addEventListener('DOMContentLoaded', function() {
    // 1. UTM-Parameter aus URL auslesen und in Hidden Fields schreiben
    const params = new URLSearchParams(window.location.search);
    ['utm_source','utm_campaign','utm_term','utm_content','utm_medium','gclid','ad_id','keyword','placement','matchtype'].forEach(p => {
        const el = document.getElementById(p);
        if (el && params.get(p)) el.value = params.get(p);
    });
    // LP URL setzen
    const lpUrl = document.getElementById('lp_url');
    if (lpUrl) lpUrl.value = window.location.href;

    // 2. Behandlung aus Meta-Tag lesen
    const metaTag = document.querySelector('meta[name="page-specific-behandlung"]');
    if (metaTag) {
        document.getElementById('behandlung_id').value = metaTag.getAttribute('data-behandlung-id');
        document.getElementById('behandlung_subkategorie').value = metaTag.getAttribute('data-behandlung_subkategorie');
    }

    // 3. Formular-Submit → Zapier Webhook + Redirect
    const form = document.querySelector('#kontakt-form');
    if (form) {
        form.addEventListener('submit', function(e) {
            e.preventDefault();
            const formData = new FormData(form);

            // GTM dataLayer Event
            window.dataLayer = window.dataLayer || [];
            window.dataLayer.push({
                'event': 'generate_lead',
                'treatment': document.getElementById('behandlung_subkategorie')?.value || ''
            });

            fetch('https://hooks.zapier.com/hooks/catch/10412562/2uqqrw5/', {
                method: 'POST',
                body: formData
            })
            .then(response => response.json())
            .then(result => {
                console.log('Success:', result);
                // Redirect-URL pro LP (Cituro Booking):
                // brustverkleinerung.html + bruststraffung.html → https://app.cituro.com/booking/6845463?presetService=11efb6dbd3fe834d9c68071c98230631
                // bauchdeckenstraffung.html → https://app.cituro.com/booking/6845463?presetService=11efb6cf2b0d44c89c68071c98230631
                // lipoedem.html → https://app.cituro.com/booking/6845463?presetService=11efb6ddc7d13a06b0de174004522194
                window.location.href = REDIRECT_URL; // ← Variable oben im Script pro LP setzen!
            })
            .catch(error => {
                console.error('Error:', error);
                window.location.href = REDIRECT_URL;
            });
        });
    }
});
```

### GTM Container
```html
<!-- Google Tag Manager -->
<script>(function(w,d,s,l,i){w[l]=w[l]||[];w[l].push({'gtm.start':
new Date().getTime(),event:'gtm.js'});var f=d.getElementsByTagName(s)[0],
j=d.createElement(s),dl=l!='dataLayer'?'&l='+l:'';j.async=true;j.src=
'https://www.googletagmanager.com/gtm.js?id='+i+dl;f.parentNode.insertBefore(j,f);
})(window,document,'script','dataLayer','GTM-NPCN58H6');</script>
<!-- End Google Tag Manager -->

<!-- Google Tag Manager (noscript) — direkt nach <body> -->
<noscript><iframe src="https://www.googletagmanager.com/ns.html?id=GTM-NPCN58H6"
height="0" width="0" style="display:none;visibility:hidden"></iframe></noscript>
```

### Zapier Webhook
- **URL:** `https://hooks.zapier.com/hooks/catch/10412562/2uqqrw5/`
- **Method:** POST mit FormData (NICHT JSON!)
- **Felder:** Name, E-Mail, Telefon, Nachricht + alle Hidden Fields (UTM, gclid, behandlung_id, behandlung_subkategorie, lp_url, etc.)

### Redirect-URLs pro LP (Cituro Booking)
Nach erfolgreichem Formular-Submit wird auf die jeweilige Cituro-Buchungsseite weitergeleitet:
- **Brustverkleinerung:** `https://app.cituro.com/booking/6845463?presetService=11efb6dbd3fe834d9c68071c98230631`
- **Bruststraffung:** `https://app.cituro.com/booking/6845463?presetService=11efb6dbd3fe834d9c68071c98230631` (gleicher Link — "Beratung Brust")
- **Bauchdeckenstraffung:** `https://app.cituro.com/booking/6845463?presetService=11efb6cf2b0d44c89c68071c98230631`
- **Lipödem:** `https://app.cituro.com/booking/6845463?presetService=11efb6ddc7d13a06b0de174004522194` (wie Fettabsaugung)

## Kontakt-CTA (auf jeder LP)
- **Headline:** "Bereit für den ersten Schritt?" oder "Jetzt Beratungstermin vereinbaren"
- **Sub:** "Unverbindlich, persönlich, vertraulich"
- **Button:** "Beratungstermin vereinbaren →"
- **Trust:** ★★★★★ Jameda Note 1,0 | 5.000+ zufriedene Patienten | 15+ Jahre Erfahrung
- **Telefon:** 09721 2912200

## Hub-Page (index.html)
- Hero mit Eisenbrand-Branding
- 3 Treatment-Cards (Bauchdeckenstraffung, Brustverkleinerung, Lipödem) → jeweils verlinkt
- Trust-Section (Bewertungen, Erfahrung, Team)
- Kurze Vorstellung Alexander Eisenbrand + Dr. Kara Kazarian

## Build-Reihenfolge
1. Hub-Page (index.html)
2. Bauchdeckenstraffung (bauchdeckenstraffung.html)
3. Brustverkleinerung (brustverkleinerung.html)
4. Bruststraffung (bruststraffung.html)
5. Lipödem (lipoedem.html)

from pathlib import Path
import zipfile, shutil

out = Path("/mnt/data/AJ_Translations_site")
out.mkdir(exist_ok=True)

index_html = """<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta name="description" content="AJ Translations - Traduction, interprétation et services linguistiques.">
    <title>AJ Translations | Traduction & services linguistiques</title>
    <link rel="stylesheet" href="style.css">
</head>

<body>

    <header class="header">
        <a href="#accueil" class="brand">
            <img src="images/logo.png" alt="Logo AJ Translations">
            <span>AJ TRANSLATIONS</span>
        </a>

        <nav class="nav">
            <a href="#accueil">Accueil</a>
            <a href="#apropos">À propos</a>
            <a href="#services">Services</a>
            <a href="#contact">Contact</a>
        </nav>
    </header>

    <main>

        <section id="accueil" class="hero">
            <div class="hero-content">
                <p class="eyebrow">AJ TRANSLATIONS</p>
                <h1>Vos mots.<br><span>Notre expertise.</span></h1>
                <p class="hero-text">
                    Des services linguistiques professionnels pour faciliter
                    vos échanges, vos projets et vos déplacements.
                </p>

                <div class="hero-buttons">
                    <a href="#services" class="button button-primary">Découvrir nos services</a>
                    <a href="#contact" class="button button-secondary">Nous contacter</a>
                </div>
            </div>

            <div class="hero-logo">
                <img src="images/logo.png" alt="AJ Translations">
            </div>
        </section>

        <section id="apropos" class="section about">
            <div>
                <p class="eyebrow">À PROPOS</p>
                <h2>AJ Translations</h2>
            </div>

            <div class="about-text">
                <p>
                    AJ Translations propose des services linguistiques destinés
                    à accompagner particuliers, professionnels et visiteurs.
                </p>
                <p>
                    Notre objectif est de faciliter la communication et de
                    permettre à chacun de comprendre et d'être compris,
                    avec un service sérieux et adapté à chaque besoin.
                </p>
            </div>
        </section>

        <section id="services" class="section services">
            <div class="section-heading">
                <p class="eyebrow">NOS SERVICES</p>
                <h2>Des solutions linguistiques adaptées</h2>
                <p>
                    Découvrez les services proposés par AJ Translations.
                </p>
            </div>

            <div class="service-grid">

                <article class="service-card">
                    <div class="service-number">01</div>
                    <h3>Traduction</h3>
                    <p>
                        Traduction de contenus et de documents afin de
                        transmettre votre message clairement dans une autre langue.
                    </p>
                </article>

                <article class="service-card">
                    <div class="service-number">02</div>
                    <h3>Interprétation</h3>
                    <p>
                        Accompagnement linguistique pour faciliter les échanges
                        et la communication entre personnes parlant des langues différentes.
                    </p>
                </article>

                <article class="service-card">
                    <div class="service-number">03</div>
                    <h3>Traduction de documents</h3>
                    <p>
                        Traduction de documents professionnels, administratifs
                        ou personnels selon vos besoins.
                    </p>
                </article>

                <article class="service-card">
                    <div class="service-number">04</div>
                    <h3>Guide touristique</h3>
                    <p>
                        Accompagnement et assistance linguistique pour découvrir
                        une destination et faciliter les échanges avec les visiteurs.
                    </p>
                </article>

            </div>
        </section>

        <section id="contact" class="contact">
            <div>
                <p class="eyebrow">CONTACT</p>
                <h2>Un projet ou une question ?</h2>
                <p>
                    Contactez AJ Translations pour discuter de votre besoin
                    linguistique.
                </p>
            </div>

            <!-- Remplacez VOTRE_EMAIL@example.com par votre vraie adresse e-mail -->
            <a class="button button-primary" href="mailto:VOTRE_EMAIL@example.com">
                Nous contacter
            </a>
        </section>

    </main>

    <footer>
        <p>© 2026 AJ Translations — Tous droits réservés.</p>
    </footer>

</body>
</html>
"""

style_css = """@import url('https://fonts.googleapis.com/css2?family=DM+Sans:wght@400;500;600;700&family=Playfair+Display:wght@600;700&display=swap');

:root {
    --navy: #071b35;
    --navy-light: #102c4e;
    --gold: #c7953f;
    --gold-light: #e5c27b;
    --white: #ffffff;
    --cream: #f8f7f4;
    --text: #26313d;
    --muted: #687482;
    --border: #e7e3db;
}

* {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
}

html {
    scroll-behavior: smooth;
}

body {
    font-family: "DM Sans", Arial, sans-serif;
    color: var(--text);
    background: var(--white);
    line-height: 1.7;
}

.header {
    position: sticky;
    top: 0;
    z-index: 100;
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 14px 7%;
    background: rgba(255, 255, 255, 0.96);
    border-bottom: 1px solid var(--border);
    backdrop-filter: blur(10px);
}

.brand {
    display: flex;
    align-items: center;
    gap: 12px;
    color: var(--navy);
    text-decoration: none;
    font-weight: 700;
    letter-spacing: 1.5px;
}

.brand img {
    width: 54px;
    height: 54px;
    object-fit: contain;
}

.nav {
    display: flex;
    gap: 30px;
}

.nav a {
    color: var(--navy);
    text-decoration: none;
    font-size: 0.95rem;
    font-weight: 600;
    transition: color 0.2s ease;
}

.nav a:hover {
    color: var(--gold);
}

.hero {
    min-height: calc(100vh - 83px);
    display: grid;
    grid-template-columns: 1.15fr 0.85fr;
    align-items: center;
    gap: 50px;
    padding: 80px 10%;
    background:
        radial-gradient(circle at 80% 45%, rgba(199, 149, 63, 0.13), transparent 32%),
        linear-gradient(135deg, #ffffff 0%, #f7f7f5 100%);
}

.eyebrow {
    color: var(--gold);
    font-size: 0.78rem;
    font-weight: 700;
    letter-spacing: 3px;
    margin-bottom: 12px;
}

.hero h1 {
    color: var(--navy);
    font-family: "Playfair Display", Georgia, serif;
    font-size: clamp(3rem, 6vw, 5.8rem);
    line-height: 1.05;
    margin-bottom: 25px;
}

.hero h1 span {
    color: var(--gold);
}

.hero-text {
    max-width: 650px;
    color: var(--muted);
    font-size: 1.15rem;
    margin-bottom: 35px;
}

.hero-logo {
    display: flex;
    justify-content: center;
    align-items: center;
}

.hero-logo img {
    width: min(430px, 90%);
    filter: drop-shadow(0 18px 35px rgba(7, 27, 53, 0.10));
}

.hero-buttons {
    display: flex;
    gap: 15px;
    flex-wrap: wrap;
}

.button {
    display: inline-block;
    padding: 13px 23px;
    border-radius: 4px;
    text-decoration: none;
    font-weight: 700;
    transition: transform 0.2s ease, box-shadow 0.2s ease;
}

.button:hover {
    transform: translateY(-2px);
}

.button-primary {
    color: var(--white);
    background: var(--navy);
    box-shadow: 0 8px 20px rgba(7, 27, 53, 0.15);
}

.button-primary:hover {
    background: var(--navy-light);
}

.button-secondary {
    color: var(--navy);
    background: transparent;
    border: 1px solid var(--navy);
}

.section {
    padding: 100px 10%;
}

.about {
    display: grid;
    grid-template-columns: 0.8fr 1.2fr;
    gap: 80px;
    align-items: start;
}

h2 {
    color: var(--navy);
    font-family: "Playfair Display", Georgia, serif;
    font-size: clamp(2rem, 4vw, 3.4rem);
    line-height: 1.15;
}

.about-text {
    max-width: 700px;
    font-size: 1.05rem;
    color: var(--muted);
}

.about-text p + p {
    margin-top: 18px;
}

.services {
    background: var(--cream);
}

.section-heading {
    max-width: 700px;
    margin-bottom: 50px;
}

.section-heading > p:last-child {
    margin-top: 18px;
    color: var(--muted);
}

.service-grid {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    gap: 22px;
}

.service-card {
    position: relative;
    padding: 35px;
    background: var(--white);
    border: 1px solid var(--border);
    border-top: 3px solid var(--gold);
    transition: transform 0.25s ease, box-shadow 0.25s ease;
}

.service-card:hover {
    transform: translateY(-5px);
    box-shadow: 0 15px 35px rgba(7, 27, 53, 0.09);
}

.service-number {
    color: var(--gold);
    font-size: 0.8rem;
    font-weight: 700;
    letter-spacing: 2px;
    margin-bottom: 20px;
}

.service-card h3 {
    color: var(--navy);
    font-family: "Playfair Display", Georgia, serif;
    font-size: 1.65rem;
    margin-bottom: 12px;
}

.service-card p {
    color: var(--muted);
}

.contact {
    display: flex;
    justify-content: space-between;
    align-items: center;
    gap: 40px;
    padding: 80px 10%;
    background: var(--navy);
    color: var(--white);
}

.contact h2 {
    color: var(--white);
}

.contact p:not(.eyebrow) {
    color: #cbd3dd;
    margin-top: 15px;
    max-width: 650px;
}

.contact .button-primary {
    background: var(--gold);
    color: var(--navy);
    white-space: nowrap;
}

.contact .button-primary:hover {
    background: var(--gold-light);
}

footer {
    padding: 25px 10%;
    text-align: center;
    background: #041326;
    color: #aeb8c4;
    font-size: 0.85rem;
}

@media (max-width: 800px) {
    .header {
        padding: 12px 5%;
    }

    .brand span {
        font-size: 0.85rem;
    }

    .nav {
        gap: 14px;
    }

    .nav a {
        font-size: 0.82rem;
    }

    .hero {
        grid-template-columns: 1fr;
        text-align: center;
        padding: 70px 7%;
    }

    .hero-text {
        margin-left: auto;
        margin-right: auto;
    }

    .hero-buttons {
        justify-content: center;
    }

    .hero-logo {
        order: -1;
    }

    .hero-logo img {
        width: 230px;
    }

    .section {
        padding: 70px 7%;
    }

    .about {
        grid-template-columns: 1fr;
        gap: 35px;
    }

    .service-grid {
        grid-template-columns: 1fr;
    }

    .contact {
        flex-direction: column;
        align-items: flex-start;
        padding: 65px 7%;
    }
}

@media (max-width: 520px) {
    .header {
        flex-direction: column;
        gap: 8px;
    }

    .brand img {
        width: 42px;
        height: 42px;
    }

    .nav {
        gap: 12px;
    }

    .nav a {
        font-size: 0.75rem;
    }

    .hero {
        min-height: auto;
        padding-top: 55px;
    }

    .hero h1 {
        font-size: 3rem;
    }
}
"""

(out / "index.html").write_text(index_html, encoding="utf-8")
(out / "style.css").write_text(style_css, encoding="utf-8")

# Copy the uploaded logo into the expected folder/name.
img_dir = out / "images"
img_dir.mkdir(exist_ok=True)
src = Path("/mnt/data/c1a4797a-3ace-46cd-96d3-54012b32502a.png")
shutil.copy2(src, img_dir / "logo.png")

zip_path = Path("/mnt/data/AJ_Translations_site.zip")
with zipfile.ZipFile(zip_path, "w", zipfile.ZIP_DEFLATED) as z:
    for p in out.rglob("*"):
        if p.is_file():
            z.write(p, p.relative_to(out))

print(f"Fichiers créés : {zip_path}")

# Nova — Landing Page Example (exmp5)

A complete, styled landing page example built with `exmp5.html` + `exmp5.css`. Mobile-first responsive design with a design system driven by CSS variables (colors, shadows, radius, spacing).

## Files

- [exmp5.html](exmp5.html)
- [exmp5.css](exmp5.css)

## Breakpoints

| Range | Target | Key changes |
|---|---|---|
| < 600px | Smartphones | 1-column grids, hamburger menu, stacked hero buttons |
| 600px – 1024px | Tablets / iPad | 2-column grids, side-by-side hero buttons, split section becomes 2 columns |
| ≥ 1025px | Desktop / computers | Inline nav (hamburger hidden), 3-column feature/testimonial grids, 4-column footer |

---

## 1. Header / Navbar

```html
<header>
  <div class="navbar">
    <div class="logo">Nova<span>.</span></div>

    <button class="hamburger" onclick="document.querySelector('nav').classList.toggle('open')">
      &#9776;
    </button>

    <nav>
      <ul>
        <li><a href="#home">Home</a></li>
        <li><a href="#features">Features</a></li>
        <li><a href="#about">About</a></li>
        <li><a href="#testimonials">Testimonials</a></li>
        <li><a href="#contact">Contact</a></li>
      </ul>
    </nav>
  </div>
</header>
```

```css
header{
  position: sticky;
  top: 0;
  /* "sticky" = l'en-tête RESTE COLLÉ en haut de l'écran même quand on fait défiler la page vers le bas */
  z-index: 100;
  /* "z-index" = qui passe au-dessus de qui, comme des feuilles empilées. Plus le chiffre est grand,
     plus l'élément est "au-dessus" des autres visuellement */
  background-color: rgba(255,255,255,0.9); /* fond blanc presque opaque (0.9 = 90% visible) */
  backdrop-filter: blur(8px);
  /* floute légèrement ce qu'il y a DERRIÈRE l'en-tête, comme un effet de verre dépoli */
  box-shadow: var(--shadow-sm);
}

.navbar{
  display: flex;
  /* "flex" = range les éléments à l'intérieur en ligne, côte à côte (au lieu de les empiler) */
  align-items: center;        /* centre-les verticalement */
  justify-content: space-between; /* pousse le logo à gauche et le menu à droite, avec l'espace au milieu */
  padding: 1rem 1.25rem;
  max-width: var(--container-width);
  margin: 0 auto;
}

.logo{
  font-size: 1.4rem;
  font-weight: 800; /* très gras */
  color: var(--color-dark);
}

.logo span{
  color: var(--color-primary); /* le petit point après "Nova" est coloré différemment */
}

.hamburger{
  /* le bouton "≡" qui n'apparaît que sur téléphone/tablette pour ouvrir le menu */
  background: none;
  border: none;
  font-size: 1.6rem;
  color: var(--color-dark);
  cursor: pointer;
  z-index: 200; /* toujours au-dessus de tout, même quand le menu est ouvert */
}

nav{
  position: fixed;
  /* "fixed" = reste à un endroit précis de l'écran, même si on fait défiler la page */
  top: 0;
  right: -100%;
  /* "-100%" = le menu est caché complètement HORS de l'écran, à droite, par défaut (sur mobile) */
  height: 100vh; /* prend toute la hauteur de l'écran */
  width: 70%;
  max-width: 320px;
  background-color: var(--color-bg);
  box-shadow: var(--shadow-md);
  padding: 6rem 2rem;
  transition: right var(--transition); /* glisse en douceur quand il s'ouvre/se ferme */
  z-index: 150;
}

nav.open{
  /* Cette classe "open" est ajoutée par le petit bouton hamburger (voir le fichier HTML)
     quand on clique dessus. Elle fait REVENIR le menu dans l'écran. */
  right: 0;
}

nav ul{
  display: flex;
  flex-direction: column; /* les liens du menu s'empilent verticalement (mobile) */
  gap: 1.5rem;            /* espace entre chaque lien */
  font-weight: 600;
}

nav a{
  position: relative;
  color: var(--color-dark);
}

nav a:hover{
  color: var(--color-primary); /* le lien change de couleur quand on passe la souris dessus */
}
```

**Screenshot:**
![Header](<header.png>)
---


## 2. Features (3 cards)

```html
<section id="features" class="section">
  <div class="container">
    <div class="section-header">
      <h2>Why Choose Nova</h2>
      <p>Everything you need to build a modern, responsive website — designed for smartphones, tablets, and desktops.</p>
    </div>

    <div class="grid">
      <div class="card">
        <div class="icon">&#9889;</div>
        <h3>Fast</h3>
        <p>Optimized, lightweight code that loads instantly on any device.</p>
      </div>
      <div class="card">
        <div class="icon">&#128241;</div>
        <h3>Responsive</h3>
        <p>Looks great on phones, iPads, and desktop screens alike.</p>
      </div>
      <div class="card">
        <div class="icon">&#127912;</div>
        <h3>Beautiful</h3>
        <p>A clean, modern design system built with care and consistency.</p>
      </div>
    </div>
  </div>
</section>
```

```css
.grid{
  display: grid;
  /* "grid" = range les éléments en tableau (lignes et colonnes) qui s'adapte tout seul */
  grid-template-columns: 1fr;
  /* "1fr" = une seule colonne qui prend toute la largeur (donc les cartes s'empilent, sur mobile) */
  gap: 1.5rem; /* espace entre chaque carte */
}

.card{
  background-color: #fff;
  border-radius: var(--radius);
  padding: 2rem;
  box-shadow: var(--shadow-sm); /* légère ombre pour donner un effet de "carte" qui flotte un peu */
  transition: transform var(--transition), box-shadow var(--transition);
  text-align: center;
}

.card:hover{
  transform: translateY(-6px); /* la carte remonte légèrement quand on passe la souris dessus */
  box-shadow: var(--shadow-md); /* et l'ombre s'agrandit, pour accentuer l'effet */
}

.card .icon{
  width: 56px;
  height: 56px;
  margin: 0 auto 1.25rem; /* centré, avec de l'espace en dessous */
  border-radius: 50%; /* 50% = fait un cercle parfait */
  background-color: rgba(108, 92, 231, 0.12); /* violet très clair et transparent, en fond du rond */
  color: var(--color-primary);
  display: flex;
  align-items: center;
  justify-content: center; /* centre l'icône (emoji) à l'intérieur du rond */
  font-size: 1.5rem;
}

.card h3{
  margin-bottom: 0.5rem;
  color: var(--color-dark);
}

.card p{
  color: var(--color-muted);
  font-size: 0.95rem;
}
```

**Screenshot:**
![Why chose...](<whychose.png>)

---

## 3. Footer

```html
<footer id="contact">
  <div class="footer-grid container">
    <div>
      <h4>Nova</h4>
      <p>Building clean, responsive websites for everyone.</p>
    </div>
    <div>
      <h4>Company</h4>
      <ul>
        <li><a href="#home">Home</a></li>
        <li><a href="#about">About</a></li>
        <li><a href="#features">Features</a></li>
      </ul>
    </div>
    <div>
      <h4>Resources</h4>
      <ul>
        <li><a href="#">Blog</a></li>
        <li><a href="#">Support</a></li>
        <li><a href="#">FAQ</a></li>
      </ul>
    </div>
    <div>
      <h4>Contact</h4>
      <ul>
        <li><a href="mailto:hello@nova.com">hello@nova.com</a></li>
        <li><a href="#">Twitter</a></li>
        <li><a href="#">LinkedIn</a></li>
      </ul>
    </div>
  </div>

  <div class="footer-bottom">
    &copy; 2026 Nova. All rights reserved.
  </div>
</footer>
```
```css
footer{
  background-color: var(--color-dark);
  color: rgba(255,255,255,0.8);
  margin-top: 4rem;
}

.footer-grid{
  display: grid;
  grid-template-columns: 1fr;
  /* sur mobile : une seule colonne, donc les 4 blocs (Nova / Company / Resources / Contact)
     s'empilent les uns sous les autres */
  gap: 2rem;
  padding: 3rem 1.25rem 2rem;
}

.footer-grid h4{
  color: #fff;
  margin-bottom: 1rem;
}

.footer-grid ul{
  display: flex;
  flex-direction: column;
  gap: 0.6rem;
}

.footer-grid a:hover{
  color: var(--color-accent); /* les liens du pied de page deviennent turquoise au survol */
}

.footer-bottom{
  /* la toute dernière ligne, avec le "copyright" */
  text-align: center;
  padding: 1.25rem;
  border-top: 1px solid rgba(255,255,255,0.1); /* une fine ligne de séparation au-dessus */
  font-size: 0.85rem;
}
```

**Screenshot:**
![Footer](<footer.png>)

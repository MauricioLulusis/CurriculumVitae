# 🚀 Desplegar el CV en tu dominio propio

Tu sitio es **un solo archivo estático** (`index.html`, sin dependencias). Eso hace el deploy
trivial y **gratis** en cualquier hosting de sitios estáticos. Solo pagás el dominio (~US$10/año).

Carpeta a desplegar (esta misma):
```
Curriculum vitae/
├── index.html                 ← el sitio
└── Lulusis Mauricio CV.pdf     ← lo usa el botón "PDF" (subilo también)
```

---

## ⭐ Camino elegido: GitHub → Netlify  (auto-deploy)

✅ Ya está: el CV está en GitHub → https://github.com/MauricioLulusis/CurriculumVitae (rama `main`).
Conectando Netlify al repo, cada `git push` redespliega el sitio automáticamente.

### 1) Crear cuenta en Netlify
https://app.netlify.com → **Sign up** → **GitHub** → autorizá con la cuenta **MauricioLulusis**.

### 2) Importar el repo y deployar
1. **Add new site → Import an existing project → Deploy with GitHub**.
2. Autorizá Netlify (si pide, elegí "Only select repositories" → **CurriculumVitae**).
3. Configuración del build (es un sitio estático, NO necesita build):
   - **Branch to deploy:** `main`
   - **Build command:** *(vacío)*
   - **Publish directory:** `.`  *(la raíz)*
4. **Deploy site** → en segundos queda online en `https://<nombre-random>.netlify.app`.
5. (Opcional) *Site configuration → Change site name* para elegir un subdominio lindo.

### 3) Dominio propio
En el sitio → **Domain management → Add a domain** → escribí `mauriciolulusiscv.com`:
- **Si Netlify ofrece registrarlo** ahí mismo (*Register domain*), lo comprás y queda todo
  configurado solo (DNS de Netlify + HTTPS automático). ✅
- **Si no**, comprá el dominio en un registrador (Cloudflare ~US$9 / Namecheap ~US$11) y:
  - Opción fácil: usá **Netlify DNS** → Netlify te da 4 *nameservers*; los pegás en el registrador.
  - Opción manual: cargás un **A** `@` → `75.2.60.5` y un **CNAME** `www` → tu-sitio.netlify.app
    *(usá siempre los valores que muestre Netlify).*
- HTTPS: Netlify emite el certificado (Let's Encrypt) solo. ✅

### 4) Actualizar el sitio en el futuro
```bash
cd "C:\Users\mauri\OneDrive\Escritorio\Curriculum vitae"
# (editás index.html)
git add -A
git commit -m "update cv"
git push
```
→ Netlify redespliega solo. 🚀

---

## ✅ Alternativa: TODO dentro de Vercel (comprar dominio + deploy)

Sí — Vercel vende dominios. Comprás y publicás en el mismo lugar, y el **DNS + HTTPS quedan
configurados solos** (no tocás ningún registro a mano). Es lo más simple posible.

### 1) Creá tu cuenta y subí el sitio
Entrá a https://vercel.com y registrate (con GitHub o email). Después, elegí UNA forma de subir:

**Opción A — CLI (ya tenés Node):**
```bash
npm i -g vercel
cd "C:\Users\mauri\OneDrive\Escritorio\Curriculum vitae"
vercel          # login la 1ra vez (te abre el navegador) → aceptá los defaults
vercel --prod   # publica a producción
```
Queda online al toque en `https://<algo>.vercel.app`.

**Opción B — Sin instalar nada (dashboard):**
1. https://vercel.com → *Add New… → Project*.
2. Conectá un repo de GitHub **o** arrastrá/subí esta carpeta.
3. Framework preset: **Other** (es estático) → **Deploy**.

### 2) Comprá el dominio en Vercel
1. En el proyecto → **Settings → Domains** (o el menú **Domains** de tu cuenta).
2. Escribí `mauriciolulusiscv.com` en el buscador.
3. Si está disponible aparece **Buy** con el precio (≈ US$15-20/año para `.com`).
   Pagás con tarjeta y **Vercel lo registra a tu nombre**.
4. Al comprarlo ahí, Vercel lo **asigna automáticamente** al proyecto y gestiona el DNS.
   → HTTPS automático, `www` y raíz configurados solos. **Listo, sin DNS manual.** ✅

> Precio: comprar el dominio *dentro* de Vercel es un poco más caro que en un registrador
> al costo (Cloudflare), pero te ahorra toda la configuración de DNS. Si querés lo más barato,
> mirá la alternativa de abajo.

---

## 💸 Alternativa más barata: dominio afuera + apuntar a Vercel

Comprás el dominio en un registrador al costo y cargás 2 registros DNS que Vercel te indica.

| Registrador | Precio .com aprox | Nota |
|---|---|---|
| **Cloudflare Registrar** | ~US$9.15/año | Al costo, WHOIS privacy gratis. **El más barato.** |
| **Namecheap** | ~US$10-12/año | Muy simple. |
| **Porkbun** | ~US$9-11/año | Barato, buena UX. |

Luego en Vercel → **Settings → Domains → Add** → `mauriciolulusiscv.com`. Vercel te muestra
los registros a cargar en el registrador (normalmente **A** `@` → `76.76.21.21` y
**CNAME** `www` → `cname.vercel-dns.com`; usá los que te muestre). Propagación: minutos a ~2 hs.

> `.dev` y `.ai` también quedan muy "AI engineer" (`.ai` es más caro, ~US$60-70/año).

---

## 🟠 Alternativa cero-configuración: Netlify Drop
1. Entrá a https://app.netlify.com/drop
2. **Arrastrá esta carpeta** → queda online en segundos (`<algo>.netlify.app`).
3. *Site settings → Domain management → Add custom domain* → seguí los pasos de DNS.

## 🔵 Alternativa todo-en-uno: Cloudflare Pages
Ideal si comprás el dominio en Cloudflare (DNS ya integrado, no tocás nada a mano).
1. Pages → *Create* → subí la carpeta (o conectá git).
2. *Custom domains → Set up a domain* → elegís tu dominio de Cloudflare → listo.

---

## Notas
- **HTTPS**: automático y gratis en las tres plataformas.
- **El PDF**: el botón "PDF" apunta a `Lulusis Mauricio CV.pdf` (relativo). Asegurate de subir
  ese archivo junto al `index.html`. *(Opcional: renombralo sin espacios, ej. `cv-mauricio-lulusis.pdf`,
  y actualizá el `href` en el `index.html`.)*
- **Actualizar el sitio**: reemplazás `index.html` y volvés a hacer deploy (`vercel --prod`,
  re-drag en Netlify, o push a git si conectaste repo).
- **www vs raíz**: agregá ambos (`mauriciolulusiscv.com` y `www.mauriciolulusiscv.com`) y dejá
  que redirijan a uno solo (la plataforma lo hace por vos).
```

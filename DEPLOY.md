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

## ⭐ Camino que estamos usando: GitHub → Vercel  (RECOMENDADO)

✅ Ya está: el CV está en GitHub → https://github.com/MauricioLulusis/CurriculumVitae (rama `main`).
Con esto, cada `git push` va a redesplegar el sitio en Vercel automáticamente.

### 1) Crear cuenta en Vercel
https://vercel.com → **Sign Up → Continue with GitHub** → autorizá con la cuenta **MauricioLulusis**.

### 2) Importar el repo
1. Dashboard → **Add New… → Project**.
2. En *Import Git Repository* buscá **CurriculumVitae** → **Import**.
   *(Si no aparece: "Adjust GitHub App Permissions" → dale acceso al repo.)*
3. **Framework Preset: Other** · Root Directory: `./` · sin build command.
4. **Deploy** → en ~20s queda online en `https://curriculumvitae-xxxx.vercel.app`.

### 3) Comprar el dominio en Vercel
1. Proyecto → **Settings → Domains**.
2. Escribí `mauriciolulusiscv.com` → si está libre, **Buy** (≈ US$15-20/año).
3. Pagás → Vercel lo registra, lo asigna al proyecto y configura **DNS + HTTPS solos**. ✅

### 4) Actualizar el sitio en el futuro
```bash
cd "C:\Users\mauri\OneDrive\Escritorio\Curriculum vitae"
# (editás index.html)
git add -A
git commit -m "update cv"
git push
```
→ Vercel redespliega solo. 🚀

---

## ✅ Alternativa: TODO dentro de Vercel sin GitHub (comprar dominio + deploy)

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

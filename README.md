# nespace-web

Sitio público de Nespace (landing, planes, descarga del instalador). Estático — HTML/CSS/JS puro, sin build, para que el deploy en GitHub Pages sea directo.

- Contenido y copy tomados de `docs/PRODUCT_SPEC.md` y de la pantalla "Acerca de Nespace" de la app (`src/components/Sistema.tsx`), para que digan lo mismo.
- Marca: assets oficiales copiados de `brand/products/gestion/` (kit "Gestión/ERP"). Tokens de color/tipografía tomados de `brand/tokens.css`.
- Sin precios todavía (a propósito, mismo criterio que la app) y sin datos de contacto inventados (nada de WhatsApp/email placeholder).
- El botón "Descargar" apunta directo al asset del Release (`.../releases/download/v0.1.0/Nespace-Setup-0.1.0.exe`), no a la página de Releases — descarga con un solo clic.
- **Al sacar una versión nueva**: generar el instalador (`npm run dist:win` en el repo principal), crear un Release en GitHub con ese `.exe` adjunto, y actualizar el link de "Descargar" en `index.html` y `gestion.html` a la URL del asset nuevo (`.../releases/download/v<version>/Nespace-Setup-<version>.exe`).

## Publicar en GitHub Pages con dominio propio

Este repo (`soportenespace/nespace`) ya existe. Pasos:

```bash
cd nespace-web
git init
git remote add origin https://github.com/soportenespace/nespace.git
git add -A
git commit -m "Sitio público de Nespace"
git branch -M main
git push -u origin main
```

Después, en GitHub → el repo → **Settings → Pages**:
1. Source: `Deploy from a branch` → rama `main`, carpeta `/ (root)`.
2. Custom domain: `nespace.com.ar` (ya está en el archivo `CNAME` de este directorio, GitHub lo toma solo).
3. Esperar a que el DNS valide y tildar **Enforce HTTPS**.

## DNS (en tu proveedor de dominio, para `nespace.com.ar`)

Para un dominio raíz (apex, sin `www`) apuntando a GitHub Pages, 4 registros A:
```
A   @   185.199.108.153
A   @   185.199.109.153
A   @   185.199.110.153
A   @   185.199.111.153
```
Opcional, si querés que `www.nespace.com.ar` también funcione:
```
CNAME   www   soportenespace.github.io
```
(Verificar esas IPs contra la [documentación oficial de GitHub Pages](https://docs.github.com/pages/configuring-a-custom-domain-for-your-github-pages-site) antes de cargarlas — pueden cambiar.)

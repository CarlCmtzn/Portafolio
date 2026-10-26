# Plantilla Just the Docs

Esta es una **Plantilla de Página o Registro Personal** y cualquiera puede usarla y modificarla para crear la suya propia.
---

## Requisitos

- Cuenta de **GitHub** (gratuita).
- Permiso para usar **GitHub Pages** y **Codespaces** (según tu cuenta/organización).

---

## Inicio rápido: Fork + Codespaces + GitHub Pages

### 1) Copia el repositorio (Fork)

1. Abre el repositorio base (el que te comparte el profesor).
2. Clic en **Fork** → **Create fork**.
3. Revisa que estés en tu repositorio (debe estar bajo tu usuario u organización).

---

### 2) Abre el proyecto en Codespaces (sin instalar nada)

En tu repositorio:

1. Clic en **Code** → pestaña **Codespaces** → **Create codespace on main**.
2. Espera a que cargue VS Code en el navegador.

---

### 3) Configura la URL en `_config.yml` (obligatorio)

Abre `_config.yml` y ajusta:

```yml
url: "https://TU_USUARIO.github.io"
baseurl: "/TU_REPO"
```

Ejemplo:

- Usuario: `ana-ibero`
- Repo: `documentacion-equipo-3`

```yml
url: "https://ana-ibero.github.io"
baseurl: "/documentacion-equipo-3"
```

> Si `baseurl` no coincide con el nombre del repo, los enlaces/estilos pueden fallar.

---

### 4) Haz tu primer cambio y súbelo (Commit + Push)

En Codespaces:

1. Edita un archivo (por ejemplo `index.md`).
2. Abre **Source Control** (ícono de rama).
3. Escribe un mensaje y haz **Commit**.
4. Haz **Sync Changes / Push**.

Flujo esperado: **editar → commit → push → se ejecuta Actions → se publica Pages**.

---

### 5) Activa GitHub Pages (solo una vez)

En GitHub (en tu repositorio):

1. **Settings** → **Pages**
2. **Build and deployment**
   - Source: **Deploy from a branch**
   - Branch: `main`
   - Folder: `/ (root)`
3. Guarda.

Tu URL quedará así:

`https://TU_USUARIO.github.io/TU_REPO/`

---

### 6) Verifica que ya se publicó (Actions)

1. Ve a la pestaña **Actions**.
2. Abre el workflow de Pages (por ejemplo “pages build and deployment”).
3. Espera a que esté en **verde (success)**.
4. Abre la URL desde **Settings → Pages**.

Tip: si no ves cambios, fuerza recarga del navegador (hard refresh):
- Windows: `Ctrl + F5`
- macOS: `Cmd + Shift + R`

---

## Dónde editar y dónde poner archivos

- Contenido (páginas): archivos `*.md` en la raíz del repo.
- Imágenes: `assets/img/`
- PDFs u otros descargables: `assets/files/`
- Videos MP4 (si los usas): `assets/videos/`

---

## En "Guia de Edicion" estara el como puedes editar cada parte del codigo a tus necesidades

- **Guia**: `Guia de Edicion.md`

---

## Personalización rápida (logo/colores/footer)

- Logo: `assets/img/logotipo.png`
- Favicon: `assets/img/favicon.ico`
- CSS: `assets/css/custom.css`
- Head: `_includes/head_custom.html`
- Footer: `_includes/footer_custom.html`

> Recomendación para clase: conserva nombres y rutas, y solo reemplaza los archivos de imagen y los colores del CSS.

---

## Licencia

Define la licencia que usarás para el contenido (por ejemplo **MIT**, **CC BY 4.0**, etc.).  
Este repositorio puede incluir ejemplos de licencia en el footer. Ajusta texto/enlaces según tu política del curso.

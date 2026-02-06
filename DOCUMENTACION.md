# Blog "En tu ciudad" - Documentación Completa

## 📋 Información General

- **Nombre del Blog:** En tu ciudad
- **URL Pública:** https://guidocc.github.io/
- **Repositorio GitHub:** https://github.com/guidocc/guidocc.github.io
- **Generador:** Hugo v0.146.0 Extended
- **Theme:** Ananke
- **Hosting:** GitHub Pages (gratuito)

---

## 🖥️ Configuración de Infraestructura

### Servidor Local (nogales)
- **IP:** 192.168.1.100
- **Sistema Operativo:** Ubuntu 24
- **Usuario:** olaf
- **Ubicación del Proyecto:** `/mnt/data/hugo/en-tu-ciudad`

### MacBook (trabajo)
- **Conexión:** SSH Remote via VS Code
- **Comando de conexión:** `ssh olaf@192.168.1.100`

### GitHub
- **Usuario:** guidocc
- **Email:** guido.cc@gmail.com
- **Autenticación:** SSH (clave ed25519)

---

## 📝 Workflow Completo de Publicación

### 1. Conectarse al servidor desde MacBook

**En VS Code:**
1. `⌘ + Shift + P`
2. Escribir: `Remote-SSH: Connect to Host`
3. Seleccionar: `olaf@192.168.1.100`
4. Abrir carpeta: `/mnt/data/hugo/en-tu-ciudad`

### 2. Iniciar servidor de preview

**En la terminal de VS Code:**
```bash
cd /mnt/data/hugo/en-tu-ciudad
hugo server -D --bind 0.0.0.0
```

**Ver preview en navegador (MacBook):**
```
http://192.168.1.100:1313/
```

**Parámetros importantes:**
- `-D` : Muestra posts en borrador (draft = true)
- `--bind 0.0.0.0` : Permite acceso desde otras máquinas en la red

### 3. Crear un nuevo post
```bash
hugo new content/posts/nombre-del-post.md
```

Esto crea el archivo: `content/posts/nombre-del-post.md`

**Estructura del archivo:**
```markdown
+++
date = '2026-02-06T14:00:00Z'
draft = true
title = 'Título del Post'
+++

Contenido del post en Markdown...
```

### 4. Escribir el contenido

**En VS Code:**
1. Abrir el archivo creado
2. Escribir en Markdown
3. Guardar (`⌘ + S`)
4. Los cambios se ven automáticamente en http://192.168.1.100:1313/

**Cuando el post esté listo para publicar:**
- Cambiar `draft = true` a `draft = false`

### 5. Publicar al sitio online
```bash
# Ver qué archivos cambiaron
git status

# Agregar todos los cambios
git add .

# Crear commit con descripción
git commit -m "Nuevo post: Título del post"

# Subir a GitHub
git push
```

### 6. Verificar publicación

1. Ir a: https://github.com/guidocc/guidocc.github.io/actions
2. Esperar que el workflow termine (check verde ✅)
3. Ver el sitio publicado en: https://guidocc.github.io/

**Tiempo de deployment:** ~1-2 minutos

---

## 🔧 Comandos de Referencia Rápida

### Hugo
```bash
# Iniciar servidor local con borradores
hugo server -D --bind 0.0.0.0

# Crear nuevo post
hugo new content/posts/nombre-del-post.md

# Compilar sitio (genera carpeta public/)
hugo

# Ver versión de Hugo
hugo version
```

### Git
```bash
# Ver estado actual
git status

# Ver historial de commits
git log --oneline

# Agregar archivos
git add .
git add archivo-especifico.md

# Crear commit
git commit -m "Mensaje descriptivo"

# Subir cambios
git push

# Ver cambios en archivos
git diff

# Ver configuración
git config --list
```

### SSH
```bash
# Conectarse a nogales
ssh olaf@192.168.1.100

# Probar conexión con GitHub
ssh -T git@github.com
```

---

## 📁 Estructura del Proyecto
```
/mnt/data/hugo/en-tu-ciudad/
├── .git/                    # Control de versiones
├── .github/
│   └── workflows/
│       └── hugo.yml         # GitHub Actions para deployment
├── .gitignore               # Archivos ignorados por Git
├── .nojekyll                # Deshabilita Jekyll en GitHub Pages
├── archetypes/
│   └── default.md           # Template para nuevos posts
├── content/
│   └── posts/               # Aquí van tus posts
│       └── *.md
├── themes/
│   └── ananke/              # Theme actual
├── hugo.toml                # Configuración principal
├── static/                  # Archivos estáticos (imágenes, CSS, etc.)
├── layouts/                 # Plantillas personalizadas
└── public/                  # Sitio generado (ignorado por Git)
```

---

## ⚙️ Archivo de Configuración (hugo.toml)

**Ubicación:** `/mnt/data/hugo/en-tu-ciudad/hugo.toml`
```toml
baseURL = 'https://guidocc.github.io/'
languageCode = 'es'
title = 'En tu ciudad'
theme = 'ananke'

[params]
  description = 'Blog personal sobre mi ciudad'
  author = 'Olaf'
```

### Parámetros importantes:
- **baseURL:** Debe coincidir exactamente con tu URL de GitHub Pages
- **languageCode:** 'es' para español
- **theme:** Nombre de la carpeta en `themes/`

---

## 🎨 Personalización del Blog

### Cambiar título y descripción
Editar `hugo.toml`:
```toml
title = 'Nuevo título'
[params]
  description = 'Nueva descripción'
```

### Agregar foto de perfil
1. Colocar imagen en: `static/images/perfil.jpg`
2. Editar `hugo.toml`:
```toml
[params]
  featured_image = '/images/perfil.jpg'
```

### Cambiar colores del theme Ananke
Ver documentación: https://github.com/theNewDynamic/gohugo-theme-ananke

---

## 🔍 Solución de Problemas Comunes

### El servidor Hugo no inicia
```bash
# Verificar que estás en el directorio correcto
pwd
# Debería mostrar: /mnt/data/hugo/en-tu-ciudad

# Verificar versión de Hugo
hugo version
```

### Los cambios no se ven en el preview local
1. Verificar que guardaste el archivo (`⌘ + S`)
2. Verificar que el servidor esté corriendo
3. Refrescar el navegador (`⌘ + R`)

### El push a GitHub falla
```bash
# Verificar conexión SSH
ssh -T git@github.com

# Ver errores específicos
git push -v
```

### El deployment falla en GitHub Actions
1. Ir a: https://github.com/guidocc/guidocc.github.io/actions
2. Click en el workflow fallido
3. Revisar logs de error
4. Verificar que `.nojekyll` existe

### No puedo conectarme via SSH desde VS Code
```bash
# Desde terminal del Mac, verificar conexión
ssh olaf@192.168.1.100

# Si funciona, verificar extensión Remote-SSH en VS Code
```

---

## 📱 Accesos Rápidos

### URLs Importantes
- **Blog público:** https://guidocc.github.io/
- **Repositorio:** https://github.com/guidocc/guidocc.github.io
- **Actions (deployments):** https://github.com/guidocc/guidocc.github.io/actions
- **Preview local:** http://192.168.1.100:1313/

### Configuración GitHub
- **SSH Keys:** https://github.com/settings/keys
- **Repositorio Settings:** https://github.com/guidocc/guidocc.github.io/settings
- **GitHub Pages:** https://github.com/guidocc/guidocc.github.io/settings/pages

---

## 🚀 Mejoras Futuras (Opcional)

### 1. Dominio Personalizado
- Comprar dominio (ej: entuciudad.com)
- Configurar DNS
- Actualizar `baseURL` en `hugo.toml`
- Configurar en GitHub Pages Settings

### 2. Cambiar Theme
```bash
# Explorar themes en: https://themes.gohugo.io/
# Descargar theme como submodule
git submodule add URL_DEL_THEME themes/nombre-theme

# Actualizar hugo.toml
theme = 'nombre-theme'
```

### 3. Analytics
- Google Analytics
- Plausible Analytics
- Simple Analytics

### 4. Comentarios
- Disqus
- utterances (basado en GitHub Issues)
- Giscus

### 5. Newsletter
- Mailchimp
- Substack
- Buttondown

---

## 📖 Recursos de Aprendizaje

### Hugo
- **Documentación oficial:** https://gohugo.io/documentation/
- **Guía de inicio rápido:** https://gohugo.io/getting-started/quick-start/
- **Markdown sintaxis:** https://www.markdownguide.org/

### Git & GitHub
- **GitHub Docs:** https://docs.github.com/
- **Git básico:** https://git-scm.com/book/es/v2

### Markdown
- **Guía completa:** https://www.markdownguide.org/
- **Cheat sheet:** https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet

---

## 🆘 Contacto y Soporte

### Si algo no funciona:
1. Revisar esta documentación
2. Verificar logs de GitHub Actions
3. Consultar documentación de Hugo
4. Revisar issues del theme Ananke

### Backup del Proyecto
El repositorio en GitHub sirve como backup automático. Todo está respaldado en:
- https://github.com/guidocc/guidocc.github.io

---

## ✅ Checklist de Mantenimiento

### Semanal
- [ ] Revisar que el sitio esté online
- [ ] Verificar que los deployments automáticos funcionen

### Mensual
- [ ] Revisar actualizaciones de Hugo
- [ ] Revisar actualizaciones del theme
- [ ] Backup local (opcional, GitHub ya lo hace)

### Cuando sea necesario
- [ ] Actualizar Hugo: `sudo snap refresh hugo`
- [ ] Actualizar theme: `git submodule update --remote`

---

## 📅 Historial de Cambios

### 2026-02-06 - Configuración Inicial
- ✅ Hugo instalado en nogales
- ✅ Proyecto creado: "En tu ciudad"
- ✅ Theme Ananke configurado
- ✅ VS Code Remote SSH configurado
- ✅ Repositorio GitHub creado
- ✅ GitHub Actions configurado
- ✅ Sitio publicado en guidocc.github.io
- ✅ Workflow documentado

---

**Última actualización:** 6 de febrero de 2026
**Versión de Hugo:** 0.146.0 Extended
**Mantenido por:** Guido (guidocc)
# 🏗️ ARQUITECTURA — Ecosistema TuSitioYa

**Última actualización:** 11 de julio 2026

Este documento define cómo se organiza TODO el ecosistema de Alexis Ferrada bajo `tusitioya.cl` y sus subdominios.

---

## 📍 MAPA DE DOMINIOS

```
tusitioya.cl/                          ← SITIO PRINCIPAL (todos los productos)
├─ /                                   ← homepage + ecosistema
├─ /seniorclick/                       ← SeniorClick (adultos mayores)
├─ /linkya/                            ← LinkYa (bio-links)
├─ /huellaviva/                        ← HuellaViva (salud)
├─ /menu-express/                      ← Menú Express (cartas digitales)
├─ /qr-express/                        ← QR Express (códigos QR)
├─ /scan/                              ← Scanner PWA (offline)
├─ /iman-clientes/                     ← CRM Imán de Clientes
└─ /clipper-fans/                      ← Clipper Fans (programa de lealtad)

alexis.tusitioya.cl/                   ← PORTAFOLIO PROFESIONAL (Alexis Ferrada)
└─ Portfolio con casos de éxito + CV

djvlex.tusitioya.cl/                   ← DJ VLEX (marca personal)
└─ Sitio del DJ + contacto

turbopos.cl/                           ← TURBOPOS SAAS (dominio separado)
└─ App POS (Django privado)

rucio.tusitioya.cl/                    ← COMMAND CENTER (privado)
└─ Dashboard interno de TuSitioYa
```

---

## 📦 REPOS ACTIVOS

| Repo | Dominio | Tipo | Deploy | Ramas |
|------|---------|------|--------|-------|
| `tusitioya-web` | tusitioya.cl | HTML estático | Cloudflare Pages | main / develop / feature/* |
| `portfolio-alexis` | alexis.tusitioya.cl | HTML estático | Cloudflare Pages | main / develop / feature/* |
| `djvlex-site` | djvlex.tusitioya.cl | HTML estático | Cloudflare Pages | main / develop / feature/* |
| `el-gran-turbopos` | turbopos.cl | Django/Python | Render | main / develop / feature/* |
| `voxmetrics` | (privado) | Python/IA | Local/pre-venta | main / develop / feature/* |

---

## 🔄 GIT WORKFLOW (igual en todos los repos)

### Estructura de ramas
```
main          ← PRODUCCIÓN (lo que ves en vivo)
├─ develop   ← STAGING (lo próximo a liberar)
└─ feature/* ← TRABAJO EN CURSO
```

### Flujo de un cambio
```bash
# 1. Partir desde develop
git checkout develop
git pull origin develop

# 2. Crear rama de feature
git checkout -b feature/mi-cambio

# 3. Hacer cambios, commit, push
git add .
git commit -m "feat: descripción del cambio"
git push origin feature/mi-cambio

# 4. En GitHub: abrir Pull Request (feature → develop)
# 5. Revisar, aprobar, mergear a develop
# 6. Cloudflare Pages hace preview automático

# 7. Cuando esté listo para producción:
git checkout main
git pull origin main
git merge develop
git push origin main
# → Deploy automático a producción
```

### Reglas
- ✅ SIEMPRE hacer cambios en `feature/nombre-corto`
- ✅ NUNCA pusheaa directo a `main` o `develop`
- ✅ NUNCA force push (`git push -f`) sin confirmación
- ❌ NO mezcles múltiples features en una rama
- ❌ NO esperes semanas para mergear; los PRs viejos generan conflictos

---

## 📝 CONVENCIONES DE COMMITS

```
feat: nueva característica (nuevo componente, sección, etc)
fix: corrección de bug
docs: cambios en documentación
style: cambios de CSS/diseño sin lógica
refactor: reorganizar código sin cambiar funcionalidad
chore: actualizaciones de tooling, deps, etc
```

**Ejemplos:**
```
feat: agregar sección de contacto en portfolio
fix: corregir responsive en móvil < 400px
docs: actualizar ARQUITECTURA.md
style: ajustar padding en hero de djvlex
```

---

## 🚀 DEPLOY AUTOMÁTICO

### Cloudflare Pages (tusitioya-web, portfolio-alexis, djvlex-site)
- **main** → deploy a producción en ~30 segundos
- **develop** → preview URL automática (ej: `develop.portfolio-alexis.pages.dev`)
- **feature/*** → preview URL por feature (si lo configuras)

### Render (turbopos.cl)
- Push a `main` → rebuild y deploy automático

---

## 🗂️ ESTRUCTURA DE CARPETAS (repo tusitioya-web)

```
tusitioya-web/
├─ index.html              ← homepage principal
├─ ARQUITECTURA.md         ← este archivo
├─ README.md               ← descripción del proyecto
├─ /css/                   ← estilos globales
├─ /js/                    ← scripts globales
├─ /img/                   ← imágenes compartidas
├─ /seniorclick/
│  ├─ index.html
│  ├─ style.css
│  └─ data.json
├─ /linkya/
├─ /huellaviva/
├─ /menu-express/
├─ /qr-express/
├─ /scan/
├─ /iman-clientes/
└─ /clipper-fans/
```

---

## 🔐 SEGURIDAD & PRIVACIDAD

- ✅ `tusitioya-web`, `portfolio-alexis`, `djvlex-site` → PÚBLICOS (no hay datos sensibles)
- ✅ `el-gran-turbopos` → PRIVADO (código comercial)
- ✅ `voxmetrics` → PRIVADO (en pre-venta)
- ❌ NUNCA commitear `.env`, keys, contraseñas, RUTs

---

## 📞 CONTACTO & PREGUNTAS

Si algo no está claro o necesitas modificar el plan:
- 📧 alexispferrada@gmail.com
- 💬 WhatsApp: +56 9 9126 1916

---

**Última vez modificado:** 11 julio 2026  
**By:** Claude + Alexis Ferrada

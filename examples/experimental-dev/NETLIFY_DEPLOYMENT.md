# Experimental Dev Example - Netlify Deployment Guide

## 🚀 Deployment Vorbereitung

Dieses Projekt ist für **Netlify Deployment** optimiert. Folgende Konfigurationen sind bereits eingerichtet:

### 📋 Konfigurierte Dateien

- **`netlify.toml`** - Vollständige Netlify-Build-Konfiguration mit:
  - Monorepo-Support (Monorepository)
  - Caching für schnellere Rebuilds
  - Node.js 22.11.0 (LTS)
  - Optimierte Memory-Limits für große Builds
  - Verschiedene Deploy-Kontexte (Production, Preview, Branch)
  - Automatisches Rebuild-Skip bei irrelevanten Dateänderungen

- **`.nvmrc`** - Spezifiziert Node.js Version 22.11.0
- **`.netlifyignore`** - Schließt unnötige Dateien vom Deployment aus

### 🔧 Environment-Variablen für Netlify

In der **Netlify UI** sollten folgende Environment-Variablen gesetzt werden:

```
NODE_ENV = production
USE_EXPERIMENTAL_DEPENDENCIES = true
USE_REACT_COMPILER = false (optional)
```

Falls eine externe Datenbank verwendet wird:
```
DATABASE_CLIENT = better-sqlite3 (oder postgresql, mysql)
DATABASE_HOST = [your-database-host]
DATABASE_PORT = [your-database-port]
DATABASE_NAME = [your-database-name]
DATABASE_USERNAME = [your-database-user]
DATABASE_PASSWORD = [your-database-password]
```

### 🏗️ Build-Prozess

Der Build läuft in dieser Reihenfolge:

1. **Monorepo Build**: `yarn --cwd ../.. build:code`
   - Kompiliert alle Packages im Monorepo
   - Generiert `dist/cli` und andere erforderliche Module
   - Timeout: 30 Minuten

2. **Example Build**: `yarn --cwd . build`
   - Buildet das Strapi-Admin-Interface
   - Erstellt optimierte Produktions-Assets
   - Output-Folder: `/dist`

### ⚡ Performance-Optimierungen

- **Yarn Caching**: node_modules und .yarn/cache werden gecacht
- **Smarte Rebuild Detection**: Skipped Rebuilds bei Änderungen in:
  - Documentation (`docs/`)
  - Tests (`tests/`)
  - CI/CD-Dateien (`.github/`)
  - Markdown-Dateien (`*.md`)

### 📊 Deploy Preview & Branch Deploys

Alle Kontexte (Production, Deploy Preview, Branch Deploy) verwenden die gleiche Build-Konfiguration für Konsistenz.

### 🔐 Production-Tipps

1. **SSL/TLS**: Netlify stellt automatisch kostenloses SSL-Zertifikat bereit
2. **Custom Domain**: Verbindet eure Domain über Netlify DNS
3. **Rollback**: Netlify speichert Deploy-History für einfaches Rollback
4. **CDN**: Alle Assets werden automatisch über Netlify CDN bereitgestellt

### 📝 Troubleshooting

Falls der Build fehlschlägt:

- ✅ **Check Node Version**: `node -v` sollte >= 22.0.0 sein
- ✅ **Clear Cache**: Netlify UI → Site Settings → Delete site data
- ✅ **Check Logs**: Netlify Deployment Logs für détails
- ✅ **Rebuild**: Trigger manual rebuild in Netlify UI

### 🎯 Nächste Schritte

1. Verbindet das Git-Repository mit Netlify
2. Setzt notwendige Environment-Variablen in Netlify UI
3. Triggert den ersten Deploy
4. Monitort die Deployment-Logs

---

**Deploy Status Badge**: Kommt bald! 🚀

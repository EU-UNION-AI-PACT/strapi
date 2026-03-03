# Netlify Deployment Checkliste - experimental-dev Example

## ✅ Vorbereitung

### Git Repository
- [ ] Repository ist auf GitHub/GitLab/Bitbucket
- [ ] Main/Master Branch ist aktuell
- [ ] Alle wichtigen Commits sind pushed

### Environment-Variablen (Netlify UI)
- [ ] `NODE_ENV = production`
- [ ] `USE_EXPERIMENTAL_DEPENDENCIES = true`
- [ ] Database URLs configured (falls erforderlich)
- [ ] API Keys und Secrets sind secure gespeichert

### Dateien & Konfiguration
- [ ] `netlify.toml` existiert und ist korrekt ✅
- [ ] `.nvmrc` spezifiziert Node.js Version ✅
- [ ] `.netlifyignore` ist konfiguriert ✅
- [ ] `NETLIFY_DEPLOYMENT.md` gelesen ✅

## 🔧 Build & Deploy

### 1. Netlify Site verbinden
```bash
# Option A: CLI
npm install -g netlify-cli
netlify init

# Option B: Web UI
# https://app.netlify.com/ → "Connect to Git" → Repo wählen
```

### 2. Build-Einstellungen konfigurieren
In Netlify UI unter "Site Settings":
- **Base directory**: `examples/experimental-dev`
- **Build command**: (automatisch aus netlify.toml)
- **Publish directory**: `dist`

### 3. Environment-Variablen setzen
Site Settings → Build & deploy → Environment:
```
NODE_ENV = production
USE_EXPERIMENTAL_DEPENDENCIES = true
```

### 4. Deploy triggern
```bash
# Via CLI
netlify deploy

# Oder: Automatisch bei Git Push
# (konfiguriert in "Deploy Settings")
```

## 📊 Monitoring & Testing

### Nach dem Deploy:
- [ ] Deploy Status ist "published"
- [ ] Netlify Preview URL lädt
- [ ] Keine Build-Fehler in Deployment Logs
- [ ] Admin Interface (`/admin`) ist erreichbar
- [ ] Database Connection funktioniert
- [ ] API-Endpoints antworten korrekt

### Performance-Checks:
```bash
# Lighthouse Score prüfen
# Chrome DevTools → Lighthouse Tab

# Network-Performance:
# Deployment sollte < 3-5 Minuten dauern
```

## 🚨 Troubleshooting

### Build schlägt fehl mit "Cannot find module"
✅ **Lösung**: netlify.toml hat `yarn --cwd ../.. build:code` - das ist korrekt!

### Timeout während Build
- Erhöhe Node Memory: `NODE_OPTIONS = --max-old-space-size=4096` ✅ (bereits konfiguriert)
- Prüfe größere Dependencies

### Database verbindet sich nicht
- Environment-Variable `DATABASE_* ` richtig gesetzt?
- Database ist online & erreichbar von Netlify?

### Yarn/npm Cache-Probleme
- Nautilty UI → Site Settings → Delete site data
- Manueller Rebuild triggern

## 💡 Optimierungstipps

### Für bessere Build-Performance:
1. **Yarn Workspaces Caching**: ✅ Aktiv (netlify.toml)
2. **Skip irrelevante Rebuilds**: ✅ Aktiv (.netlifyignore)
3. **Memory Optimization**: ✅ NODE_OPTIONS gesetzt
4. **Parallele Builds**: Verwende `nx run-many` für schnellere Builds

### Für bessere Runtime-Performance:
1. **CDN Caching**: Aktivore in Netlify UI
2. **Asset Compression**: Automatisch aktiviert
3. **HTTP/2 Push**: Automatisch aktiviert
4. **Lambda Functions**: Falls APIs umgelagert werden können

## 📚 Helpful Links

- [Netlify Documentation](https://docs.netlify.com/)
- [Strapi Deployment Guide](https://docs.strapi.io/dev-docs/deployment)
- [Netlify Build Settings](https://docs.netlify.com/configure-builds/overview/)
- [Environment Variables](https://docs.netlify.com/configure-builds/environment-variables/)

## 🎯 Support

- **Netlify Support**: https://support.netlify.com/
- **Strapi Community**: https://strapi.io/community
- **GitHub Issues**: Für projekt-spezifische Issues

---

**Letzte Aktualisierung**: März 2026
**Status**: ✅ Bereit für Netlify Deployment

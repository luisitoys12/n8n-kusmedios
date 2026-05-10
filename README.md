# n8n Kusmedios — Deploy en Fly.io

## Specs
- 🖥️ RAM: 2 GB
- 💾 Volumen persistente: 10 GB
- 🌎 Región: Dallas (más cercana a Irapuato)
- ⚡ URL: https://n8n-kusmedios.fly.dev

---

## Deploy completo en 4 pasos

### 0. Instalar flyctl (si no lo tienes)
```bash
curl -L https://fly.io/install.sh | sh
```

---

### 1. Login en Fly.io
```bash
fly auth login
```
(Abre el navegador — entra con tu cuenta de estacionkusmedios)

---

### 2. Crear la app y el volumen
```bash
# Clonar este repo
git clone https://github.com/luisitoys12/n8n-kusmedios.git
cd n8n-kusmedios

# Crear la app en tu org
fly apps create n8n-kusmedios --org estacionkus-medios

# Crear volumen de 10 GB persistente
fly volumes create n8n_data \
  --app n8n-kusmedios \
  --region dfw \
  --size 10
```

---

### 3. Configurar secrets (usuario y password de n8n)
```bash
fly secrets set \
  N8N_BASIC_AUTH_ACTIVE=true \
  N8N_BASIC_AUTH_USER=admin \
  N8N_BASIC_AUTH_PASSWORD=Kusmedios2026! \
  --app n8n-kusmedios
```

---

### 4. Deploy 🚀
```bash
fly deploy --app n8n-kusmedios
```

**Listo! En ~3 minutos tu n8n estará corriendo en:**
https://n8n-kusmedios.fly.dev

Usuario: `admin`
Password: `Kusmedios2026!`

---

## Después del deploy — Configurar OpenRouter

En n8n → Credenciales → Nueva credencial → tipo **OpenAI API**:

| Campo | Valor |
|---|---|
| Nombre | OpenRouter Kusmedios |
| Base URL | https://openrouter.ai/api/v1 |
| API Key | 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 |

---

## Webhook para Facebook
```
URL: https://n8n-kusmedios.fly.dev/webhook/kusmedios-cm
Verify Token: kusmedios2026
```

---

## Monitorear y gestionar
```bash
# Ver logs en vivo
fly logs --app n8n-kusmedios

# Ver estado
fly status --app n8n-kusmedios

# Reiniciar si se cae
fly machine restart --app n8n-kusmedios

# Ver uso de disco
fly volumes list --app n8n-kusmedios
```

---

## Costo estimado
- VM (2 CPU shared, 2GB RAM): ~$10-15 USD/mes
- Volumen 10 GB: ~$1.50 USD/mes
- **Total: ~$12-17 USD/mes (~240-340 MXN)**

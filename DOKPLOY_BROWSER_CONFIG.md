# 🔧 Полная конфигурация для Dokploy

## ✅ **Добавьте эти переменные в Dokploy Environment:**

```env
# === LLM КОНФИГУРАЦИЯ ===
DEFAULT_LLM=openai
OPENAI_API_KEY=ваш_openai_ключ
OPENAI_ENDPOINT=https://api.openai.com/v1

# === ОСНОВНЫЕ НАСТРОЙКИ ===
NODE_ENV=production
PORT=7788
ENV_RESOLUTION=1280x720x24
ENV_VNC_PASSWORD=ваш_пароль_vnc

# === БРАУЗЕР НАСТРОЙКИ (Docker) ===
USE_OWN_BROWSER=false
KEEP_BROWSER_OPEN=true
BROWSER_DEBUGGING_PORT=9222
BROWSER_DEBUGGING_HOST=0.0.0.0

# === ДОПОЛНИТЕЛЬНЫЕ НАСТРОЙКИ ===
BROWSER_USE_LOGGING_LEVEL=info
ANONYMIZED_TELEMETRY=false
DISPLAY=:99

# === БЕЗОПАСНОСТЬ ===
BROWSER_USER_DATA=
```

## ❌ **НЕ добавляйте эти настройки:**

```env
# ⚠️ Эти настройки только для локальной разработки:
# BROWSER_PATH=/Applications/Google Chrome.app/Contents/MacOS/Google Chrome
```

## 🔍 **Объяснение:**

- **`USE_OWN_BROWSER=false`** - использовать встроенные браузеры Playwright
- **`BROWSER_DEBUGGING_HOST=0.0.0.0`** - разрешить подключения извне контейнера
- **Пустой `BROWSER_PATH`** - позволяет Playwright автоматически найти браузер

## 🚀 **После обновления:**

1. **Redeploy** в Dokploy
2. В логах должно появиться:
   ```
   ✅ Browser initialized successfully
   ✅ Agent starting task
   ```
3. **VNC интерфейс** (порт 6080) покажет реальный браузер в действии!

## 🎯 **Результат:**
- Агент сможет открыть браузер
- LinkedIn автоматизация заработает
- Все задачи будут выполняться через встроенный Chrome 
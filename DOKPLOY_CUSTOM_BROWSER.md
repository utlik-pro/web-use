# 🚀 Конфигурация для использования СВОЕГО браузера в Dokploy

## ✅ **Переменные окружения для Dokploy:**

### **Вариант 1: Использовать установленный Chromium**
```env
# === БРАУЗЕР НАСТРОЙКИ (свой браузер) ===
USE_OWN_BROWSER=true
BROWSER_PATH=/ms-browsers/chromium-*/chrome-linux/chrome
BROWSER_USER_DATA=/tmp/chrome-user-data
KEEP_BROWSER_OPEN=true
BROWSER_DEBUGGING_PORT=9222
BROWSER_DEBUGGING_HOST=0.0.0.0

# === LLM И ОСНОВНЫЕ НАСТРОЙКИ ===
DEFAULT_LLM=openai
OPENAI_API_KEY=ваш_openai_ключ
OPENAI_ENDPOINT=https://api.openai.com/v1
NODE_ENV=production
PORT=7788
ENV_RESOLUTION=1280x720x24
ENV_VNC_PASSWORD=ваш_пароль_vnc

# === ДОПОЛНИТЕЛЬНЫЕ ===
BROWSER_USE_LOGGING_LEVEL=info
ANONYMIZED_TELEMETRY=false
DISPLAY=:99
```

### **Вариант 2: Автопоиск браузера Playwright**
```env
# === БРАУЗЕР НАСТРОЙКИ (автопоиск) ===
USE_OWN_BROWSER=true
BROWSER_PATH=auto
BROWSER_USER_DATA=/tmp/chrome-user-data
PLAYWRIGHT_BROWSERS_PATH=/ms-browsers
KEEP_BROWSER_OPEN=true
BROWSER_DEBUGGING_PORT=9222
BROWSER_DEBUGGING_HOST=0.0.0.0
```

## 🔧 **Объяснение настроек:**

- **`USE_OWN_BROWSER=true`** - включает использование своего браузера
- **`BROWSER_PATH=/ms-browsers/chromium-*/chrome-linux/chrome`** - путь к Chromium в контейнере
- **`BROWSER_USER_DATA=/tmp/chrome-user-data`** - временная папка для профиля браузера
- **`BROWSER_DEBUGGING_HOST=0.0.0.0`** - разрешает подключения извне контейнера

## 🎯 **Преимущества использования своего браузера:**

✅ **Больше контроля** над поведением браузера  
✅ **Можно настроить расширения** и профили  
✅ **Лучшая совместимость** с некоторыми сайтами  
✅ **Видимость в VNC** - можете наблюдать работу браузера  

## 🚀 **После обновления:**

1. **Redeploy** в Dokploy
2. В логах должно появиться:
   ```
   ✅ Using custom browser at: /ms-browsers/chromium-*/chrome-linux/chrome
   ✅ Browser debugging enabled on port 9222
   ```
3. **VNC интерфейс** покажет ваш настроенный браузер!

## 📋 **Отладка:**

Если браузер не найден, попробуйте Вариант 2 с `BROWSER_PATH=auto` 
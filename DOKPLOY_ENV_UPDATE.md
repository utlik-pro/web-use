# 🔧 Обновление переменных окружения в Dokploy

## ⚠️ Проблемы найдены:

1. **noVNC путь исправлен** ✅
2. **DeepSeek модель не поддерживает tool use** ❌

## 📝 Обновите переменные окружения в Dokploy:

### **Замените или добавьте:**

```env
# === LLM КОНФИГУРАЦИЯ ===
DEFAULT_LLM=openai
OPENAI_API_KEY=ваш_openai_ключ
OPENAI_ENDPOINT=https://api.openai.com/v1

# Убрать или закомментировать DeepSeek если используется:
# DEEPSEEK_API_KEY=
# DEEPSEEK_ENDPOINT=

# === ОСНОВНЫЕ НАСТРОЙКИ ===
NODE_ENV=production
PORT=7788
ENV_RESOLUTION=1280x720x24
ENV_VNC_PASSWORD=ваш_пароль_vnc

# === БРАУЗЕР НАСТРОЙКИ ===
BROWSER_USE_LOGGING_LEVEL=info
ANONYMIZED_TELEMETRY=false
KEEP_BROWSER_OPEN=true
USE_OWN_BROWSER=false
```

## 🚀 После обновления переменных:

1. **Redeploy** приложение в Dokploy
2. Проверьте логи - должны исчезнуть ошибки:
   - ✅ noVNC запустится без ошибок
   - ✅ Agent будет использовать OpenAI вместо DeepSeek
   - ✅ Tool use будет работать

## 🎯 Результат:

- **Веб-интерфейс**: http://ваш-домен:7788
- **VNC браузер**: http://ваш-домен:6080
- **Рабочий AI агент** с поддержкой инструментов 
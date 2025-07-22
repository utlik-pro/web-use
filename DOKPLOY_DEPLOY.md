# 🚀 Развертывание Browser Use Web UI на Dokploy

## Предварительные требования

1. **Dokploy server** установлен и запущен
2. **Git репозиторий** с этим кодом (GitHub, GitLab, etc.)
3. **API ключи** для LLM провайдеров (OpenAI, Anthropic, etc.)

## 📋 Пошаговая инструкция

### Шаг 1: Подготовка репозитория

1. Загрузите код в ваш Git репозиторий (GitHub/GitLab)
2. Убедитесь, что файлы `Dockerfile` и `docker-compose.yml` присутствуют

### Шаг 2: Создание приложения в Dokploy

1. Откройте ваш Dokploy dashboard
2. Нажмите **"Создать новое приложение"**
3. Выберите тип: **"Docker Compose"**
4. Укажите ссылку на ваш Git репозиторий

### Шаг 3: Настройка переменных окружения

В настройках приложения добавьте следующие переменные:

#### Обязательные переменные:
```env
OPENAI_API_KEY=ваш_ключ_openai
ANTHROPIC_API_KEY=ваш_ключ_anthropic  
GOOGLE_API_KEY=ваш_ключ_google
DEFAULT_LLM=openai
VNC_PASSWORD=ваш_безопасный_пароль
```

#### Дополнительные переменные (по желанию):
```env
DEEPSEEK_API_KEY=ваш_ключ_deepseek
MISTRAL_API_KEY=ваш_ключ_mistral
ANONYMIZED_TELEMETRY=false
BROWSER_USE_LOGGING_LEVEL=info
RESOLUTION_WIDTH=1920
RESOLUTION_HEIGHT=1080
```

### Шаг 4: Настройка портов

Dokploy автоматически откроет порты из docker-compose.yml:

- **7788** - Основной веб-интерфейс 🌐
- **6080** - noVNC веб-интерфейс 🖥️ 
- **5901** - VNC сервер
- **9222** - Chrome debugging port

### Шаг 5: Настройка ресурсов

Рекомендуемые настройки:
- **RAM**: минимум 2GB, рекомендуется 4GB
- **CPU**: минимум 1 core, рекомендуется 2 cores
- **Disk**: минимум 5GB

### Шаг 6: Развертывание

1. Нажмите **"Deploy"** в Dokploy
2. Дождитесь завершения сборки (это может занять 10-15 минут при первом запуске)
3. Проверьте логи на наличие ошибок

## 🔗 Доступ к приложению

После успешного развертывания:

### Основной интерфейс:
```
https://ваш-домен:7788
```

### VNC интерфейс для просмотра браузера:
```
https://ваш-домен:6080
```
Пароль: тот, что указали в `VNC_PASSWORD`

## 🔧 Дополнительная настройка

### Настройка домена

1. В Dokploy перейдите в настройки приложения
2. Добавьте ваш домен для порта 7788
3. Настройте SSL сертификат (Let's Encrypt)

### Настройка обратного прокси

Если используете собственный прокси, настройте:
```nginx
server {
    listen 80;
    server_name ваш-домен.com;
    
    location / {
        proxy_pass http://localhost:7788;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
    
    # Для WebSocket соединений
    location /ws {
        proxy_pass http://localhost:7788;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "upgrade";
    }
}
```

## 🐛 Устранение неполадок

### Проблема: Контейнер не запускается
**Решение:** Проверьте логи в Dokploy dashboard, возможно не хватает ресурсов

### Проблема: Браузер не отображается
**Решение:** 
1. Проверьте доступность порта 6080
2. Убедитесь, что VNC_PASSWORD установлен
3. Проверьте переменную DISPLAY=:99

### Проблема: LLM не отвечает
**Решение:**
1. Проверьте правильность API ключей
2. Убедитесь, что DEFAULT_LLM соответствует настроенному провайдеру

## 📚 Полезные команды

### Просмотр логов:
```bash
docker logs имя_контейнера
```

### Перезапуск приложения:
Используйте кнопку "Restart" в Dokploy dashboard

### Обновление кода:
1. Push изменения в Git репозиторий
2. В Dokploy нажмите "Redeploy"

## 💡 Советы по безопасности

1. **Используйте сильные пароли** для VNC
2. **Ограничьте доступ** к портам VNC (5901) и debugging (9222)
3. **Регулярно обновляйте** API ключи
4. **Настройте мониторинг** ресурсов

---

## 🆘 Поддержка

Если возникли проблемы:
1. Проверьте [документацию Browser Use](https://docs.browser-use.com/)
2. Создайте issue в репозитории проекта
3. Обратитесь к сообществу Dokploy 
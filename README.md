# Sausage Store Project (Semester 2)

📦 **Проект: Сосисочная**  
🧑‍🎓 *Выполнен в рамках второго семестра по курсу Cloud Services Engineer.*

---

## 📋 Состав проекта

Микросервисная система, включающая:

- **Backend** — Java Spring Boot, работа с PostgreSQL, миграции Flyway
- **Backend-report** — Go-приложение для отчетов, работает с MongoDB
- **Frontend** — Angular SPA, деплой через Nginx
- **Infra** — Helm-чарт для PostgreSQL и MongoDB

---

## 🚀 Запуск в Kubernetes

Проект разворачивается с помощью Helm-чарта `sausage-store-chart`, включающего 4 компонента:

- `backend`
- `backend-report`
- `frontend`
- `infra` (PostgreSQL, MongoDB)

### Установка:

```bash
helm install sausage-store ./sausage-store-chart
```

Для удаления:

```bash
helm uninstall sausage-store
```

---

## 📦 Vault

В проект интегрирован HashiCorp Vault:

- Используется `spring.config.import=vault://...` (Config Data API)
- Чувствительные данные (`username`, `password`, `mongodb.uri`) хранятся в Vault
- `application.properties` не содержит паролей напрямую

---

## 📊 Автоматическое масштабирование и мониторинг

- `backend` использует **VerticalPodAutoscaler**
- `backend-report` — **HorizontalPodAutoscaler**
- `LivenessProbe` реализована для обоих приложений
- Настроены `resources.requests` и `resources.limits`

---

## ⚙️ CI/CD и Helm

- Присутствует `Chart.yaml` и `values.yaml`
- Поддержка `helm lint` и `helm install`
- Helm-чарт публикуется в Nexus (`helm(hosted)`, `Allow redeploy`)
- Используются шаблоны `{{ .Values }}`, `{{ .Release.Name }}` и др.

---

## 🧪 Проверка

- Все Dockerfile'ы проходят сборку
- Миграции Flyway выполняются корректно
- Приложение разворачивается в Kubernetes
- Фронтенд отображает список сосисок, можно оформить заказ



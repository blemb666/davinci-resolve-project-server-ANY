# davinci-resolve-project-server-ANY
Install davinci server of any version on LINUX/Debian/Ubuntu
# DaVinci Resolve Project Server в Docker

Этот проект позволяет легко развернуть **DaVinci Resolve Project Server (PostgreSQL)** на Linux-сервере с помощью **Docker** и **docker-compose**. Этот гайд написан специально для новичков, монтажёров и тех, кто хочет быстро и без мучений развернуть сервер проектов.

---

# 🚀 Возможности

* Полностью готовый PostgreSQL-сервер для DaVinci Resolve
* Веб-интерфейс **pgAdmin** для управления базой
* Автоматический запуск контейнеров
* Простая настройка и инструкция «от А до Я»

---

# 🧩 1. Требования

Перед установкой убедитесь, что у вас есть:

* Linux (Ubuntu / Debian / любой другой с systemd)
* root-доступ
* internet connection

---

# 🐳 2. Установка Docker

Запустите команды:

```bash
sudo apt update
sudo apt install -y ca-certificates curl gnupg
```

Добавляем ключ Docker:

```bash
sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo tee /etc/apt/keyrings/docker.asc > /dev/null
sudo chmod a+r /etc/apt/keyrings/docker.asc
```

Добавляем репозиторий:

```bash
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

Устанавливаем Docker:

```bash
sudo apt update
sudo apt install -y docker-ce docker-ce-cli containerd.io
```

Проверяем:

```bash
docker --version
```

---

# 📦 3. Установка Docker Compose

```bash
sudo apt install docker-compose -y
```

Проверка:

```bash
docker-compose --version
```

---

# 📁 4. Скачивание репозитория

```bash
git clone https://github.com/blemb666/davinci-resolve-project-server-ANY.git
cd davinci-resolve-project-server-ANY
```

---

# ⚙️ 5. Проверка, что порт 5432 свободен

DaVinci Resolve Project Server использует порт 5432.
Проверяем:

```bash
sudo lsof -i :5432
```

Если там есть процесс **postgres**, остановите системный PostgreSQL:

```bash
sudo systemctl stop postgresql
sudo systemctl disable postgresql
```

---

# ▶️ 6. Запуск сервера

Запускаем контейнеры:

```bash
docker-compose up -d
```

Проверяем статус:

```bash
docker ps
```

Контейнеры должны быть:

* **dr_postgres** — база для DaVinci Resolve
* **dr_pgadmin** — панель управления

---

# 🌐 7. Доступ к pgAdmin

Открываем в браузере:

```
http://IP_СЕРВЕРА:8080
```

Авторизация:

* Email: **[admin@admin.com](mailto:admin@admin.com)**
* Password: **admin**

Добавляем сервер:

* Name: `DaVinci`
* Host: `postgres`
* Port: `5432`
* User: `postgres`
* Password: `DaVinci`

---

# 🎬 8. Подключение DaVinci Resolve к серверу

Открыть:
**DaVinci Resolve → Project Manager → Connect → PostgreSQL**

Данные подключения:

* Host: `IP_СЕРВЕРА`
* User: `postgres`
* Password: `DaVinci`
* Database: `resolve_db`
* Port: `5432`

Нажать **Connect**.

---

# 🔧 9. Полезные команды

Посмотреть логи:

```bash
docker logs dr_postgres
```

Перезапустить контейнеры:

```bash
docker-compose restart
```

Остановить:

```bash
docker-compose down
```

---

# 🧹 10. Резервное копирование базы

Зайти в pgAdmin → выбрать базу → **Backup**.

---

# ✔️ Готово!

Ваш DaVinci Resolve Project Server полностью настроен и готов к работе.

Если нужно — могу создать версию инструкции под:

* Windows + WSL
* macOS
* Docker Swarm или Kubernetes
* Авто-бэкапы

Пиши — помогу!

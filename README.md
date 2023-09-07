# Контейнер для разработки на С\С++

## Сборка и использование контейнера без vscode
### 0. Подготовка
- Раскоментировать соответсвующие строки в файле **.devcontainer/docker-compose_develop.yaml**, которые соответсвуют сборке без vscode

- Указать в *.env* параметры пользователя от которого будет произведена разработка **UID, GID, USER_NAME, USER_PASSWORD**, а также директорию для разработки **DEV_FOLDER** она будет создана по пути **/home/USER_NAME/DEV_FOLDER** туда же будет скопирован исходный код приложения (корень).
- Для подключения необходимо сгенерировать ключи на своей машине с наименованием **auth_key** и положить публичный ключ (**auth_key.pub**) в директорию *.devcontainer/ssh_keys*, предварительно создав директорию *.devcontainer/ssh_keys*. (Она будет добавлена в .gitignore)
- Для проброса git user/email (**GIT_USER** = user
**GIT_EMAIL** = user@mail.ru) и иных приватных переменных окружения, которые не должны быть в репозитории, по умолчанию используется *.devcontainer/.env_secret*
 
### 1. Сборка
```bash
docker-compose --env-file .env --env-file .devcontainer/.env_secret -f docker-compose.yaml -f .devcontainer/docker-compose_develop.yaml build --no-cache
```

### 2. Запуск контейнера
```bash
docker-compose --env-file .env --env-file .devcontainer/.env_secret -f docker-compose.yaml -f .devcontainer/docker-compose_develop.yaml up -d
```

### 3. Подключение к контейнеру (не использовать в проде)

```bash
ssh -o StrictHostKeyChecking=no -o UserKnownHostsFile=/dev/null -A user@localhost -p 2222
```
## Сборка и использование контейнера c vscode
### 1. Открыть папку через vscode и выбрать *reopen in container*:)
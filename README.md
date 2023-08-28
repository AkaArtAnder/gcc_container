# Контейнер для разработки на С\С++

## Сборка и использование контейнера без vscode
### 0. Подготовка
- Раскоментировать соответсвующие строки в файле **.devcontainer/docker-compose_develop.yaml**, которые соответсвуют сборке без vscode

- Указать в compose параметры пользователя от которого будет произведена разработка **UID, GID, USER_NAME, USER_PASSWORD**, а также директорию для разработки **DEV_FOLDER** она будет создана по пути **/home/USER_NAME/DEV_FOLDER** туда же будет скопирован исходный код приложения. Папка с исходным кодом на компьютере должна иметь идентичное название **DEV_FOLDER** и находиться в корне.
### 1. Сборка
```bash
docker-compose -f docker-compose.yaml -f .devcontainer/docker-compose_develop.yaml build --no-cache
```
### 2. Запуск контейнера
```bash
 docker-compose -f docker-compose.yaml -f .devcontainer/docker-compose_develop.yaml up -d
```

### 3. Подключение к контейнеру
Подключение к контейнеру организованно по ssh для созданного пользователя
# Пример
```bash
ssh -p 2222 user@localhost
```

При первом подключении будет сгенерирована пара ssh ключей. 

# Внимание!
Если пересобрать контейнер, то пара ключей перестанет быть валидной и вы не сможете войти по ssh, для устранения ошибки необходимо на своей машине удалить ключ, находящийся в файле **kwon_hosts (Пример: /home/user/.ssh/known_hosts)**. После этой операции подключение к контейнеру по ssh будет разрешено (сгенерируется новая пара ключей)

# Пока не разобрался как можно перегенерировать на лету без боли СОРИ

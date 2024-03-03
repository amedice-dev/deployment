### Подготовка
Создать тома:
```shell
docker volume create pg_data_vol &&
docker volume create staticfiles_vol &&
docker volume create mediafiles_vol
```

### Развертывание проекта

Запуск:
```shell
docker-compose up -d --build
```

После запуска подключаемся к контейнеру backend:
```shell
docker exec -it <полное_название_контейнера> /bin/bash
```

Статические файлы:

```shell
python manage.py collectstatic --noinput --clear
```

Миграции:

```shell
python manage.py migrate
```


### Очистка всех данных Docker

Чтобы полностью очистить все данные Docker, нужно выполнить следующие шаги:

1. **Остановка всех контейнеров Docker:**
   ```
   docker stop $(docker ps -a -q)
   ```

2. **Удаление всех контейнеров Docker:**
   ```
   docker rm $(docker ps -a -q)
   ```

3. **Удаление всех образов Docker:**
   ```
   docker rmi $(docker images -a -q)
   ```

4. **Удаление всех сетей Docker:**
   ```
   docker network prune -f
   ```

5. **Удаление всех томов Docker:**
   ```
   docker volume prune -f
   ```

6. **Очистка всего остального мусора Docker:**
   ```
   docker system prune -a --volumes --force
   ```
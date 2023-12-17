# one-click-own-free-proxy

Шаблон для запуска бесплатного иностранного SOCKS5 прокси yна базе [chisel](https://github.com/jpillora/chisel) с использованием [Render](https://render.com)


## Начало работы
0. Форкните этот репозиторий.
1. Установите клиент [chisel](https://github.com/jpillora/chisel) 
2. Опубликуйте сервер на Render.com
Для этого: [зарегистрируйтесь](https://dashboard.render.com/register) в сервисе (поддерживается также авторизация через Github)

3. Создайте новый [Blueprint проект](https://dashboard.render.com/select-repo?type=blueprint)

В процессе сервис запросит вас выдать доступ к репозиториям Github

Достаточно выбрать ваш форк.

В результате он должен появиться в списке репозиториев для подключения (Connect a repository). Нажмите коннект и заполните значение переменной `AUTH` в формате `логин:пароль`, например `user:password` и нажмите "Create New Resources".

Дождитесь создания сервера и скопируйте его url (вида https://something.onrender.com) 

4. Подключитесь к  серверу (без docker)
```
chisel client --keepalive 10s --auth user:pass <ваш_url_здесь> socks
```

Вместо https://shrouded-springs-35880.render.com укажите url отдеплоенного сервера

Вариант с Docker доступен в директории `client`. Обратите внимание на содержимое .env.client.example


4. Проверьте работу прокси:
```bash
curl --socks5 127.0.0.1:1080 ifconfig.co
```
В результате вы увидите IP прокси.

5. Укажите `127.0.0.1:1080` в качестве SOCKS5 прокси в вышем приложении, например в конфиге Docker для обхода ограничений на доступ к dockerhub 
из рф.
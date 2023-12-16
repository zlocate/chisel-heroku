# one-click-own-free-proxy

Шаблон для запуска собственного SOCKS5 прокси yна базе [chisel](https://github.com/jpillora/chisel) с использованием [Render](https://render.com) (бесплатно) или [Heroku](https://www.heroku.com/).

## Начало работы

1. Установите клиент [chisel](https://github.com/jpillora/chisel) 

2. Опубликуйте сервер

Выберите один из вариантов деплоя ниже:

<div>
<a href="https://render.com/deploy?repo=https://github.com/zlocate/one-click-own-free-proxy">
  <img src="https://render.com/images/deploy-to-render-button.svg" height="32" alt="Deploy to Render">
</a>

<a href="https://heroku.com/deploy">
  <img src="https://www.herokucdn.com/deploy/button.svg" alt="Heroku Deploy">
</a>
</div>

При создании сервера /  серверов укажите значение переменной AUTH - в ней хранится секретный ключ для подключения к прокси
 
Или создайте приложение вручную:

<div><details>
<summary>Heroku</summary>
Для корректной работы скрипта необходим установленный render сli. 
Не забудьте авторизоваться в cli перед выполнением команды


```bash
heroku create
heroku stack:set container
heroku config:set CHISEL_AUTH=user:pass
git push heroku main
```
</details>
</div>

<div>
<details>
<summary>Render</summary>
Для корректной работы скрипта необходим установленный render сli. 
Не забудьте авторизоваться в cli перед выполнением команды
  
```bash
render create
render stack set --build-command "render build"
render secret create CHISEL_AUTH --env user:pass
git push render main
```

</details>
</div>

3. Подключитесь к  серверу

Запустите клиент chisel и подключените к cерверу:

```
chisel --version
chisel client --keepalive 10s --auth user:pass https://shrouded-springs-35880.herokuapp.com socks
```

Вместо https://shrouded-springs-35880.herokuapp.com укажите url отдеплоенного сервера

4. Проверьте работу прокси:
```bash
curl --socks5 127.0.0.1:1080 ifconfig.co
```

5. Укажите `127.0.0.1:1080` в качестве SOCKS5 прокси в вышем приложении

# Wireguard Vpn
Инструкция, как поднять vpn wireguard на сервере

Сервер можно найти много где, советую использовать [Vdsina](https://www.vdsina.com/?partner=9kmku94czt)

## Подключаемся к серверу
Подключиться к серверу можно с помощью [PuTTY](https://www.putty.org/)

`ssh root@ip-адрес`

IP адрес можно найти в тикете

Согласитесь с подключением — yes

После введите пароль сервера (его также можно найти в тикете)

## Устанавливаем Docker
```
curl -sSL https://get.docker.com | sh
sudo usermod -aG docker $(whoami)
exit
```

После снова подключаемся к серверу, как в предыдущем пункте.

## Устанавливаем WireGuard
```
docker run -d --name=wg-easy -e WG_HOST=(IP-адрес вашего сервера без скобок) -e PASSWORD=(придумайте пароль для входа в веб-интерфейс) -v ~/.wg-easy:/etc/wireguard -p 51820:51820/udp -p 51821:51821/tcp --cap-add=NET_ADMIN --cap-add=SYS_MODULE --sysctl="net.ipv4.conf.all.src_valid_mark=1" --sysctl="net.ipv4.ip_forward=1" --restart unless-stopped weejewel/wg-easy
```

## Настройка профилей Wireguard
Чтобы подключиться к веб-интерфейсу, введите в адресной строке: `http://IP-адрес сервера:51821`

Авторизовываемся с указанными паролем при установке Docker

Добавляем профили

# Red Privada sin Anuncios: Configura tu Propio Servidor con Pi-hole y VPN

## Inspiración

Este proyecto representa una de las principales razones por las que decidí crear un servidor en casa. Estos servicios, aunque ya los había utilizado individualmente, ahora se combinan de manera perfecta para crear un ecosistema de red y servicios propio. Esta integración no solo mejora la funcionalidad, sino que también te permite comprender mejor la infraestructura que respalda estos servicios.

## Objetivo

Con este proyecto, podrás navegar de forma cifrada, privada y libre de anuncios dentro de tu propia red privada. Un componente clave es Pi-hole, un servidor DNS que filtra los anuncios que pasan a través de él. Además, el servidor VPN cifra todo el tráfico de red, lo que te permite navegar de manera "segura". Esta combinación te proporciona un entorno más controlado y protegido para tus actividades en línea.

## Requisitos

- Docker
- Docker Compose
- Liberacion de puertos
- Dominio (opcional)
- IP fija (opcional)

## Recursos

- [¿Qué es un DNS?](https://www.webempresa.com/hosting/que-son-dns.html)
- [Pi-hole](https://pi-hole.net)
- [Docker](https://docs.docker.com/engine/install/debian/)
- [¿Qué es VPN-Wireguard?](https://nordvpn.com/es/blog/vpn-wireguard-que-es/?srsltid=AfmBOornxw7C4eCaS6Z6fD3e-oujkyzZVl_tcK0Jd9UYn8XjEn5P1Loi)

[Codigo ](Codigo/Codigo-explanation.md)

## Tutorial de uso

1. Clonamos el repositorio con `git clone [https://github.com/Gamabere921/VPN-Pihole-docker.git](https://github.com/Gamabere921/VPN-Pihole-docker.git)`
2. Entramos a la carpeta.
3. Configuramos las variables **PEERS** y **WEBPASSWORD** del docker-compose.yml a nuestro gusto.
4. Ejecutamos el comando `docker-compose up -d` para levantar los servicios
5. Para configurar Pi-hole entramos a [http://172.20.0.7/admin](http://172.20.0.7/admin) ponemos la contraseña que definimos y configuramos nuestra propia blacklist
6. Para conectarte a la VPN basta con poner `docker-compose logs` y nos visualizara unos codigo QR, los podemos escanear o agregarlo manualmente desde la aplicación

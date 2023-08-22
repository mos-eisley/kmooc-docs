---
title: Szerver telepítés
parent: Üzemeltetés
nav_order: 3
---
Az dev rendszeren a következők lettek konfigurálva:

- /etc/yum.repos.d/docker.repo fájl létrehozva a docker repo adataival
- sudo yum install docker-engine
- sudo systemctl enable docker.service
- sudo systemctl start docker
- sudo systemctl enable docker
- sudo systemctl stop httpd
- sudo systemctl disable httpd
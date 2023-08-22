---
title: Deployment
parent: Üzemeltetés
nav_order: 3
---
# Automatikus deployment

A rendszerből új verzió automatikus deployment segítségével kerül ki a teszt rendszerekre és az éles rendszerre. Első körben kikerül a teszt rendszerre az új verzió, majd tesztelés után kap egy verziócímkét a GIT-ben, melynek hatására elindul az automatikus telepítés az éles rendszerre.

Automatikus deployment-kor a következő lépések hajtódnak végre:

* A kód fordítása
* Automatikus egységtesztek futtatása
* A változásoknak megfelelően a containek újbóli létrehozása a deploy-álása. A kiesési idő ilyenkor minimális: leáll a régi container és indul az új.

!!! important "Fontos"
    A fenti pipeline miatt nem javasolt a container-eken kézzel módosítást végezni (pl. szoftvert telepíteni, konfigurációt módosítani), mivel a következő release-kor ezek felülíródnak. A konfigurációk a forráskód részét képezik és a forráskezelő rendszerben kerülnek tárolásra (a sensitive adatok, pl. SSH privát kulcs nem kerülnek be a források közé, ezeket a deployment rendszer *secure variables* tárolója szolgáltatja).

# Előfeltételek CentOS rendszeren

Ahhoz, hogy az automatikus deployment működjön távolról, a következő előfeltételeknek szükséges teljesülnie:

* Telepítsük a Docker-t: [https://docs.docker.com/engine/installation/linux/centos/](https://docs.docker.com/engine/installation/linux/centos/)
* Inicializáljuk a Docker Swarm clustert:
```
docker swarm init
```
* Hozzuk létre a konfiguráljuk a `kmooc-gitlabci` felhasználót, amit a GitLab fog használni az automatikus deployment-hez:
  * A szerveren hozzuk létre a felhasználót és adjuk hozzá a `docker` csoporthoz:
```
sudo adduser kmooc-gitlabci
sudo passwd kmooc-gitlabci
sudo usermod -aG docker kmooc-gitlabci
```
  * Hozzunk létre és másoljuk fel a felhasználóhoz ssh kulcsot:
```
ssh-keygen -f ./kmooc_gitlabci_rsa
ssh-copy-id -i ./kmooc_gitlabci_rsa.pub kmooc-gitlabci@HOST
```
  * Másoljuk be a privát kulcs (`kmooc_gitlabci_rsa`) tartalmát a GitLab projekt *Settings > CI/CD > Variables* alatt a következők szerint:
    * teszt rendszer esetén: `K8S_SECRET_TEST_SSH_PRIVATE_KEY` változóba
    * éles rendszer esetén: `K8S_SECRET_PROD_SSH_PRIVATE_KEY` változóba
  
* Amennyiben a szerveren fut http szerver, azt állítsuk le:
```
sudo systemctl stop httpd
sudo systemctl disable httpd
```
* A deployment szerver érje el SSH-val a szervert (publikus kulcs autentikációval).
* A szerver *80*-as és *443*-as portja legyen publikus.




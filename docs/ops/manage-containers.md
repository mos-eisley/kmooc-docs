---
title: Container-ek kezelése
parent: Üzemeltetés
nav_order: 3
---
# Áttekintés

A következőkben áttekintjük azokat az alapvető parancsokat, melyekkel a container-eket lekérdezni és adminisztrálni tudjuk. Ez nem tekinthető teljes Docker leírásnak, csupán az alapvető adminisztrációhoz szükséges parancsokat tartalmazza (teljeskörű leírás: [Docker docs](https://docs.docker.com/)).

# Parancsok
## Container-ek listázása
A futó container-eket a `docker ps` paranccsal tudjuk lekérdezni.

## Egy container részletes adatainak lekérdezése

A `docker inspect` paranccsal tudunk részletes információt kapni egy adott container-ről, pl.
```
docker inspect nginx
```

Többek között itt tudunk információt kapni arról, hogy a container-t a host gépről milyen IP címen érjük el. Ezt a `NetworkSettings/Networks` alatt találjuk:

```json
"Networks": {
  "nginx-proxy": {
  ...
    "IPAddress": "172.20.0.2",
  }
}
```

Illetve itt kapunk információt arról, hogy ha egy container portja ki van kötve a host egy adott portjára. Ezt a `NetworkSettings/Ports` alatt találjuk. Itt láthatjuk, hogy az `nginx` container `80`-as és `443`-as portja van kicsatornázva a host ugyanezen portjaira:

```json
"NetworkSettings": {
  ...
  "Ports": {
    "443/tcp": [
      {
        "HostIp": "0.0.0.0",
        "HostPort": "443"
      }
    ],
    "80/tcp": [
      {
        "HostIp": "0.0.0.0",
        "HostPort": "80"
      }
    ]
  }
	...
}
```

## Container log-ok megtekintése

A container-ek a logjaikat általában az `stdout`-ra irányítják át, melyet a `docker logs` paranccsal tudunk megtekinteni. Amennyiben követni akarjuk az új logbejegyzéseket, használjuk az `-f` kapcsolót, pl.:
```
docker logs -f coursecatalog_app_1
```

## Container újraindítása

A `docker restart` paranccsal tudunk egy container-t újraindítani, pl.:

```
docker restart coursecatalog_app_1
```

# Belépés a container-ekre

Amennyiben szükséges, a container-ekre a `docker exec -it container_name bash` paranccsal lehet bejelentkezni. Ilyenkor tulajdonképpen egy a container-ben futtatott `bash`-t tudunk interaktívan használni.

## Belépés az adatbázis szerverre

Az adatbázis container-be a  a következő parancs segítségével tudunk belépni:
```
docker exec -it coursecatalog_db_1 bash
```

Itt a `mysql` parancs segítségével tudjuk az adatbázist adminisztrálni:
```
mysql -p course_catalog
```

A host-ról lehetőség van a `3306`-os porton is elérni a szervert, illetve ha ki van csatornázva a host egy adott portjára, akkor amennyiben a host tűzfalán engedélyezve van, kívülről is el tudjuk érni.


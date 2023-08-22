---
title: Hibaelhárítás
parent: Üzemeltetés
nav_order: 3
---
# Hibaelhárítás

## Nem működik az adatok mentése

* **Jelenség**: Az oldal mentési funkciói nem működnek.
    * **Ok**: Elfogyott a rendelkezésre álló lemezterület a szerveren.
        * **Megoldás**: Szabadítsunk fel helyet.
            * Hasznos parancs lehet a nagy fájlok listázásához: ``
    * **Ok**: Nem sikerül az emailek kiküldése, a tranzakciók nem záródnak le.
        * **Megoldás 1**: Lehetséges, hogy elakadt egy tranzakció, de egyébként nincs probléma. Ebben az esetben a `projection_state` táblában a `phase` oszlop értéke az egyik rekordban `1`, vagy más, `0`-tól különböző érték lesz. Ezt szerkesszük át `0`-ra. Az emailek kiküldése folytatódni fog, ha nincs probléma az SMTP konfigurációval.
        * **Megoldás 2**: Ellenőrizzük a beállításokat, hogy helyesen vannak-e megadva az SMTP szerver adatai:
            * A [GitLab projekt CI/CD beállításaiban](https://gitlab.com/kmooc-course-catalog/course-catalog/-/settings/ci_cd), a `Variables` szekcióban találjuk a `CFG_SMTP_URL` változót. Ez az URL tartalmazza a teljes SMTP konfigurációt (cím, jelszó, stb).
            * Hiba esetén [kérjük rendszergazda segítségét](mailto:support@uni-obuda.hu).
            * Szerkesztés után a [Pipelines oldalon](https://gitlab.com/kmooc-course-catalog/course-catalog/-/pipelines/new) futtassunk egy új pipelinet a `release/production` branchhez, hogy a szerverre feltöltésre kerüljön az új érték.

## Lejárt tanúsítvány

* **Jelenség**: Az oldal lejárt tanúsítványt jelez.
    * **Ok**: Az ok az lehet, hogy *Let's encrypt* tanúsítványfrissítés után az NGINX nem töltötte újra a konfigurációt.
         * **Megoldás**: Jelentkezzünk be az NGINX container-re és töltsük újra a konfigurációt:
```
docker exec -it nginx bash
nginx reload
```

## Nem megfelelő tanúsítvány

* **Jelenség**: Az oldal azt jelzi, hogy nem megfelelő a tanúsítvány.
    * **Ok**: Ilyenkor tulajdonképpen nem a tanúsítvánnyal van baj, hanem valamiért kilépett az alkalmazás container-e.
        * **Megoldás**:
            1. A `docker logs coursecatalog_app_1` paranccsal nézzük meg a log-ot.
            2. Indítsuk újra az alkalmazást: `docker restart coursecatalog_app_1`




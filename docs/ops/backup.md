---
title: Biztonsági mentés
parent: Üzemeltetés
nav_order: 3
---
# Áttekintés

Mivel a rendszer teljes futtatási környezete újra előállítható az automatikus deployment segítségével, csupán az adatokat szükséges menteni. A rendszer által használt összes változó adat a `coursecatalog_db_1` container-ben futó MariaDB adatbázis szerver `course_catalog` adatbázisában található.

# Adatbázis biztonsági mentés

A `coursecatalog_backup_1` container feladata az adatbázis biztonsági mentése. 5 percenként készít egy új időponttal ellátott fájlnevű zip állományt. Ezeket a container-eket futtató host következő könyvtárába helyezi el: `/var/opt/kmooc/backup/`

{: .success-title }
> Rotáció
> 
> A biztonsági mentés rotálja a lementett fájlokat. Minden hónap elején törli a napi mentéseket, és a hónapból egy mentést archivál.
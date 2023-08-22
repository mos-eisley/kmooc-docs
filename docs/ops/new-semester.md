# Új félév indításakor elvégzendő lépések

!!! important "Fontos"
    A felhasználók a félév lezárta után is beiratkoztatva maradnak a kurzusokra, és a KMOOC-ból elérhetik azokat. Ezért új félév indításakor a Moodle-ban a meglévő kurzusok maradjanak elérhetőek, és az új félévhez új Moodle kurzust hozzunk létre. Ezt a Moodle kurzust fogjuk hozzárendelni a KMOOC egy kurzusidőpontjához.

!!! important "Fontos"
    Amennyiben új Moodle kerül telepítésre (nem frissítés), az LMS kapcsolatoknál hozzunk létre egy újat, így az azonosítóütközések elkerülhetőek.

A lépések:

1. Hozzuk létre a kurzust a Moodle-ban. (Amennyiben egy meglévő kurzust másolunk, a beiratkoztatási módszereket és a beiratkoztatott felhasználókat ne másoljuk.)
2. Konfiguráljuk be a beiratkoztatási módszert:
    1. A kurzus alatt válasszuk a *Course administration > Users > Enrolment methods* menüpontot.
    2. Az *Add method* alatt válasszuk az *MNET remote enrolments*-et.
    3. Remote host-nál válasszuk ki a KMOOC URL-jét.
    4. Kattintsunk az *Add method* gombra. **Fontos: Miután létrehoztuk a beiratkoztatási módszert és már van beiratkoztatott felhasználónk, ne töröljük a beiratkoztatási módszert, mert a KMOOC nem a teljes beiratkoztatási listát küldi, hanem csak a változásokat.**
3. A KMOOC-ban az *Adminisztráció > LMS kapcsolatok* oldalon kattintsunk a frissítés gombra az adott Moodle társgép sorában, majd ellenőrizzük, hogy megjelenik-e a kurzus a listában. Ezután a **Beírat**, **Leírat** és **Megnyitás** gombokkal tesztelhetjük is a beiratkoztatást.
4. Ezután hozzá tudjuk kapcsolni a Moodle kurzust a KMOOC kurzus egy adott időpontjához. Amennyiben még nem létezik a kurzusunk a KMOOC-ban, hozzuk azt létre az *Adminisztráció > Kurzusok* oldalon.
5. A kurzuslistában az adott kurzus sorában az **Időpontok** gombra kattintva tudunk új kurzusidőpontot létrehozni. Itt a dátumok megadása után válasszuk ki a megfelelő **Szervert**, majd válasszuk ki a szerveren kiajánlott **Kurzust**.
6. A **Megjelenik** opció segítségével tehetjük elérhetővé a kurzusidőpontot a felhasználók számára.

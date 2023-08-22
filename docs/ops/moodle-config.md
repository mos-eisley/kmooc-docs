# Áttekintés

A KMOOC és a Moodle MNET szabványú kommunikációs csatornát használ az távoli autentikációhoz, illetve a kurzusokra való beiratkozáshoz. A csatorna asszimetrikus kulccsal titkosított xmlrpc alapon működik.

További információk: [https://docs.moodle.org/32/en/MNet](https://docs.moodle.org/32/en/MNet)

Ahhoz, hogy a kapcsolat működjön, a következő lépéseket kell elvégezni:

1. A távoli Moodle-t konfigurálnunk kell az MNET-el való együttműködésre.
2. A KMOOC-ban fel kell vennünk a Moodle szervert, mint LMS.

# Moodle konfigurációja a KMOOC-al való kapcsolathoz

Ahhoz, hogy a Moodle MNET távoli bejelentkeztetés és a kurzusra való távoli beiratkoztatás működjön, a következő lépéseket hajtsuk végre a Moodle-ban:

1. Ellenőrizzük, hogy az MNET-hez szükséges modulok be vannak-e töltve:
    - `curl`
    - `openssl`
    - `xmlrpc`
2. Ellenőrizzük, hogy a `php.ini`-ben a `disable_functions`-ök között nincs-e `curl`-es vagy `openssl`-es függvénynév.
3. Kapcsoljuk be az MNET-et: az *Administration > Site administration > Advanced Features* oldalon kapcsoljuk be a *Networking*-et.
4. Kapcsoljuk be az MNET autentikációs modult: az *Administration > Site administration > Plugins > Authentication > Manage authentication* oldalon kapcsoljuk be az *MNET authentication*-t.
5. Kapcsoljuk be az MNET kurzusbeiratkoztatási modult: az *Administration > Site administration > Plugins > Enrolments > Manage enrol plugins* oldalon kapcsoljuk be a *MNet remote enrolments*-t.
6. Vegyük fel a KMOOC-ot, mint MNET társgép:
    1. Kattintsunk *Administration > Networking > Manage peers*-re.
    2. Az *Add a new host* alatt adjuk meg:
        - *Hostname*-nél adjuk meg a KMOOC teljes gyökér URL-jét: `https://www.kmooc.uni-obuda.hu`
        - Az *Application type* legyen `moodle`
    3. Kattintsunk az *Add host*-ra.
    4. A *Public key* alatt adjuk meg a KMOOC publikus tanúsítványát. Ezt a következő URL-ről tudjuk kimásolni: [https://www.kmooc.uni-obuda.hu/mnet/publickey.php](https://www.kmooc.uni-obuda.hu/mnet/publickey.php)
    5. Kattintsunk a *Save changes*-re.
    6. Felül kattintsunk a *Services* fülre, majd kattintsuk be a következőket:
        - *Remote enrolment service*: *Publish*
        - *SSO (Identity Provider)*: *Subscribe*
        - *SSO (Service Provider)*: *Publish*
7. A KMOOC küldi a tanulói kódot (Neptun kód vagy egyéb kód) és az intézmény nevét is, ahhoz, hogy a Moodle fogadni tudja ezeket, a következő beállításokat szükséges elvégezni:
    1. Kattintsunk az *Administration > Networking > Profile fields*-re.
    2. A *Fields to import*-nál jelöljük be az `idnumber` és `institution` mezőket és mentsük el az űrlapot.
8. Ezután ki tudjuk ajánlani a Moodle kurzusokat a KMOOC számára. A következő lépéseket minden kiajánlandó kurzusnál végre kell hajtani:
    1. A kurzus alatt válasszuk a *Course administration > Users > Enrolment methods* menüpontot.
    2. Az *Add method* alatt válasszuk az *MNET remote enrolments*-et.
    3. Remote host-nál válasszuk ki a KMOOC URL-jét.
    4. Kattintsunk az *Add method* gombra.

# Moodle szerver felvétele a KMOOC-ban

1. Az *Adminisztráció > LMS kapcsolatok* alatt kattintsunk az *Új Moodle kapcsolása* gombra.
2. Adjuk meg az adatokat:
    - A *Név* mezővel lehet majd hivatkozni a szerverre, ez bármi lehet.
    - A *Moodle URL*-nél a távoli Moodle publikus URL-ét adjuk meg, pl.: `https://elearning.uni-obuda.hu/kmooc`
    - A *Publikus tanúsítvány* mezőbe másoljuk be a Moodle publikus kulcsát a *Administration > Networking > Settings* oldalról.
3. Kattintsunk a létrehozás gombra.
4. Amennyiben rögtön nem jelenik meg a listában, frissítsük az oldalt.
5. Teszteljük a funkciókat:
    - A szerver sorában lévő *Frissítés* gomb segítségével tudjuk letölteni a Moodle szerver által kiajánlott kurzusokat. Sikeres letöltés esetén megjelenik a *Sikeres kurzuslista frissítés* üzenet.
    - Válasszunk ki egy kurzust, majd a *Beírat* és *Leírat* gombokkal teszteljük a kurzusra való beiratkoztatást.
    - A *Megnyitás* gombra kattintva tudjuk tesztelni a tananyag megnyitását.

# Hibaelhárítás

Amennyiben a beiratkoztatás vagy a kurzus megnyitás nem működik:

1. Ellenőrizzük, hogy kölcsönösen jó publikus kulcsok vannak-e beállítva a Moodle-ban és a KMOOC-ban.
2. Ha a kulcsok megfelelőek, a Moodle *Administration > Networking > Settings* oldalán a *Delete this key* melletti gomb megnyomásával töröljük a jelenlegi kulcsot, majd a KMOOC-ban állítsuk be a Moodle által újonnan generált kulcsot.
3. Kapcsoljuk be a Moodle-ban a debug módot és figyeljük a PHP warning és error üzeneteket.

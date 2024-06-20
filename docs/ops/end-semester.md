---
title: Félév zárása
parent: Üzemeltetés
nav_order: 3
---
*Útmutató kezdőknek és feledékenyeknek, avagy hogyan ne haljunk meg félév végén.*

## Jegyek beírása K-MOOC rendszerbe
A jegyek beírásához az oktatóktól kapott táblázatokat az importfájl szerint kell formázni:

| Email | Érdemjegy |
|:-----|:---------:|
| pelda.panna@mail.com	| 2|

> Ha a kapott táblázat nem tartalmazza az e-mail-címeket, a K-MOOC webről a kurzushoz tartozó jelentkezéseket kell letölteni, az Excel exportra kattintva.

Az adatok összefésülésére **XKERES** függvényt érdemes használni. A kész táblázat fájltípusa: **.csv** (pontosvesszővel elválasztott)

A K-MOOC weben a jegyek felöltésére a **Jegy Import** funkció felel.
![image](https://github.com/mos-eisley/kmooc-docs/assets/94133260/4c2ff90f-fa17-4594-8fb1-303675f459ed)

>Ha az oktató nem küldött teljes listát, csak 2-es és jobb jegyekről, akkor importálás után szedd le az **Excel exporttal** a teljes táblát, írd át a 0-s érdemjegyeket 1-esre, és .csv fájlként töltsd vissza.

## Beírt jegyek ellenőrzése
Töltsd le a kurzus felületéről az Excel fájlt.
Hozz létre benne egy új munkalapot, ahová másolod az oktatótól kapott táblázatot.
 
Ellenőrizd XKERES függvénnyel, hogy azt az érdemjegyet kapták-e, ami az oktatói táblában szerepel.

> =XKERES(D2;Munka1!E:E;Munka1!D:D;1)

![image](https://github.com/mos-eisley/kmooc-docs/assets/94133260/4d90138b-89fb-4ed2-b951-c34b09c4d8ed)

*Ha eltérés van, mint a fenti ábrán, az oktatói táblában a 0-kat, kihúzásokat és egyéb kommenteket is cseréld le 1-esre.*
Az Ellenőrzés oszlop egy sima összehasonlítás, hogy az Érdemjegy oszlop megegyezik-e a KMOOC check-kel (később csak CH és OK? oszlopok).

> =HA(L2=M2;1;404)

Ahol az Ellenőrzés oszlopban 404 található, ott eltérés van. Ezeket írd fel! *Lehetőleg a Jegybeírás folyamatjelző megosztott Excel fájl külön lapjára*

## K-MOOC kreditigazolás kiküldése

*Lehetőleg csináld rendesen, hogy ne kelljen utána ezzel szórakozni ^^*

Mentsd el a visszaadott fájlokat, töltsd fel a megfelelő mappába.
## Neptun import
Kösd fel a gatyót…
Hozzávalók:
-	1 db K-MOOC kurzusjelentkezések táblázat (letölt)
-	1 db UltimateImportfileGenerator.exe importfájl
-	1 db Neptun_courses táblázat (létezik)
-	1 db Neptun_students tábelle (generálni)
Egyéb hozzávalók:
-	VPN
-	Neptun kari admin jogosultság
-	Benedek (baj esetére)
Elkészítés:
A K-MOOC webről szedd le az aktuális félévhez tartozó teljes kurzusjelentkezés táblát (kmooc_enrollments.xlsx néven).
Futtasd az UltimateImportfileGenerator.exe programot. Gyönyörködj, aztán adj meg egy egyéncsoport nevet (pl. jp7x4c-kmooc-2023-24-2)
Ezt követően megkapod az egyéncsoport generálásához szükséges szart (egyencsoport_import.xlsx)
Lépj be Neptunba és imádkozz, hogy ne akarjon frissíteni.
Adminisztráció  Tartalmi adminisztráció 	itt valahol keresd meg az Egyéncsoportokat
Hozz létre itt egy egyéncsoportot a félévre (pl. jp7x4c-kmooc-2023-24-2 ugyanaz legyen, mint fent!)
Importáld a program által generált szart: jobb click az egyéncsoportok listájába és Import, itt kérdezd meg Benedeket, hogy melyiket válaszd. Aztán a megjelenő ablakban fent keresd meg a nagyon logikus 3 pontos gombot, és tallózd be a generált fájlt. Aztán hajrá!
A megjelenő táblát nem kell letölteni.
Átmész az Általános lekérdezésekbe. Saját lekérdezések, Egyéncsoportok, K-MOOC (…)
Itt az első adattáblánál módosítsd a feltételt a fenti egyéncsoportos névre (pl. jp7x4c-kmooc-2023-24-2), majd az utolsó táblánál a félévet az aktuálisra, az ott található formátumban.
Aztán hajrá, lekérdezés!
A kapott táblázatot töltsd le a UltimateImportfileGenerator.exe mellé neptun_students.xlsx néven!
Szedd elő valahonnan a NAS-ról a neptun_courses Excel fájlt. Ellenőrizd, hogy minden K-MOOC-os kurzus benne van-e, és helyes-e. Ellenőrizd, hogy Bilicska Csaba nem kis L-lel írta-e a nagy I-t.
Folytasd a program futtatását.


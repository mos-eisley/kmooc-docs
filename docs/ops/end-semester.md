---
title: Félév zárása
parent: Üzemeltetés
nav_order: 3
---
*Útmutató kezdőknek és feledékenyeknek, avagy hogyan ne haljunk meg félév végén. ❤*

## Jegyek beírása K-MOOC rendszerbe
A jegyek beírásához az oktatóktól kapott táblázatokat az importfájl szerint kell formázni:

| Email | Érdemjegy |
|:-----|:---------:|
| pelda.panna@mail.com	| 2|

> Ha a kapott táblázat nem tartalmazza az e-mail-címeket, a K-MOOC webről a kurzushoz tartozó jelentkezéseket kell letölteni, az Excel exportra kattintva.

Az adatok összefésülésére **XKERES** függvényt érdemes használni. A kész táblázat fájltípusa: **.csv** (pontosvesszővel elválasztott)

A K-MOOC weben a jegyek felöltéséért a **Jegy Import** funkció felel.
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

Ahol az Ellenőrzés oszlopban 404 található, ott eltérés van. Ezeket írd fel! *Lehetőleg a Jegybeírás folyamatjelző megosztott Excel fájl külön lapjára.*

## K-MOOC kreditigazolás kiküldése

*Lehetőleg csináld rendesen, hogy ne kelljen utána ezzel szórakozni ^^*
Ha minden jó, ***push the button***!

Mentsd el a visszaadott fájlokat, töltsd fel a megfelelő mappába.

## Neptun import
*Kösd fel a gatyót…*\
Elkészítési idő: **3-5 óra**\
Kalória: -156.000 cal

### Hozzávalók:
-	1 db K-MOOC kurzusjelentkezések táblázat (letölt)
-	1 db UltimateImportfileGenerator.exe importfájl
-	1 csipet Neptun_courses táblázat (létezik)
-	1 szem Neptun_students táblázat (generálni)

Egyéb hozzávalók:
-	VPN
-	Neptun kari admin jogosultság
-	Benedek (baj esetére)

### Elkészítés:

#### El**Ő**készítés:

Töltsd le [innen](https://github.com/mos-eisley/ultimate-importfile-generator/releases) az **UltimateImportfileGenerator** programot, majd futtasd és... *Gyönyörködj!*

A K-MOOC webről szedd le az aktuális félévhez tartozó teljes kurzusjelentkezés táblát, és tedd bele az előbb létrejött `data/` mappába
>data/kmooc_enrollments.xlsx

Futtasd újra és adj meg egy egyéncsoport nevet!

>pl. jp7x4c-kmooc-2023-24-2

Ezt követően megkapod az egyéncsoport generálásához szükséges fájlt a `generated/` mappába.
>generated/egyencsoport_import.xlsx

Lépj be Neptunba és imádkozz, hogy ne akarjon frissíteni.

1. Adminisztráció
2. Tartalmi adminisztráció
3. itt valahol keresd meg az Egyéncsoportokat

Hozz létre itt egy egyéncsoportot a félévre
>pl. jp7x4c-kmooc-2023-24-2 **ugyanaz legyen, mint fent!**

Importáld a program által generált szart:
1. jobb click az egyéncsoportok listájába,
2. Import,
3. Csoportok egyénei,
4. bal alul válts át a vegyes importálásra,
   
   ![image](https://github.com/mos-eisley/kmooc-docs/assets/94133260/4dbf2d64-04ef-4ac6-93a9-445433a38108)
5. aztán a megjelenő ablakban fent keresd meg a nagyon logikus 3 pontos gombot, és tallózd be a generált fájlt. Aztán hajrá!

*A megjelenő táblát nem kell letölteni.*

Utána...
1. Átmész az Adminisztráció/Központi beállítások/Általános lekérdezésekbe,
2. itt fura ikon jobb alul
   
   ![image](https://github.com/mos-eisley/kmooc-docs/assets/94133260/3b854835-bdbf-43cb-9a45-e96b0cd95aac)

3. saját lekérdezések,
4. Egyéncsoportok,
5. Autoimport K-MOOC képzés lekérés


Itt az első adattáblánál módosítsd a feltételt a fenti egyéncsoportos névre,
>pl. jp7x4c-kmooc-2023-24-2

majd az utolsó táblánál a félévet az **aktuálisra**, az ott található formátumban.

Aztán hajrá, lekérdezés!

A kapott táblázatot töltsd le, majd mentsd:
>data/neptun_students.xlsx

Szedd elő valahonnan a NAS-ról a
>neptun_courses.xlsx

Excel fájlt, és aktualizáld, ha kell.

Ellenőrizd, hogy minden K-MOOC-os kurzus benne van-e, és **helyes-e**.

Ellenőrizd, hogy Bilicska Csaba nem kis L-lel írta-e a nagy I-t, ha nem, köszönd meg neki. 😊

Futtasd újra a programot; létrejönnek:
- `generated/neptun_enrollment_import.xlsx`: Minden tárgy minden kurzusára minden hallgatót ráírató NAGYON EXCEL
- `generated/subjects/*`: Kurzusonként importálható jegy-adatsorok
- Valamint `_error` végződésű fájlok. Itt ellenőrizd, hogy nem volt-e váratlan hiba a kurzusok vagy hallgatók között!

#### Az IMPORTÁLÁS maga!

##### Tárgyak/Kurzusok/Hallgatók
Neptunban lépj be konkrétan bármelyik tárgy bármelyik kurzusába.

> Jobbklikk -> Import -> Tárgyak, Hallgató, Kurzusok összerendelése

Az ablakban tallózd a `neptun_enrollment_import.xlsx` fájlt, ellenőrizd meg hogy minden kulcsot megtalált-e, és ZSA! (Ez nagyon sokáig fog tartani, addig menj le Marci a pékhez, majd ebédelni Andihoz, és még mindig nem lesz kész. Ha visszaértél, _telepíts plugint_ amíg kész nem lesz.

##### Jegybeírás

A tárgyaknál szűrj az `EKM` kezdetű kurzuskódokra, kattints jobb felül az Összes adat megjelenítésére és rendezz kurzuskód szerint (ezt még megköszönöd).

Tárgyanként lépj be a megfelelő kurzusba, majd a Kurzusjegy beírásra.\
Válaszd ki alul tanárt. When in doubt, válaszd Andit (nem a büfést). Ha van alapértelmezett, hagyd úgy.\
Importáld a kurzusnak megfelelő jegyadatsort a `generated/subjects/` mappából. Így bekerül mindenkihez a beírandó jegy. Ezt ellenőrizd, ha unatkozol, utána kattints a Jegybeírásra.

Ízlés szerint ismételd az előző lépést (vagy amíg kész nem leszel - amelyik később következik be).

That's it.

![image](https://github.com/mos-eisley/kmooc-docs/assets/94133260/08fd6ba4-11fa-48fa-a075-338b978bd27d)

Made with ❤

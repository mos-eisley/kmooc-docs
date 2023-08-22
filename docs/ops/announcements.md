---
title: Közlemények, szerkeszthető szövegek
parent: Üzemeltetés
nav_order: 3
---
# Közlemények és szerkeszthető szövegek

Az admin felületen az Általános oldalon találjuk a [Közleményeket](https://kmooc.uni-obuda.hu/admin/general).

A Közlemények rendszerben található az oldalon szereplő minden dinamikusan szerkeszthető szöveg.

## Hely

A közleményeket a `Hely` tulajdonság azonosítja - ez dönti el, hogy melyik oldalon jelennek meg. Kötelező megadni.

Az oldal kódjában a helyek előre meg vannak határozva, ezek a következők:

| `Hely` kód | Feladat | Tulajdonságok |
|-|-|-|-|
| `home` | Főoldali rendszerüzenetek | Több azonos kódú üzenet esetén mind megjelenik.<br />Minden tulajdonság használható. |
| `home_periods` | Idővonalon megjelenő kártyák | Több azonos kódú üzenet esetén mind megjelenik. Közöttük nyilak jelennek meg. *Tipp: A design 4db ilyen üzenetre van tervezve.*<br />Használható: ikon, cím (periódus neve), tartalom (periódus leírása, ideje). |
| `faq` | Gyakran Ismételt Kérdések elemei | Több azonos kódú üzenet esetén mind megjelenik.<br />Használható: ikon, cím, tartalom (lenyílóban jelenik meg). |
| `course_no_period` | Kurzusoldalon jelenik meg, ha nincs nyitott időpont. | Több azonos kódú üzenet esetén mind megjelenik.<br />Minden tulajdonság használható. |

{: .success-title }
> Egészíts ki
>
> Ha fejlesztés során új közleményhelyeket hozunk létre, ne felejtsük el őket a fenti táblázathoz hozzáadni [ezen a linken](https://github.com/mos-eisley/kmooc-docs/edit/main/docs/ops/announcements.md) (írási hozzáférés szükséges)!

## Ikon

*A különböző közleményhelyek más-más módon jeleníthetik meg az ikont.*

[Innen,](https://fontawesome.com/v4/icons/) a FontAwesome v4 verzióból válasszunk ikont.

Az ikon kódja önmagában használható (pl. fa- előtag, egyebek nélkül). Kötőjelek helyett használjunk szóközt.  
Pl: `fa-chain-broken` ➡ `chain broken`

## Szint

*Bizonyos közleményhelyek nem jelenítik meg a szint tulajdonságot.*

A Szint tulajdonsággal beállíthatjuk egy közlemény "színét", egy előre meghatározott listából. Ezek megegyeznek az `elearning.uni-obuda.hu` szerveren használt `config.yml` fájlban használható értékekkel.

[Innen válasszunk.](https://getbootstrap.com/docs/4.0/components/alerts/)

## Dátumtól Dátumig

Megadhatjuk, hogy a közlemény mikor legyen érvényes. Minden közleményhelyre vonatkozik.

Egy közlemény csakis akkor jelenik meg, amikor a jelenlegi időpont a megadott időpontok közé esik. *Ez az egyetlen közleményt használó, szövegbehelyettesítő közleményhelyekre is vonatkozik!*

Mindkét dátummező opcionálisan üresen hagyható. Ilyen esetben az adott dátum "végállapotú":  
Ha nincs kezdődátum, a közlemény öröktől fogva érvényes.  
Ha nincs végdátum, a közlemény örökké érvényes lesz.

## Cím

*Nem minden közleményhely jeleníti meg.*

Egyszerű, többnyelvű szövegmező. Címként jelenik meg a legtöbb helyen.

## Tartalom

*Nem minden közleményhelyen alkalmazódik a Markdown formázás!*

Többnyelvű, Markdown formázott mező (a legtöbb helyen - ahol nem, ott egyszerű szövegként jelenik meg).  
A szövegbehelyettesítő közleményhelyeknél ez az egyetlen megjelenő információ.

Kötelező megadni.
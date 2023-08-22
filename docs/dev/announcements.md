---
title: Közlemények, szerkeszthető szövegek
parent: Fejlesztés
nav_order: 3
---
# Közlemények és szerkeszthető szövegek

## Új közleményhely hozzáadása

### Előfeltétel

Mivel a közleményeket az adatbázisból, GraphQL segítéségvel kell lekérni, ezért minden közleményeket használó komponens `Container` kell, hogy legyen, ami megkapja a `props`-on keresztül a `viewer`-t.  
Ez az `app/routes.tsx` fájlból érkezik minden `Route`-beli komponensnek, ami megkapja a `queries={viewerQueryRoot}` tulajdonságot.

Nem az átlagos React komponensünket fogjuk tehát használni, hanem azt először `Relay Container`be foglaljuk.

Példa: `CoursePage` az eredeti, "sima" React komponens.

```tsx
export const CoursePageContainer =
	Relay.createContainer(Controls.withRelay(CoursePage), {
		initialVariables: {
			courseId: '0'
		},
		fragments: {
			viewer: () => Relay.QL`
			fragment on Viewer {
        ...
			}
		`}
	});
```

Ha ez megvan (vagy már eredetileg is így volt), a `fragment`-hez adjuk hozzá a kívánt közleményhely szűrését:

```graphql
fragment on Viewer {
  course_no_period: frontendAnnouncements(field: "course_no_period") {
    edges {
      node {
        icon
        severity
        titleData
        contentData
      }
    }
  }
}
```

*A szűrést a `field: "SZŰRŐ"` végzi, a sor elején csak kényelmi célból megadhatjuk - akár ugyanazt - egy mezőnévként, hogy a kódban könnyebb legyen rá hivatkozni.*

### Hagyományos üzenetdobozokat megjelenítő hely

Ha beírtuk a `fragment`-be a lekérést, nincs más dolgunk, mint a komponenshez hozzáadni az `AnnouncementAlerts` elemet, aminek továbbítjuk a `viewer`-ből az adatokat.

Importáljuk:

```tsx
import { AnnouncementAlerts } from '../../announcement/frontend/alerts';
```

Majd az előző példában használt névvel:

```tsx
<AnnouncementAlerts data={this.props.viewer.course_no_period} />
```

Ezen a helyen meg fognak jelenni az erre a helyre kiírt közlemények színezett, ikonozott, stb. üzenetdobozokban.

### Szövegbehelyettestítés közleményből

Ha beírtuk a `fragment`-be a lekérést, nincs más dolgunk, mint a komponenshez hozzáadni a `TextAnnouncement` elemet, aminek továbbítjuk a `viewer`-ből az adatokat.

Importáljuk:

```tsx
import { TextAnnouncement } from '../../announcement/frontend/text';
```

Majd egy szövegen belül használhatjuk is, az előző példában használt névvel:

```tsx
<div>
  Szia, én egy szöveg vagyok. A következő szó {<TextAnnouncement data={this.props.viewer.course_no_period}>} be van helyettesítve.
</div>
```
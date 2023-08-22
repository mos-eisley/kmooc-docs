!!! warning "Deprecated"
		A Facebook és Google bejelentkezés a jelenlegi verzióban nem működik.
		
		A dokumentáció archív célból érhető csak el.


# Áttekintés

Ahhoz, hogy a felhasználók be tudjanak jelentkezni Facebook, illetve Google azonosítóval is, létre kell hozni az ehhez szükséges API azonosítókat. Az így létrehozott azonosítókat az alkalmazás konfigurációs fájljába szükséges felvenni. A konfigurációs állományokat ezután az automatikus deployment juttatja el az éles szerverre.

# Facebook App ID és App Secret létrehozása
1. Jelentkezz be a **`https://developers.facebook.com/`** oldalon a saját Facebook fiókoddal.
2. A jobb felső sarokban találod a profilodhoz tartozó menüsort, ott klikk az **Add a New App** linkre.
3. A felugró ablakban töltsd ki a **Display Name**, **Contact Email** mezőket, a **Category**-ban válaszd az **Apps For Pages** lehetőséget, majd klikk a **Create App ID** gombra.
4. A bal oldali navigációs területen a **Settings** menüpontra klikkelve megtekintheted az *App ID*-t és a *App Secret*-et, és az oldal alján található **+ Add Platform** gombra klikkelve feljön egy ablak, melyben válaszd ki a **Website** lehetőséget.
5. A **Site URL** mezőbe írd be a **`https://www.kmooc.uni-obuda.hu/login`** címet.

# Google Client ID és Client Secret
1. A Google-fiókódba bejelentkezés után lépj az **API Manager**-be: `https://console.developers.google.com/projectselector/apis/credentials`.
2. A bal oldali menüben válasszd ki a **Credentials** menüpontot, majd hozz létre egy új projektet (**Create a project**).
3. A felugró ablakban adj nevet a projektnek (**Project name** mező).
4. Klikk a **Create credentials** combo boxra és válaszd ki a **0Auth client ID** lehetőséget a megjelenő listából.
5. A jobb oldalon megjelenik a **Configure consent screen** gomb, klikkelj rá.
6. A megjelenő formon válaszd ki a használni kívánt email címet (**Email address**), ha többet is felajánl, és töltsd ki a **Product name shown to users** mezőt (pl. Auth0 Client), aztán mentsd el a beállításokat a **Save** gombbal.
7. A megjelenő listából válaszd ki a **Web application**-t.
8. Adj nevet az "alkalmazásnak" (**Name** mező), írd be az **Authorized JavaScript origins** és az **Authorized redirect URIs** mezőkbe a **`https://www.kmooc.uni-obuda.hu`** értéket, majd klikk a **Save** gombra.
A felugró ablakban megkapod a *Client ID*-t és a *Client Secret* értékeket.
10. Engedélyezd az Admin SDK service-t:
	- Klikk a bal oldali sávban található **Library** menüpontra.
	- Klikk az **Admin SDK**-n a listából.
	- Az Admin SDK oldalon kattints az **Enable** gombra.
## Csatlakozás engedélyezése Auth0-val
1. Jelentkezz be a **`https://manage.auth0.com/`** oldalra és klikk a bal oldali menüpontok közül a **Connections -> Social** menüpontra.
2. Válaszd ki a **Google** feliratot, és az **Apps** fülön engedélyezd a kapcsolatot, aztán **Save**.
3. A **Settings** fülön a **Client ID** és **Client Secret** mezőbe írd a korábban létrehozott *Client ID* és *Client Secret* értékeket, majd válaszd ki az engedélyeket a felsorolásból, és mentsd el a beállításokat a **Save** gombbal.

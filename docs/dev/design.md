# Design

## Semantic UI témázása

.variables fájlok szerkeszthetők, pl:
semantic-themes/frontend/semantic/src/themes/default/globals/site.variables

Szerkesztés után futtassuk:
```sh
cd semantic-themes/frontend/semantic/
# első alkalommal erre is szükség lesz:
# npm install
gulp build
```

Ezzel legenerálódik többek között a `semantic-themes/frontend/semantic/dist/components` mappa tartalma. Ezeket a .css és .js fájlokat kézzel ne szerkesszük, mert felülíródnak a következő build során!

A parancs kiadása után automatikus a hot reload, láthatjuk a módosításainkat.

## Egyéni css

További css definíciókat adhatunk meg pl: `src/app/styles/themes/frontend/frontend.scss` fájlban, és az emellett található scss fájlokban.

Ezek elmentésekor szintén automatikus a hot reload.
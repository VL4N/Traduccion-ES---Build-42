# Estado de la traduccion

Base: Project Zomboid 42.19.0. Total de cadenas ausentes en el ES del juego: **21 147**.

## Hecho (9255 cadenas, validadas sin errores)

Todo lo que un jugador ve esta traducido. No queda nada pendiente de interfaz.

| Archivo | Cadenas | Estado |
|---|---:|---|
| ItemName.json | 3165 | COMPLETO |
| Recipes.json | 1898 | COMPLETO |
| IG_UI.json | 1315 | COMPLETO (lo visible) |
| UI.json | 647 | completo |
| Sandbox.json | 453 | completo |
| ContextMenu.json | 312 | completo |
| Moveables.json | 306 | completo |
| Tooltip.json | 292 | completo |
| SurvivalGuide.json | 228 | completo |
| Fluids.json | 197 | completo |
| Moodles.json | 190 | completo |
| Farming.json | 107 | completo |
| Stash.json | 71 | completo |
| Entity.json | 37 | completo |
| MapLabel.json | 14 | completo |
| Attributes.json | 12 | completo |
| BodyParts.json | 11 | completo |

En UI.json se omitieron a proposito 218 claves `UI_credits_*` (nombres del equipo de
desarrollo). Al no estar en el ES, el juego cae al ingles, que es lo correcto para
un nombre propio. Los encabezados `UI_credits_header_*` si estan traducidos.

## Pendiente, por prioridad de juego

| Archivo | Cadenas | Que es |
|---|---:|---|
Nada de interfaz. Solo queda texto de lore, que se lee unicamente si abres un libro,
una revista o pones una cinta:
| Recorded_Media.json | 615 | cintas, CDs y VHS (lore) |
| Print_Media.json | 345 | libros y revistas (lore, textos largos) |
| Print_Text.json | 318 | notas y textos impresos (lore) |
| Farming/otros sueltos | ~20 | mapas y varios |

## No se traducen a proposito

| Archivo / bloque | Cadenas | Motivo |
|---|---:|---|
| SurvivorNames.json | 6008 | nombres propios |
| Credits.json | 77 | nombres del equipo |
| UI.json `UI_credits_*` | 218 | nombres del equipo |
| IG_UI `IGUI_PetName_*` | 229 | nombres de mascotas |
| IG_UI marcas y empresas | 201 | nombres comerciales ficticios |
| IG_UI claves vacias | 350 | el juego base no tiene texto ahi |
| IG_UI depuracion y editores | 580 | paneles que solo salen arrancando con -debug |

El bloque de depuracion se deja en ingles a proposito: quien abra el depurador de clima,
el editor de vehiculos o el monitor de recetas espera los nombres tecnicos originales.
Traducirlos dificulta buscar ayuda o reportar bugs. Las traducciones oficiales del juego
hacen lo mismo.

Al no estar en el ES, el juego cae al ingles, que es lo correcto para un nombre propio.

## IG_UI: como esta repartido

`Documents\TraduccionES_B42_herramientas\split-igui.ps1` reparte IG_UI en cuatro bloques:

| Bloque | Cadenas | Estado |
|---|---:|---|
| core (interfaz real) | 2446 | 792 hechas, 1654 pendientes |
| flavor (titulos de libros, comics, revistas, fotos) | 2597 | pendiente, baja prioridad |
| debug (menus de depuracion y editores) | 334 | pendiente, muy baja prioridad |
| skip (nombres de mascotas) | 229 | no se traduce |

## Flujo de trabajo por tandas

`Documents\TraduccionES_B42_herramientas\restante.ps1` dice que queda de un archivo, comparando el material en ingles
contra lo que ya esta en el mod. Lanzalo antes de cada tanda:

```
.\restante.ps1 -Archivo ItemName.json
.\restante.ps1 -Archivo IG_UI.json -Origen .\igui\core.txt
```

Deja el resultado en `Documents\TraduccionES_B42_herramientas\restante-<archivo>.txt`.

Las tandas ya traducidas viven en `Documents\TraduccionES_B42_herramientas\<archivo>\es-p*.txt` y se ensamblan asi
(desde bash, no PowerShell):

```
{ printf '{\n'; cat es-p*.txt | sed '$ s/,$//'; printf '}\n'; } > destino.json
```

Despues, siempre `Documents\TraduccionES_B42_herramientas\validar.ps1`: comprueba BOM, duplicados, claves huerfanas
y placeholders `%1` descuadrados en todos los archivos del mod de una pasada.

## Herramientas

En el scratchpad de la sesion quedaron tres scripts:

- `extract-missing.ps1` - vuelca a `pendiente\*.json` las claves que faltan con su texto en ingles.
- `validar.ps1` - comprueba BOM, duplicados, claves huerfanas y placeholders `%1` descuadrados.
- `diff-es.ps1` - tabla de cobertura EN vs ES.

Conviene volver a lanzar `extract-missing.ps1` despues de cada parche del juego: cada version
anade claves nuevas.

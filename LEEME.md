# Traduccion ES - Build 42

Mod de traduccion al espanol para Project Zomboid 42.19. Solo aporta las claves que el
juego base no tiene traducidas; no sustituye ningun archivo del juego.

## Estructura

```
Zomboid\Workshop\TraduccionES_B42\     <- esta carpeta es la que lee el subidor de Steam
├─ workshop.txt                        <- titulo, descripcion y tags del item
├─ preview.png                         <- imagen de la ficha en Steam (512x512)
├─ LEEME.md
├─ estado.md
└─ Contents\mods\TraduccionES_B42\
   ├─ mod.info                         <- obligatorio en la raiz
   ├─ poster.png
   └─ 42\                              <- carpeta de version (aplica a toda la 42.x)
      ├─ mod.info                      <- OBLIGATORIO tambien aqui
      ├─ poster.png
      └─ media\lua\shared\Translate\ES\
         └─ *.json                     <- las traducciones
```

**Importante:** en Build 42 cada carpeta de version necesita su propio `mod.info`. Si solo
esta el de la raiz, el subidor del juego falla con *"No se encuentra el archivo mod.info en
tu mod"*. El `poster` declarado en el `mod.info` de la version tiene que existir en esa
misma carpeta.

`Zomboid\mods\TraduccionES_B42` es una junction (enlace) a `Contents\mods\TraduccionES_B42`,
asi que el juego carga directamente lo que edites aqui. No hay que copiar nada.

## Reglas al traducir

- UTF-8 **sin BOM**. Con BOM o en ANSI los acentos salen rotos.
- Los marcadores `%1`, `%2`, `<LINE>`, `\n`, `\\n` se copian tal cual.
- Las comillas dentro del texto van escapadas: `\"`.
- La clave (izquierda) nunca se toca.
- Ojo con las claves que solo difieren en mayusculas (`Farming_Lemongrass` y
  `Farming_LemonGrass`): el juego las trata como distintas, hay que poner las dos.

## Que NO conviene traducir

- `SurvivorNames.json` (6008): nombres propios estadounidenses.
- `Credits.json` (77): nombres del equipo.
- `MapLabel.json`: nombres de pueblos reales de Kentucky (solo se tradujeron los rios).

## Estado

Ver `estado.md`.

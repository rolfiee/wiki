---
lang: hu-HU
layout: wiki
section: twilightmenu
category: customization
title: DSi/3DS szkinek - Egyedi hangeffektusok
description: Hogyan használj egyedi háttérzenét és hang effekteket a DSi és 3DS szkinekben a TWiLight Menu++-ban
---

A TWiLight Menu++ támogatja az egyedi hang fájlokat a témákban. Rakd a hangfájlokat a `sound` alkönyvtárba a téma mappádba, például a `white` téma esetén, a fájljaid a `themes/white/sound/sfx.bin` és a `themes/white/sound/bgm.pcm.raw` kell legyenek. Mindkét fájl opcionális, ha a `bmg.pcm.raw` hiányzik, az alapértelmezett zene kerül felhasználásra. Ugyanez történik a hangeffektekkel is, ha az `sfx.bin` szintén hiányzik.

Ezek a lépések feltételezik, hogy rendelkezel devkitPro-val telepített mmutil-lal. A devkitPro-t beszerezheted a [devkitPro weboldaláról](https://devkitpro.org/wiki/Getting_Started).

## Hang effektusok bank
A hang effekt bank (sfx.bin) olyan hangeffekteket tartalmaz, mint például az ikon választás hang, stb.

| Fájl        | Leírás                                                                                          |
| ----------- | ----------------------------------------------------------------------------------------------- |
| startup.wav | Induláskor játszódik le. Tekintsd meg a [Indítási hang](#startup-sound) szekciót a részletekért |
| back.wav    | Vissza                                                                                          |
| launch.wav  | Játék indításakor játszódik le                                                                  |
| select.wav  | Ez játszódik le, amikor mozgatjuk a kurzort a játékonkénti beállításokban és a választó menüben |
| wrong.wav   | Az oldal végének elérésekor játszódik le                                                        |
| switch.wav  | Oldalak váltásakor játszódik le                                                                 |
| stop.wav    | A DSi témán játszódik le, ha a kiválaszt kurzor abbahagyja a mozgást                            |

Minden fent listázott fájlra szükség van az egyéni hangeffekt bank létrehozásához. Ha valamelyik hangot némítani szeretnéd egy csendes audió fájlt kell használnod. A `.wav` formátum kötelező, és a kódolásnak PCM-nek *kell* lennie.

A hanghatásbank létrehozásához le kell töltened [ezt a](/assets/files/Makefile) fájlt, és az összes `.wav` fájl mellé kell tenned, amelyeket használni fogsz. Miután minden fájl ugyanabban a mappában van, nyisd meg a terminálodat (vagy a parancssort, ha Windows-t használsz), cseréld le az aktuális könyvtárat (`cd`) arra a mappára, ahol a `Makefile` van, majd futtasd a `make` parancsot.

Eredményként létrejön neked az `sfx.bin` fájl, ami bemásolható a `sound` almappába a témád mappáján belül. **Ennek a fájlnak a mérete 512000 B = 512 KB alatt kell legyen**. Bármi nagyobb vagy összeomláshoz vezethet vagy néhány hang nem játszódik le teljesen.

### Indítási hang
Amíg más hang effektusok működnek bármilyen PCM kódolású WAV fájllal, az indítási hangnak egy megadott formátumúnak kell lennie, hogy megfelelően működjön, egyébként szünet lesz az indítási hang vége és a háttérzene kezdete között.

A startup.wav fájl **16-bit 16 kHz** minőségű kell legyen. Használhatod például az [Audacity](https://www.audacityteam.org/download/)-t erre a formátumra konvertáláshoz. Amint a fájl betöltött az Audacity-be, változtasd meg a **Project Rate (Hz)**-et **16000**-re, majd nyomd meg a **Shift+M**-et, és változtasd meg a **Formátum**-ot **16-bit PCM**-re.

Ha a fájlod Sztereó, akkor le kell konvertálnod monóra a **Sávok > Mix > Mix Stereo down to Mono** menüpontban.

Be kell állítanod a `PlayStartupJingle=1` opciót a saját `theme.ini` fájlodban, hogy az indítási zene lejátszódjék.


## Menü BGM
A Menü BGM-nek **16-bit 16 kHz Monó** nyers PCM fájlnak kell lennie. Alább található két metódus arra, hogy audió fájlokat konvertálhass erre a formátumra.

Az sfx.bin-nel ellentétben, a *bgm.pcm.raw* akármekkora nagy lehet.

### ffmpeg
A legegyszerűbb módja zene a TWiLight Menu++-hoz zene konvertálásának, ha futtatod ezt az [ffmpeg](https://ffmpeg.org) parancsot egy terminálban:

```bash
ffmpeg -i [input fájl] -f s16le -acodec pcm_s16le -ac 1 -ar 16k bgm.pcm.raw
```

Cseréld az `[input fájl]` részt a fájl nevére, amit konvertálni szeretnél. Ezt általában megteheted egy terminál ablakban azzal, hogy ráhúzod a fájlt az ablakra, miközben a kurzorral a megfelelő helyen állsz.

### Audacity
Ha nem szeretnéd a parancssort használni, konvertálhatod [Audacity](https://www.audacityteam.org/download/) alkalmazással is.

Az audió konvertálás lépései:
1. Töltsd be a fájlt Audacity-be
1. Ha a fájlod Sztereó, akkor le kell konvertálnod monóra a `Tracks` > `Mix` > `Mix Stereo down to Mono` menüpontban
1. Cseréld a `Project Rate (Hz)`-et bal oldalt alul `16000`-re

A megfelelő formátumban exportáláshoz a következőket tedd:
1. Válaszd a `File` > `Export` > `Export Audio...` opciókat
1. Állítsd a `File Type` opciót `Other uncompressed files`-ra
1. Állítsd a `Header`-t `RAW (header-less)`-re
1. Állítsd az `Encoding`-ot to `Signed 16-bit PCM`-re
1. Állítsd a fájlnevet `bgm.pcm.raw`-ra, majd kattints a `Save` gombra
1. Kattints az `OK`-ra a metaadat szerkesztése ablakban

Most már rendelkezel a `bgm.pcm.raw` fájllal, ami bemásolható a `sound` almappába a témád mappáján belül.

 Ezután a `DSi/3DS téma zene` opciót a TWiLight Menu++ beállításaiban a "Téma" értékre kell állítani, hogy az egyéni BGM lejátszódjon a menüben.
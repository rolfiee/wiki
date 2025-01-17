---
lang: en-US
layout: wiki
section: twilightmenu
category: customization
title: Font Kustom
description: Cara menggunakan font kustom dengan TWiLight Menu++
---

TWiLight Menu++ dapat menggunakan font ubah suai (custom) dengan format NFTR (Nitro FonT Resource). They will be used in Settings, the Manual's titles, and in the Nintendo DSi, Nintendo 3DS, SEGA Saturn, and Homebrew Launcher themes.

### Included font info
There are three fonts included with TWiLight Menu++. When TWiLight Menu++ is running in DSi Mode they all contain all of the characters that should be needed for all of the languages TWiLight is translated to, but when running in DS Mode they are more limited due to RAM limitations. They are as follows:
- Default: This uses the official DSi font as it's primary font and supports all characters that are used in TWiLight Menu++ itself in all languages in DS mode
- Chinese (Simplified): This uses Noto Sans CS as the primary font and has significantly more Chinese (Simplified) characters in DS Mode, at the cost of characters for other languages
- Korean: This is identical to Default in DSi Mode, but in DS Mode has a more complete set of hangul, at the cost of characters for other languages

### Directory structure
Custom fonts are loaded from `sd:/_nds/TWiLightMenu/extras/fonts/[font name]/[font file].nftr` where `[font name]` is whatever name you want and `[font file].nftr` is one of the following:
- `large-ds.nftr`, `large-dsi.nftr`, or `large.nftr`: The larger font used for titles
- `small-ds.nftr`, `small-dsi.nftr`, or `small.nftr`: The smaller font used for most other text

The `-ds` and `-dsi` files have higher priority than the normal one and if found will be used when TWiLight Menu++ is running in DS or DSi Mode respectively.

### Menghasilkan font kustom
You can make your own fonts using a utility such as Pk11's [nftr-editor](https://pk11.us/nftr-editor/). To regenerate one of TWiLight Menu++'s existing fonts using it:
1. Load an NFTR file in nftr-editor
1. Type the names of the fonts you want to use from highest to lowest priority in the `Input font` text box, comma separated
   - You can see a preview of the input fonts in the top box on the left and the current NFTR in the bottom box
1. Click `Generate from font`, then say `OK` to regenerating existing characters and `Cancel` to regenerating the special button characters (ex. &#xE000;)
1. Click `Save`, then repeat for the other sizes

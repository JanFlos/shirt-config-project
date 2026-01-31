
# Master Prompt: LUKO Shirt Configurator

Jsi expert na vývoj moderních webových aplikací v **Nuxt 3** (Vue 3, TypeScript). Tvým úkolem je vytvořit luxusní, responzivní konfigurátor košil pro značku LUKO.

## 1. Technologický Stack
- **Framework:** Nuxt 3
- **State Management:** Pinia
- **Styling:** SCSS (Scoped) - žádný Tailwind, použij vlastní CSS proměnné pro konzistentní design systém.
- **Design:** Moderní, minimalistický, "Glassmorphism" efekty, jemné stíny a animace přechodů.

## 2. Strukturální Požadavky
Aplikace se skládá ze dvou hlavních částí rozdělených na desktopu vedle sebe (na mobilu pod sebou):
1.  **Levá část (Preview):** Interaktivní vizualizace košile.
2.  **Pravá část (Controls):** Krok za krokem konfigurace (Wizard).

### Grafická Vizualizace (Layering System)
Košile se neskládá z jednoho obrázku, ale z vrstev (transparent PNG), které se skládají na sebe pomocí `absolute positioning` a `z-index`.
**Adresářová struktura obrázků (`public/images/`):**
- `/cuts`: `regular.png`, `slim.png`, `extra_slim.png` (Tělo košile)
- `/collars`: `kent.png`, `button_down.png`, `stand_up.png` (Límečky)
- `/sleeves`: `long.png`, `short.png`,`roll-up.png`  (Rukávy)
- `/cuffs`: `rounded.png`, `mitered.png`, `french.png` (Manžety)

**Logika skládání (Z-index odspodu):**
1.  **Sleeves** (Spodní vrstva)
2.  **Cut** (Tělo)
3.  **Cuffs** (Manžety - zobrazit pouze pokud rukáv není krátký)
4.  **Collar** (Límeček - Vrchní vrstva)

## 3. Kroky Konfigurace (Wizard Flow)
Aplikace musí vést uživatele těmito kroky v přesném pořadí:

**Krok 1: Střih a Velikost**
- **UX Požadavek:** Zobrazit možnosti střihu (Regular, Slim, Slim Fit) jako **velké karty s plným náhledem obrázku střihu**, nikoliv jen malé miniatury. Uživatel musí jasně vidět siluetu.
- Výběr velikosti (37-56).

**Krok 2: Materiál a Barva**
- Výběr látky (zobrazit texturu v kroužku).
- Výběr barvy (Color swatches).

**Krok 3: Límeček**
- Seznam typů límečků (Kent, Button-down, Stojáček).

**Krok 4: Rukávy a Manžety**
- Přepínač: Dlouhý / Krátký rukáv.
- Pokud Dlouhý: Výběr manžety (Kulatá, Hranatá, Francouzská).

**Krok 5: Zapínání (Léga)**
- Typy: Standardní, Francouzská, Skrytá. (Bez vizualizace v náhledu, pouze výběr).

**Krok 6: Detaily**
- Kapsa (Checkbox) - (Bez vizualizace).
- Barva knoflíčků.

**Krok 7: Shrnutí a Odeslání**
- Rekapitulace volby (Tabulka).
- **Monogram:** Vstup pro text + výběr fontu.
- **Logo:** Upload obrázku (náhled).
- **Cena:** Dynamický výpočet ceny (Základ + příplatky za materiál, monogram).
- Tlačítko "Odeslat objednávku".

## 4. Backend (Server API)
Vytvoř API endpoint `/api/send-order` (POST request).
- Použij `nodemailer` pro odeslání emailu.
- Údaje pro SMTP (Host, User, Pass) čti z `runtimeConfig` (prostřednictvím `.env`).
- Email musí obsahovat hezky formátované shrnutí objednávky.

## 5. Design Guidelines
- Použij fonty jako *Inter* nebo *Roboto*.
- Hlavní barvy: Tmavě modrá (Navy), Bílá, Akcentní zlatá/Hnědá.
- Tlačítka musí mít hover efekty.
- Přechody mezi kroky musí být animované (`slide-fade`).

## 6. Implementation Notes
- Použij **Pinia** store (`stores/shirt.ts`) pro držení stavu celé konfigurace.
- Všechna data (seznamy materiálů, střihů...) měj definovaná jako konstanty ve storu nebo samostatném souboru, aby byla snadno rozšiřitelná.
- Komponenty rozděl logicky: `ConfiguratorPreview.vue`, `ConfiguratorControls.vue`, `StepFit.vue`, `StepMaterial.vue` atd.

Vygeneruj kompletní strukturu projektu a klíčové soubory.

# Specifikace: Multistep konfigurátor košile

## 1. Přehled projektu

Webová aplikace — vícekrokový konfigurátor košile na míru. Uživatel projde 9 konfiguračními kroky, na konci uvidí shrnutí, vyplní kontaktní údaje a odešle objednávku emailem.

Cílová skupina: mladí lidé (18–35 let). Design musí být moderní, vizuálně atraktivní a působit svěže.

### Fáze projektu

| Fáze       | Název               | Technologie                     | Cíl                                          |
| ---------- | ------------------- | ------------------------------- | -------------------------------------------- |
| **Fáze 0** | Designové prototypy | Čistý HTML + Tailwind CSS (CDN) | 3 vizuální varianty → výběr finálního stylu |
| **Fáze 1** | Implementace        | Nuxt 3 + Pinia + Tailwind       | Plně funkční aplikace ve zvoleném designu    |

Fáze 0 probíhá **před** implementací. Výstupem jsou 3 statické HTML prototypy se shodným obsahem, ale odlišným vizuálním stylem. Zadavatel vybere jeden styl (případně mix prvků z více prototypů) a ten se stane designovým zadáním pro Fázi 1.

### Jazyk UI

Kompletně v češtině. Žádné anglické odborné termíny — vše přeloženo do běžného jazyka nákupu košil.

### Zásada: jeden krok = jedna volba

Každý krok konfigurátoru obsahuje právě jednu volbu. Žádný krok neslučuje více voleb dohromady. Důvod: na mobilním zařízení je omezený prostor a sloučené kroky vedou k nutnosti scrollovat nebo k nepřehlednosti.

### Zásada: jeden obrázek na obrazovce

U kroků s obrázkovými volbami (Střih, Límec, Rukáv, Manžeta) se na obrazovce vždy zobrazuje **jeden velký obrázek** aktuálně vybrané (nebo výchozí první) volby. Uživatel přepíná mezi volbami pomocí **tlačítek/tabů pod obrázkem** — při kliknutí na jinou volbu se obrázek plynule změní. Žádný grid více obrázků vedle sebe. Důvod: na mobilním zařízení je jeden velký obrázek čitelný a přehledný, zatímco 3 malé obrázky v gridu jsou špatně rozpoznatelné.

---

---

# FÁZE 0: DESIGNOVÉ PROTOTYPY

---

## 2. Společné požadavky na všechny prototypy

### Technologie

- **Čistý HTML** — jeden `.html` soubor na prototyp (žádný framework, žádný build step)
- **Tailwind CSS** přes CDN (`<script src="https://cdn.tailwindcss.com">`)
- **Vanilla JavaScript** — pouze pro interaktivitu prototypu (přepínání kroků, výběr karet)
- Žádný backend, žádné odesílání — prototyp je čistě vizuální

### Struktura souborů

```
/prototypes
  prototype-1-glassmorphism.html
  prototype-2-minimal.html
  prototype-3-gradient-cards.html
  /images                          — sdílená složka s obrázky
    /cuts
    /collars
    /cuffs
    /sleeves
```

### Co musí každý prototyp obsahovat

Každý prototyp zobrazuje **všech 9 kroků konfigurátoru** (stačí 2–3 kroky plně interaktivní, zbytek může být statický). Účelem je ukázat **vizuální styl**, ne plnou funkcionalitu.

**Povinné zobrazené kroky (plně interaktivní):**

1. **Krok 2: Střih** — jeden velký obrázek + 3 přepínací tlačítka (ukázka obrázkového kroku)
2. **Krok 6 nebo 7: Barva** — barevné kroužky/swatche (ukázka swatchů)
3. **Krok 9: Shrnutí + formulář** — rekapitulace + kontaktní formulář

**Ostatní kroky:** mohou být statické ukázky (viditelný layout, ale bez funkční navigace).

**Povinné UI prvky v každém prototypu:**

- Stepper / progress bar (9 kroků)
- Navigační tlačítka Zpět / Další
- Karta volby (vybraný a nevybraný stav)
- Barevný swatch (vybraný a nevybraný stav)
- MiniSummary (mini-souhrn dosud zvolených parametrů)
- Kontaktní formulář (povinná/nepovinná pole)
- Mobilní responzivita (funguje na 375px i 1440px)

### Obsah kroků (shodný pro všechny prototypy)

Viz sekce **Fáze 1, bod 9 — Detailní popis kroků konfigurátoru** pro kompletní přehled voleb, obrázků a interních hodnot. Prototypy používají stejná data.

---

## 3. Prototyp 1: Glassmorphism

**Soubor:** `prototype-1-glassmorphism.html`

### Vizuální styl

Poloprůhledné matné sklo na barevném gradientovém pozadí. Efekt hloubky a vrstev.

### Klíčové vlastnosti

- **Pozadí stránky:** Animovaný gradient — jemný přechod dvou/tří barev (modrá → fialová → růžová), pomalá plynulá animace (CSS `@keyframes`), žádné ostré přechody.
- **Karty:** `background: rgba(255, 255, 255, 0.15)`, `backdrop-filter: blur(12px)`, `border: 1px solid rgba(255, 255, 255, 0.2)`, `border-radius: 16px`. Při hoveru opacita stoupne na 0.25.
- **Vybraná karta:** Záře (glow) accent barvou (`box-shadow: 0 0 20px rgba(accent)`), jasný border accent barvou, ikona fajfky.
- **Stepper:** Skleněný pruh nahoře, kroky jako průhledné kroužky s čísly, dokončené vyplněné accent barvou.
- **Navigační tlačítka:** Skleněná tlačítka s jemným hover efektem (světlení).
- **Typografie:** Bílá/světlá na tmavším gradientu. Font: Inter nebo systémový sans-serif.
- **MiniSummary:** Skleněný sidebar (desktop) / skládací pruh (mobil) se seznamem.
- **Barevné swatche:** Kroužky s glassmorphism rámečkem, vybraný s glow efektem.
- **Formulář:** Inputy se skleněným pozadím, jemné border, focus stav s glow.

### Nálada

Futuristická, éterická, prémiová. Připomíná iOS/macOS estetiku.

### Ukázkové CSS hodnoty (Tailwind)

```
Karta:        bg-white/15 backdrop-blur-md border border-white/20 rounded-2xl shadow-lg
Vybraná:      bg-white/25 border-accent ring-2 ring-accent/50 shadow-accent/20
Pozadí:       bg-gradient-to-br from-blue-600 via-purple-600 to-pink-500
Stepper:      bg-white/10 backdrop-blur-sm
Tlačítko:     bg-white/20 hover:bg-white/30 backdrop-blur-sm text-white
```

### Výzva pro kontrast

Zajistit čitelnost textu na poloprůhledném pozadí. Kde je kontrast nedostatečný, zvýšit opacitu karty lokálně (`bg-white/70` pro textové bloky).

---

## 4. Prototyp 2: Minimalistický čistý

**Soubor:** `prototype-2-minimal.html`

### Vizuální styl

Čistý, vzdušný, hodně bílého prostoru. Inspirace: Apple produktové stránky, skandinávský design. Důraz na typografii a obsah, minimum dekorace.

### Klíčové vlastnosti

- **Pozadí stránky:** Čistě bílé (`#FFFFFF`), nebo jemně teplý odstín (`#FAFAF8`).
- **Karty:** Bez viditelného pozadí — pouze jemný border (`border: 1px solid #E5E7EB`) a zaoblení 12px. Hover: jemný stín. Žádné přehnané efekty.
- **Vybraná karta:** Černý/tmavý border (2px), malá fajfka v rohu. Žádné glow, žádné barevné záře. Jednoduchá a jasná indikace.
- **Stepper:** Tenká horizontální čára s kroužky/tečkami. Dokončené: černé vyplněné. Aktuální: černý obrys. Budoucí: šedé. Žádné zbytečné dekorace.
- **Navigační tlačítka:** Černé primární tlačítko ("Další"), šedý text/outline ("Zpět"). Čisté, ploché.
- **Typografie:** Velká, čitelná. Nadpisy tučné, černé. Popis šedý. Font: Inter nebo systémový sans-serif. Výrazná hierarchie velikostí (nadpis kroku: 28–32px, podpis: 16px).
- **MiniSummary:** Jednoduchý seznam s tečkami/ikonami, šedý text, žádné pozadí.
- **Barevné swatche:** Kroužky s tenkým šedým okrajem, vybraný s černým okrajem (2px) a fajfkou uvnitř.
- **Formulář:** Čisté inputy s dolním podtržením (underline styl) nebo jemným borderem. Focus: černý border.

### Nálada

Elegantní, sofistikovaná, klidná. Nic neruší, obsah mluví sám. Profesionální, ale přitom příjemný.

### Ukázkové CSS hodnoty (Tailwind)

```
Karta:        bg-white border border-gray-200 rounded-xl hover:shadow-md transition-shadow
Vybraná:      border-2 border-gray-900 shadow-sm
Pozadí:       bg-white nebo bg-stone-50
Stepper:      border-b border-gray-100 (tenká linka)
Tlačítko:     bg-gray-900 text-white rounded-lg hover:bg-gray-800 (primární)
              text-gray-500 hover:text-gray-900 (sekundární)
```

### Poznámka

Tento styl je nejbezpečnější z hlediska čitelnosti a přístupnosti. Nízké riziko kontrastních problémů.

---

## 5. Prototyp 3: Gradientní karty

**Soubor:** `prototype-3-gradient-cards.html`

### Vizuální styl

Světlé neutrální pozadí, ale karty samotné mají jemné barevné gradienty. Každý krok může mít svou barevnou identitu. Inspirace: moderní fintech/health aplikace (Revolut, Headspace).

### Klíčové vlastnosti

- **Pozadí stránky:** Jemně šedé/krémové (`#F5F5F0` nebo `#F8F9FA`).
- **Karty:** Bílý základ s jemným gradientem na hover/výběr. Nevybraná karta: čistě bílá s tenkým borderem. Vybraná karta: jemný gradient fill (např. `from-blue-50 to-purple-50`) s tmavým borderem.
- **Barevná identita kroků:** Každý krok má svou accent barvu pro aktivní stav stepperu a vybranou kartu:
  - Krok 1 (Materiál): modrá (`blue-500`)
  - Krok 2 (Střih): indigo (`indigo-500`)
  - Krok 3 (Límec): fialová (`violet-500`)
  - Krok 4 (Rukáv): růžová (`pink-500`)
  - Krok 5 (Manžeta): oranžová (`orange-500`)
  - Krok 6 (Knoflíčky): zelená (`emerald-500`)
  - Krok 7 (Barva košile): červená (`rose-500`)
  - Krok 8 (Velikost): teal (`teal-500`)
  - Krok 9 (Shrnutí): šedá (`gray-700`)
- **Stepper:** Kroužky v barvě příslušného kroku, spojené tenkou linkou. Animace přechodu barvy při posunu.
- **Navigační tlačítka:** Tlačítko "Další" má gradient v barvách aktuálního a následujícího kroku. "Zpět" je neutrální.
- **Typografie:** Tmavá (`gray-900`) na světlém pozadí. Accent barvy použity v nadpisech kroků.
- **MiniSummary:** Kompaktní seznam, u každé volby malý barevný tečkový indikátor odpovídající barvě kroku.
- **Barevné swatche:** Větší kroužky (56px), vybraný s gradientním ring efektem.
- **Formulář:** Čisté bílé inputy, focus border v barvě kroku 9 (šedá).

### Nálada

Hravá, přívětivá, barevná ale ne přeplácená. Každý krok má svou osobnost. Působí moderně a přátelsky.

### Ukázkové CSS hodnoty (Tailwind)

```
Karta:        bg-white border border-gray-200 rounded-2xl shadow-sm hover:shadow-md
Vybraná (krok 1): bg-gradient-to-br from-blue-50 to-blue-100 border-2 border-blue-400
Vybraná (krok 4): bg-gradient-to-br from-pink-50 to-pink-100 border-2 border-pink-400
Pozadí:       bg-gray-50
Stepper:      gap-2 (kroužky v barvě kroku, linka šedá)
Tlačítko:     bg-gradient-to-r from-blue-500 to-violet-500 text-white rounded-xl
```

### Poznámka

Barevná identita kroků může být i jemnější (jen stepper + border vybrané karty). Nemusí být přehnaně pestrá — jemné odstíny stačí.

---

## 6. Hodnotící kritéria pro výběr prototypu

Po vytvoření všech 3 prototypů zadavatel vybere finální styl na základě těchto kritérií:

| Kritérium                 | Popis                                                           |
| ------------------------- | --------------------------------------------------------------- |
| **Vizuální přitažlivost** | Který styl nejlépe osloví cílovou skupinu (mladí 18–35)?        |
| **Čitelnost a kontrast**  | Je text všude dobře čitelný? Splňuje WCAG AA?                   |
| **Mobilní fungování**     | Vypadá prototyp dobře na 375px šířce?                           |
| **Rozlišitelnost stavů**  | Je jasně vidět, co je vybrané, co ne, co je disabled?           |
| **Celkový dojem**         | Působí prototyp jako moderní aplikace, nebo jako zastaralý web? |

Výstupem je jedno z:

- **Celý prototyp** — styl se přenese 1:1 do Nuxt implementace.
- **Mix** — kombinace prvků z více prototypů (např. layout z P1, barvy z P3, tlačítka z P2).
- **Variace** — vybraný prototyp s úpravami (např. P3 ale s jemnějšími gradienty).

---

---

# FÁZE 1: IMPLEMENTACE V NUXT 3

---

## 7. Technologie

- **Framework:** Nuxt 3
- **State management:** Pinia store
- **Stylování:** Tailwind CSS
- **Design:** Podle vybraného prototypu z Fáze 0 (viz sekce 2–5). Všechny designové hodnoty (barvy, zaoblení, stíny, efekty) se přenesou z vybraného prototypu.
- **Jazyk UI:** Kompletně v češtině.

### Poznámky k designu (ergonomie)

- **Kontrast:** Všechny texty musí splňovat WCAG AA (kontrastní poměr min. 4.5:1). Pokud vybraný prototyp má problematický kontrast (Glassmorphism), musí se lokálně zvýšit opacita/světlost pozadí.
- **Jednoduchost kroků:** Každý krok obsahuje právě jednu volbu. Žádný krok neslučuje více voleb.
- **Průběžný přehled:** V každém kroku je vedle obsahu (desktop) nebo nad ním (mobil) viditelný mini-souhrn dosud zvolených parametrů.

---

## 8. Architektura aplikace

### 8.1 Adresářová struktura (doporučená)

```
/pages
  index.vue                     — hlavní stránka s konfigurátorem
/components
  ConfiguratorStepper.vue       — navigace kroků (stepper/progress bar)
  StepMaterial.vue              — Krok 1: Materiál
  StepCut.vue                   — Krok 2: Střih
  StepCollar.vue                — Krok 3: Límec
  StepSleeve.vue                — Krok 4: Rukáv
  StepCuff.vue                  — Krok 5: Manžeta
  StepButtonColor.vue           — Krok 6: Barva knoflíčků
  StepShirtColor.vue            — Krok 7: Barva košile
  StepSize.vue                  — Krok 8: Velikost
  StepSummary.vue               — Krok 9: Shrnutí a kontaktní formulář
  OptionCard.vue                — Univerzální karta/tlačítko volby (textová karta nebo přepínací tlačítko pod obrázkem)
  ColorSwatch.vue               — Barevný kroužek/čtverec pro výběr barvy
  ShirtPreview.vue              — Náhled košile s přebarvením (zobrazuje se pouze v kroku 7: Barva košile)
  MiniSummary.vue               — Průběžný mini-souhrn dosud zvolených parametrů
/stores
  configurator.ts               — Pinia store s celým stavem konfigurátoru
/config
  app.config.ts                 — Konfigurační soubor (email příjemce, testovací režim, pořadí kroků)
/public/images
  /cuts                         — regular.png, slim.png, extra-slim.png
  /collars                      — stand_up.png, button_down.png, kent.png
  /cuffs                        — rounded.png, mitered.png, french.png
  /sleeves                      — long.png, short.png, roll-up.png
```

### 8.2 Pinia Store (`configurator.ts`)

Centrální stav celé konfigurace. Store obsahuje:

```
state:
  currentStep: number           — aktuální krok (1–9)
  material: string | null       — vybraný materiál
  cut: string | null            — vybraný střih
  collar: string | null         — vybraný límec
  sleeve: string | null         — vybraný rukáv
  cuff: string | null           — vybraná manžeta
  shirtColor: string | null     — vybraná barva košile
  buttonColor: string | null    — vybraná barva knoflíčků
  sizeType: 'letter' | 'number' — typ velikosti (konfekční / číselná)
  size: string | null           — vybraná velikost
  contact:
    firstName: string           — jméno (povinné)
    lastName: string            — příjmení (povinné)
    phone: string               — telefon (nepovinné)
    email: string               — email (povinný)
    note: string                — poznámka (nepovinná)

getters:
  isStepValid: boolean          — validace aktuálního kroku
  summaryText: string           — textové shrnutí konfigurace
  canProceed: boolean           — zda lze přejít na další krok
  completedChoices: object      — objekt dosud zvolených parametrů pro MiniSummary

actions:
  nextStep()                    — přechod na další krok
  prevStep()                    — přechod na předchozí krok
  goToStep(n)                   — skok na konkrétní krok (pouze pokud předchozí jsou vyplněny)
  reset()                       — reset celé konfigurace
  submitOrder()                 — odeslání objednávky emailem
```

---

## 9. Detailní popis kroků konfigurátoru

---

### Krok 1: Materiál

**Zobrazení:** Dvě textové karty vedle sebe (OptionCard).

| Volba                      | Interní hodnota    |
| -------------------------- | ------------------ |
| 60% bavlna / 40% polyester | `bavlna-polyester` |
| 100% bavlna Easy           | `bavlna-100`       |

- Žádný obrázek — pouze název materiálu.

**Validace kroku:** Tlačítko "Další" je aktivní po výběru materiálu.

---

### Krok 2: Střih

**Zobrazení:** Jeden velký obrázek aktuálně vybrané volby + řada přepínacích tlačítek pod ním.

| Volba    | Obrázek                       | Interní hodnota |
| -------- | ----------------------------- | --------------- |
| Regular  | `/images/cuts/regular.png`    | `regular`       |
| Slim     | `/images/cuts/slim.png`       | `slim`          |
| Slim Fit | `/images/cuts/extra-slim.png` | `slim-fit`      |

- Obrázek zabírá hlavní prostor obrazovky. Pod ním 3 tlačítka/taby s názvy voleb.
- Výchozí stav: zobrazen obrázek první volby (Regular). Po kliknutí na jiné tlačítko se obrázek plynule změní (fade/crossfade přechod).
- Vybraný střih určuje **základní obrázek košile** pro krok barvy (krok 7).

**Validace kroku:** Tlačítko "Další" je aktivní po výběru střihu.

---

### Krok 3: Límec

**Zobrazení:** Jeden velký obrázek aktuálně vybrané volby + řada přepínacích tlačítek pod ním.

| Volba                  | Obrázek                           | Interní hodnota |
| ---------------------- | --------------------------------- | --------------- |
| Stojáček               | `/images/collars/stand_up.png`    | `stojacek`      |
| Propnutý (Button Down) | `/images/collars/button_down.png` | `propnuty`      |
| Kent                   | `/images/collars/kent.png`        | `kent`          |

- Obrázek zabírá hlavní prostor obrazovky. Pod ním 3 tlačítka/taby s názvy voleb.
- Výchozí stav: zobrazen obrázek první volby (Stojáček). Po kliknutí na jiné tlačítko se obrázek plynule změní.

**Validace kroku:** Tlačítko "Další" je aktivní po výběru límce.

---

### Krok 4: Rukáv

**Zobrazení:** Jeden velký obrázek aktuálně vybrané volby + řada přepínacích tlačítek pod ním.

| Volba     | Obrázek                       | Interní hodnota |
| --------- | ----------------------------- | --------------- |
| Dlouhý    | `/images/sleeves/long.png`    | `dlouhy`        |
| Krátký    | `/images/sleeves/short.png`   | `kratky`        |
| Ohrnovací | `/images/sleeves/roll-up.png` | `ohrnovaci`     |

- Obrázek zabírá hlavní prostor obrazovky. Pod ním 3 tlačítka/taby s názvy voleb.
- Výchozí stav: zobrazen obrázek první volby (Dlouhý). Po kliknutí na jiné tlačítko se obrázek plynule změní.

**Validace kroku:** Tlačítko "Další" je aktivní po výběru rukávu.

---

### Krok 5: Manžeta

**Zobrazení:** Jeden velký obrázek aktuálně vybrané volby + řada přepínacích tlačítek pod ním.

| Volba                          | Obrázek                     | Interní hodnota |
| ------------------------------ | --------------------------- | --------------- |
| Kulatá                         | `/images/cuffs/rounded.png` | `kulata`        |
| Hranatá                        | `/images/cuffs/mitered.png` | `hranata`       |
| Ohrnovací na manžetový knoflík | `/images/cuffs/french.png`  | `ohrnovaci`     |

- Obrázek zabírá hlavní prostor obrazovky. Pod ním 3 tlačítka/taby s názvy voleb.
- Výchozí stav: zobrazen obrázek první volby (Kulatá). Po kliknutí na jiné tlačítko se obrázek plynule změní.

**Validace kroku:** Tlačítko "Další" je aktivní po výběru manžety.

---

### Krok 6: Barva knoflíčků

**Zobrazení:** Čtyři barevné kroužky (ColorSwatch).

| Volba | Barva     | Interní hodnota |
| ----- | --------- | --------------- |
| Bílý  | `#FFFFFF` | `bily`          |
| Černý | `#1a1a1a` | `cerny`         |
| Modrý | `#2563eb` | `modry`         |
| Šedý  | `#9ca3af` | `sedy`          |

- Knoflíčky se vizuálně na náhledu košile nezobrazují (nejsou obrázky) — výběr slouží pouze pro objednávku.

**Validace kroku:** Tlačítko "Další" je aktivní po výběru barvy knoflíčků.

---

### Krok 7: Barva košile

**Zobrazení:** Pět barevných voleb. Náhled (ShirtPreview) zobrazuje **bílou verzi obrázku střihu** (z kroku 2) s CSS přebarvením.

| Volba           | CSS barva (orientační) | Interní hodnota   |
| --------------- | ---------------------- | ----------------- |
| Bílá            | `#FFFFFF` (bez filtru) | `bila`            |
| Černá           | `#1a1a1a`              | `cerna`           |
| Královská modrá | `#1e3a8a`              | `kralovska-modra` |
| Světle šedá     | `#d1d5db`              | `svetle-seda`     |
| Světle modrá    | `#93c5fd`              | `svetle-modra`    |

**Technické řešení přebarvení:**

- Základní obrázek je bílá košile (obrázek střihu z `/images/cuts/`).
- Na bílou košili se aplikuje CSS filtr nebo overlay technika:
  - Varianta A: CSS `filter: brightness() sepia() saturate() hue-rotate()` kombinace pro jednotlivé barvy.
  - Varianta B: Překrytí obrázku div elementem s `mix-blend-mode: multiply` a příslušnou barvou pozadí.
- Pro bílou barvu se neaplikuje žádný filtr.
- Každá barva bude mít předem definovanou sadu CSS hodnot.

**Výběr UI:** Barevné kroužky (ColorSwatch) s názvem barvy pod nimi. Náhled košile se živě mění podle vybrané barvy.

**Validace kroku:** Tlačítko "Další" je aktivní po výběru barvy košile.

---

### Krok 8: Výběr velikosti

**Zobrazení:** Dva režimy výběru (přepínač/taby).

#### Režim A: Konfekční velikost (písmenná)

**Záložka:** "Konfekční velikost"

| Velikost | Obvod krku |
| -------- | ---------- |
| S        | 37/38 cm   |
| M        | 39/40 cm   |
| L        | 41/42 cm   |
| XL       | 43/44 cm   |
| XXL      | 45/46 cm   |
| 3XL      | 47/48 cm   |
| 4XL      | 49/50 cm   |
| 5XL      | 51/52 cm   |

- **Desktop/Tablet:** Zobrazí se jako karty/tlačítka s písmenem velikosti a pod ním orientační obvod krku (grid 4 sloupce).
- **Mobil:** Kompaktní grid tlačítek (3 sloupce, výška tlačítka cca 56px). Každé tlačítko obsahuje písmeno velikosti a pod ním menším fontem obvod krku. Celý výběr se vejde na jednu obrazovku bez scrollu.

#### Režim B: Číselná velikost (podle obvodu krku)

**Záložka:** "Podle obvodu krku"

| Velikost |
| -------- |
| 37/38    |
| 39/40    |
| 41/42    |
| 43/44    |
| 45/46    |
| 47/48    |
| 49/50    |
| 51/52    |
| 53/54    |
| 55/56    |

- **Desktop/Tablet:** Zobrazí se jako karty/tlačítka s číslem (grid 5 sloupců).
- **Mobil:** Kompaktní grid tlačítek (3 sloupce, výška tlačítka cca 48px). Celý výběr (10 velikostí) se vejde na jednu obrazovku bez scrollu.
- Číselná škála zahrnuje navíc velikosti 53/54 a 55/56 (nemají ekvivalent v písmenné).

**UI:** Přepínač nad volbami — dvě záložky: "Konfekční velikost" / "Podle obvodu krku". Při přepnutí se změní sada voleb. Pokud uživatel vybral velikost v jednom režimu a přepne na druhý, výběr se zachová pokud existuje ekvivalent (např. S ↔ 37/38), jinak se resetuje.

**Validace kroku:** Tlačítko "Další" je aktivní po výběru velikosti v kterémkoli režimu.

---

### Krok 9: Shrnutí a odeslání

**Zobrazení se dělí na dvě části:**

#### Část A: Rekapitulace konfigurace

**Desktop/Tablet:** Přehledná tabulka/seznam všech zvolených parametrů, vždy viditelná.

**Mobil:** Rekapitulace je zobrazena jako **sbalitelný akordeon** (defaultně sbalený) s nadpisem "Vaše konfigurace" a šipkou pro rozbalení. Důvod: formulář pod rekapitulací musí být co nejdříve viditelný, aby uživatel nemusel scrollovat.

Přehledná tabulka/seznam všech zvolených parametrů:

- Materiál: [hodnota]
- Střih: [hodnota]
- Límec: [hodnota]
- Rukáv: [hodnota]
- Manžeta: [hodnota]
- Barva knoflíčků: [hodnota] (s barevným kroužkem)
- Barva košile: [hodnota] (s barevným kroužkem)
- Velikost: [hodnota + typ]

U každého řádku ikona tužky / odkaz "Upravit" — kliknutím se uživatel vrátí na příslušný krok:

- Materiál → krok 1
- Střih → krok 2
- Límec → krok 3
- Rukáv → krok 4
- Manžeta → krok 5
- Barva knoflíčků → krok 6
- Barva košile → krok 7
- Velikost → krok 8

#### Část B: Kontaktní formulář

| Pole     | Typ      | Povinné | Validace                         |
| -------- | -------- | ------- | -------------------------------- |
| Jméno    | text     | Ano     | min. 2 znaky                     |
| Příjmení | text     | Ano     | min. 2 znaky                     |
| Telefon  | tel      | Ne      | formát českého telefonního čísla |
| Email    | email    | Ano     | validní formát emailu            |
| Poznámka | textarea | Ne      | max. 500 znaků                   |

**Tlačítko "Odeslat objednávku"** — aktivní pouze při vyplněných povinných polích.

#### Mobilní optimalizace formuláře

- Tlačítko "Odeslat objednávku" je na mobilu **sticky na spodní hraně** (`position: sticky; bottom: 0`), viditelné i při vysunuté klávesnici.
- Formulářová pole mají správné `inputmode` atributy: `inputmode="tel"` pro telefon, `inputmode="email"` pro email.
- Po tapnutí na pole se formulář automaticky odscrolluje tak, aby aktivní pole bylo viditelné nad klávesnicí.
- Pole Jméno a Příjmení mohou být na mobilu vedle sebe (grid 2 sloupce) pro úsporu místa.

---

## 10. Navigace a stepper

### Progress bar / Stepper

#### Desktop / Tablet

- Zobrazený nahoře na stránce, vždy viditelný.
- 9 kroků vizuálně znázorněno (ikony nebo čísla + názvy):
  1. Materiál
  2. Střih
  3. Límec
  4. Rukáv
  5. Manžeta
  6. Knoflíčky
  7. Barva
  8. Velikost
  9. Shrnutí
- Dokončené kroky: zvýrazněné (jiná barva + ikona fajfky).
- Aktuální krok: výrazně zvýrazněný.
- Budoucí kroky: šedé, neklikatelné (dokud nejsou předchozí vyplněny).
- Kliknutím na dokončený krok se uživatel vrátí na daný krok.

#### Mobil

- Stepper se na mobilu zjednodušuje — 9 pojmenovaných bodů se na šířku 320–390px nevejde.
- Zobrazí se **kompaktní progress bar**: tenký vyplněný pruh s textem **"Krok 3 / 9"**.
- Pod progress barem **název aktuálního kroku** (např. "Límec").
- Tapnutím na progress bar se rozbalí overlay/dropdown se seznamem všech kroků (dokončené klikatelné, budoucí šedé). Tap mimo overlay ho zavře.
- Celý mobilní stepper zabírá max. 2 řádky výšky (~48–56px).

### Navigační tlačítka

- **Zpět** (vlevo) — návrat na předchozí krok. Skryté v 1. kroku.
- **Další** (vpravo) — přechod na další krok. Aktivní pouze pokud je volba v aktuálním kroku vyplněna.
- Animovaný přechod (slide vlevo/vpravo podle směru navigace).

#### Pozice na mobilu

- Tlačítka "Zpět" a "Další" jsou na mobilu **sticky na spodní hraně obrazovky** (`position: sticky; bottom: 0`).
- Tenký pruh ve stylu vybraného prototypu, aby nezakrýval obsah, ale byl vždy dostupný.
- Výška pruhu max. 56px, tlačítka vedle sebe (Zpět vlevo, Další vpravo).
- Obsah kroku má `padding-bottom` odpovídající výšce sticky pruhu, aby se poslední karta nepřekrývala.

#### Auto-advance na mobilu

- U kroků s jedním výběrem z mála možností (Materiál, Střih, Límec, Rukáv, Manžeta, Barva knoflíčků, Barva košile) se po výběru volby automaticky přejde na další krok po krátké prodlevě (400ms) s jemnou vizuální zpětnou vazbou (vybraná karta se krátce zvýrazní, pak slide přechod).
- Uživatel může stále použít tlačítko "Zpět" pokud se chce vrátit.
- Auto-advance se neaplikuje na krok 8 (Velikost — přepínač režimů).

---

## 11. Komponenta MiniSummary (průběžný přehled)

- Zobrazuje se od kroku 2 výše (v kroku 1 není co shrnovat).
- **Desktop:** Boční panel (sidebar) vedle hlavního obsahu kroku.
- **Mobil:** Skládací lišta nad krokem (tap pro rozbalení/sbalení), defaultně sbalená.
- Obsahuje pouze parametry, které už uživatel zvolil, v kompaktní formě:
  - Materiál: 60% bavlna / 40% polyester
  - Střih: Regular
  - Límec: Kent
  - ... (další přibývají s každým krokem)
- U barev se vedle textu zobrazí malý barevný kroužek.
- Kliknutím na položku v MiniSummary se uživatel vrátí na příslušný krok.

---

## 12. Design a UX specifikace

### Vizuální styl

Vizuální styl celé aplikace vychází z prototypu vybraného ve Fázi 0. Všechny designové hodnoty — barvy, zaoblení rohů, stíny, efekty, typografie — se přenesou z vybraného prototypu (nebo mixu prototypů) do Tailwind konfigurace.

### Interakce

- Hover na kartách: efekt podle vybraného stylu (zvětšení / stín / glow / posun).
- Vybraná karta: jasná vizuální indikace (border, výplň, ikona, glow — dle stylu).
- Přechody mezi kroky: slide animace (`transition` 300–400ms).
- Tlačítka: hover efekt, disabled stav (šedé, `cursor-not-allowed`).

### Responzivita

- **Desktop:** karty vedle sebe (grid 3 sloupce), MiniSummary jako sidebar vpravo.
- **Tablet:** karty 2 sloupce, MiniSummary nad krokem (sbalitelná).
- **Mobil:**
  - Obrázkové kroky (střih, límec, rukáv, manžeta): **jeden velký obrázek** (plná šířka) + řada přepínacích tlačítek pod ním. Tlačítka min. 44px výška, v jedné řadě vedle sebe.
  - Textové karty bez obrázků (materiál): plná šířka, vyšší karty s textem na střed.
  - Barevné kroužky (barva košile, knoflíčky): **inline řada** vedle sebe (flex-wrap), kroužky min. 48×48px s názvem pod nimi.
  - MiniSummary jako sbalitelná lišta nahoře (pod stepperem).

---

## 13. Odesílání emailu

### Konfigurace (`app.config.ts` nebo `.env`)

```
EMAIL_RECIPIENT=adresa@priklad.cz     — cílová emailová adresa
TEST_MODE=true                         — testovací režim (true/false)
```

### Obsah emailu

**Předmět:** `[Konfigurátor košile] Nová objednávka — {jméno} {příjmení}`

V testovacím režimu předmět: `[TEST — Konfigurátor košile] Testovací objednávka — {jméno} {příjmení}`

**Tělo emailu:**

```
===================================================
⚠️ TESTOVACÍ REŽIM — Toto NENÍ skutečná objednávka
(Tento řádek se zobrazuje pouze při TEST_MODE=true)
===================================================

KONFIGURACE KOŠILE
-------------------
Materiál:        60% bavlna / 40% polyester
Střih:           Regular
Límec:           Kent
Rukáv:           Dlouhý
Manžeta:         Kulatá
Barva košile:    Světle modrá
Barva knoflíčků: Bílý
Velikost:        L (konfekční) / 41/42 cm

KONTAKTNÍ ÚDAJE
-------------------
Jméno:           Jan Novák
Telefon:         +420 123 456 789
Email:           jan@priklad.cz
Poznámka:        Prosím o rychlé dodání

===================================================
⚠️ TESTOVACÍ REŽIM — Nejedná se o skutečnou objednávku!
(Tento řádek se zobrazuje pouze při TEST_MODE=true)
===================================================
```

### Technické řešení odesílání

- Nuxt server route (`/api/send-order`) — API endpoint pro odeslání emailu.
- Na backendu použít knihovnu pro odesílání emailu (např. `nodemailer` nebo Nuxt modul `nuxt-mail`).
- Endpoint přijme POST s daty konfigurace a kontaktu, sestaví email a odešle na nakonfigurovanou adresu.
- Po úspěšném odeslání zobrazit uživateli potvrzovací obrazovku s textem "Děkujeme, vaše konfigurace byla odeslána."
- Po neúspěšném odeslání zobrazit chybovou hlášku a možnost zkusit znovu.

---

## 14. Validace a chybové stavy

| Situace                           | Chování                                                        |
| --------------------------------- | -------------------------------------------------------------- |
| Krok bez výběru                   | Tlačítko "Další" je neaktivní (disabled).                      |
| Přeskočení kroku přes URL         | Přesměrování na první nevyplněný krok                          |
| Povinné pole ve formuláři prázdné | Červený rámeček, chybová hláška pod polem                      |
| Email špatný formát               | "Zadejte platnou emailovou adresu"                             |
| Odeslání selhalo                  | Toast/banner: "Odeslání se nezdařilo. Zkuste to prosím znovu." |
| Odeslání úspěšné                  | Přechod na potvrzovací obrazovku                               |

---

## 15. Potvrzovací obrazovka (po odeslání)

- Ikona úspěchu (zelená fajfka).
- Text: "Děkujeme! Vaše konfigurace košile byla úspěšně odeslána."
- Podtext: "Na emailovou adresu {email} jsme odeslali potvrzení." (pokud je to implementováno)
- Tlačítko: "Vytvořit novou konfiguraci" → reset store a návrat na krok 1.

---

## 16. Konfigurovatelné pořadí kroků

### Požadavek

Pořadí kroků 2–8 (tedy všech kroků mezi prvním krokem "Materiál" a posledním krokem "Shrnutí") musí být flexibilně konfigurovatelné prostřednictvím konfiguračního souboru. Krok 1 (Materiál) je vždy první. Krok 2 (Střih) musí být vždy před krokem 7 (Barva košile), protože střih určuje základní obrázek pro náhled přebarvení.

### Konfigurační soubor (`app.config.ts` nebo samostatný `steps.config.ts`)

```
stepsOrder: [
  'material',          // Krok 1 — vždy první, nelze přesunout
  'cut',               // výchozí krok 2
  'collar',            // výchozí krok 3
  'sleeve',            // výchozí krok 4
  'cuff',              // výchozí krok 5
  'button-color',      // výchozí krok 6
  'shirt-color',       // výchozí krok 7
  'size',              // výchozí krok 8
  'summary'            // výchozí krok 9 — vždy poslední, nelze přesunout
]
```

- `material` je vždy na pozici 1 (fixní).
- `summary` je vždy na poslední pozici (fixní).
- Kroky `cut`, `collar`, `sleeve`, `cuff`, `button-color`, `shirt-color` a `size` mohou být v libovolném pořadí (s omezením: `cut` musí být před `shirt-color`).
- Stepper, navigace a validace se dynamicky přizpůsobí nakonfigurovanému pořadí.
- MiniSummary zobrazuje parametry v pořadí, v jakém je uživatel skutečně volil (podle konfigurace kroků).

### Implementace

- Pinia store a komponenta stepperu musí číst pořadí kroků z konfigurace.
- Mapování `stepOrder[index]` → komponenta kroku (StepCut, StepCollar, StepSleeve, StepCuff, StepButtonColor, StepShirtColor, StepSize).
- Navigace (nextStep, prevStep, goToStep) pracuje s pořadím z konfigurace, ne s pevnými čísly.
- Stepper zobrazuje názvy kroků v pořadí z konfigurace.
- Validace `isStepValid` se dynamicky řídí podle toho, který krok je aktuálně na dané pozici.
- Odkazy "Upravit" v kroku Shrnutí a MiniSummary musí odkazovat na správnou pozici kroku podle aktuální konfigurace.
- Validace konfigurace: při startu aplikace ověřit, že `cut` je v poli před `shirt-color` (jinak chyba/warning).

---

## 17. Stavová logika a omezení

- Uživatel nemůže přeskočit krok — musí projít kroky postupně (v pořadí dle konfigurace).
- Uživatel se může vracet na předchozí kroky a měnit volby.
- Při změně volby v dřívějším kroku se následující kroky neresetují (uživatel si ponechá svůj výběr), pokud změna nemá vliv na dostupné možnosti.
- Store přežívá reload stránky (persist plugin pro Pinia, uložení do `localStorage`).

---

## 18. Shrnutí datového toku

```
[Krok 1: Materiál]
       ↓
  uložení do store

[Krok 2: Střih]
       ↓
  uložení do store, obrázek střihu → základ pro přebarvení v kroku 7

[Krok 3: Límec]
       ↓
  uložení do store

[Krok 4: Rukáv]
       ↓
  uložení do store

[Krok 5: Manžeta]
       ↓
  uložení do store

[Krok 6: Barva knoflíčků]
       ↓
  uložení do store

[Krok 7: Barva košile]
       ↓
  obrázek střihu (z kroku 2) + CSS barva = náhled košile

[Krok 8: Velikost]
       ↓
  uložení do store

[Krok 9: Shrnutí + formulář] → POST /api/send-order → Email s konfigurací
```

Poznámka: Čísla kroků výše odpovídají výchozímu pořadí. Při změně konfigurace se mění pořadí, ale datový tok zůstává stejný — střih vždy určuje základ náhledu pro barvu košile.

---

## 19. Klíčové implementační poznámky

1. **Obrázky:** Všechny obrázky jsou ve formátu PNG s průhledným pozadím (důležité pro CSS přebarvení v kroku barvy).
2. **CSS přebarvení:** Bílé obrázky košil jsou ideální základ pro `mix-blend-mode: multiply` — bílé oblasti převezmou barvu overlay vrstvy.
3. **Pinia persist:** Použít `pinia-plugin-persistedstate` pro ukládání stavu do `localStorage`.
4. **Email:** Server route `/api/send-order` musí číst konfiguraci `TEST_MODE` a `EMAIL_RECIPIENT` z runtime configu/env proměnných.
5. **Přechody:** Použít Vue `<Transition>` komponentu s dynamickým názvem animace podle směru (vpřed/zpět).
6. **Přístupnost:** Všechny volby musí být přístupné klávesnicí. Obrázky musí mít `alt` texty v češtině.
7. **Kontrast:** Splnění WCAG AA dle požadavků vybraného prototypu. Glassmorphism vyžaduje lokální úpravu opacity.
8. **MiniSummary:** Komponenta čte data z Pinia store (getter `completedChoices`) a dynamicky zobrazuje pouze vyplněné parametry.
9. **Auto-advance:** Na mobilu u jednoduchých kroků (1–7) se po výběru automaticky přejde na další krok. Na desktopu se neaplikuje. Neaplikuje se na krok 8 (Velikost — přepínač režimů).

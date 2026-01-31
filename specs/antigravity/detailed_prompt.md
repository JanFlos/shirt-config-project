# Zadání pro AI vývojáře: Konfigurátor Košil (Nuxt 3 + Pinia + Tailwind)

## 1. Přehled projektu

Vytvoř webovou aplikaci pro konfiguraci košil na míru. Aplikace bude fungovat jako "wizard" (průvodce), který uživatele provede jednotlivými kroky výběru. Důraz je kladen na moderní "Glassmorphism" design, plynulé animace a skvělý UX na mobilech i desktopu.

**Jazyk aplikace:** Čeština.

## 2. Fáze 0: HTML/JS Prototyp (Validace vizuálu)

Před samotnou implementací do Nuxtu vytvořte jednoduchý statický prototyp (jedna HTML stránka + CSS + JS), který ověří vizuální směr.

**Experimentování se styly (Git Worktrees):**
Vytvořte **5 git worktrees** (např. v adresářích `proto-minimal`, `proto-glass`, `proto-bold`, `proto-dark`, `proto-luxury`) a v každém implementujte odlišnou vizuální variantu:

- **Vytvořte hlavní rozcestník (`index.html`)**, ze kterého bude možné navigovat na jednotlivé prototypy.

1. **Minimalistický:** Hodně bílé místo, tenké linky, čistá typografie.
2. **Glassmorphism (výchozí):** Výrazné rozostření, poloprůhledné karty, gradienty na pozadí.
3. **Bold / Modern:** Velká písma, vysoký kontrast, ostré stíny.
4. **Dark Mode:** Tmavá paleta, neonové akcenty nebo tlumené luxusní barvy.
5. **Luxury / Elegant:** Patkové písmo (Serif), zlaté/hnědé akcenty, klasický vzhled.

**Cíl:** Rychle porovnat 5 různých přístupů vedle sebe a vybrat vítěze pro finální implementaci.

**Technologie pro prototyp:**

- Čisté HTML5
- Tailwind CSS (přes CDN pro rychlost)
- Vanilla JavaScript (pro jednoduchou interaktivitu)
- Barvení košile: Funkčnost CSS mix-blend-mode nebo filtrů na bílém podkladu.

## 3. Technologický Stack (Finální aplikace)

- **Frontend:** Nuxt 3 (Vue 3)
- **State Management:** Pinia (pro uchování stavu konfigurace mezi kroky)
- **Styling:** Tailwind CSS (využití utility classes pro glassmorphism, stíny, animace)
- **Ikony:** Lucide-vue-next, Heroicons nebo podobné (pro UI prvky)

## 4. Designové požadavky

- **Vzhled:** Minimalistický, čistý, prémiový.
- **Efekty:** Glassmorphism – poloprůhledná pozadí s rozostřením (backdrop-blur), jemné bílé ohraničení (border-white/20), výrazné stíny pro hloubku.
- **Přístupnost a Kontrast (CRITICAL):**
  - Text na kartách s Glassmorphism efektem **MUSÍ splňovat WCAG AA standard (kontrast min. 4.5:1)**.
  - **Řešení:** Pokud je pozadí gradient nebo příliš světlé, použijte vyšší opacitu pozadí karet (např. `bg-white/70` místo `bg-white/25`) nebo přidejte pod text tmavší poloprůhledný podklad.
  - Cílová skupina (muži 30-60 let) vyžaduje perfektní čitelnost.
- **Animace:** Plynulé přechody mezi kroky (fade/slide). Interaktivní prvky musí reagovat na hover/click (scale efekt).
- **Responzivita:** Plně přizpůsobitelné pro mobilní zařízení i desktop.

## 5. Konfigurační kroky (Workflow)

Aplikace bude mít následující sekvenční kroky. Uživatel postupuje lineárně, ale může se vracet. Data se ukládají do Pinia storu.

### Krok 1: Výběr materiálu a střihu

Tento krok obsahuje dvě podsekce.
**Sekce A: Materiál**

- **Možnosti:**
  1. `60% Bavlna / 40% Polyester`
  2. `100% Bavlna Easy Care`
- **UI:** Interaktivní karty s názvem materiálu.

**Sekce B: Střih (Fit)**

- **Možnosti:**
  1. `REGULAR`
  2. `SLIM`
  3. `SLIM FIT`
- **Vizualizace:**
  - Zobrazit obrázek příslušného střihu ze složky `/images/cuts`:
    - REGULAR -> `regular.png`
    - SLIM -> `slim.png`
    - SLIM FIT -> `extra-slim.png`

### Krok 2: Výběr límce a manžety

Tento krok obsahuje dvě podsekce.
**Sekce A: Límec**

- **Možnosti:**
  1. `Stojáček`
  2. `Propnutý (Button Down)`
  3. `Kent`
- **Vizualizace:**
  - Zobrazit obrázek ze složky `/images/collars`:
    - Stojáček -> `stand_up.png`
    - Propnutý -> `button_down.png`
    - Kent -> `kent.png`

**Sekce B: Manžeta**

- **Možnosti:**
  1. `Kulatá`
  2. `Hranatá`
  3. `Ohrnovací (na manžetový knoflík)`
- **Vizualizace:**
  - Zobrazit obrázek ze složky `/images/cuffs`:
    - Kulatá -> `rounded.png`
    - Hranatá -> `mitered.png`
    - Ohrnovací -> `french.png`

### Krok 3: Výběr rukávu

- **Možnosti:**
  1. `Dlouhý`
  2. `Krátký`
  3. `Ohrnovací`
- **Vizualizace:**
  - Zobrazit obrázek ze složky `/images/sleeves`:
    - Dlouhý -> `long.png`
    - Krátký -> `short.png`
    - Ohrnovací -> `roll-up.png`

### Krok 4: Barva košile

- **Možnosti:**
  1. Bílá
  2. Černá
  3. Královská modrá
  4. Světle šedá
  5. Světle modrá
- **Vizualizace (Klíčová funkčnost):**
  - Jako podklad použij obrázek košile vybrané v **Kroku 1 (sekce Střih)** (protože střih definuje tvar těla).
  - Pomocí CSS (např. `filter`, `mix-blend-mode: multiply/overlay` nebo dynamického SVG maskování) obarvi tento bílý podklad na zvolenou barvu.
  - Cílem je, aby textura košile zůstala viditelná, ale změnila se barva.

### Krok 5: Barva knoflíčků

- **Možnosti:** Bílý, Černý, Modrý, Šedý.
- **Vizualizace:**
  - Zobrazit výběr barev (color swatches) nebo text.
  - V náhledu zůstává košile z předchozího kroku (obrázky pro knoflíky nejsou k dispozici).

### Krok 6: Velikost

Dvě metody výběru (přepínač / taby):

1. **Konfekční velikost (S - 5XL)**
   - U každé volby zobrazit i orientační obvod krku:
   - S (37/38), M (39/40), L (41/42), XL (43/44), XXL (45/46), 3XL (47/48), 4XL (49/50), 5XL (51/52).
2. **Číselná velikost (Obvod krku)**
   - Výběr z hodnot: 37/38, 39/40, 41/42, 43/44, 45/46, 47/48, 49/50, 51/52, 53/54, 55/56.

### Krok 7: Souhrn a Odeslání

- **Rekapitulace:** Přehledný seznam všech zvolených parametrů.
- **Kontaktní formulář:**
  - Jméno a příjmení (Povinné)
  - Telefon (Nepovinné)
  - Email (Povinné - validace formátu)
  - Poznámka (Nepovinné)
- **Akce:** Tlačítko "Odeslat objednávku".

## 6. Logika odesílání (Backend)

- Vytvoř API endpoint v Nuxtu (např. `/server/api/submit.post.ts`).
- Tento endpoint přijme JSON s konfigurací a osobními údaji.
- Odešle formátovaný email na adresu `jan.flos@volny.cz` (konfigurovatelné v `.env` nebo `nuxt.config`).
- **Testovací režim:**
  - Přidej konfigurační proměnnou `IS_TEST_MODE` (boolean).
  - Pokud je `true`: Do předmětu emailu a do těla zprávy vlož výrazné upozornění: **"JEDNÁ SE O TESTOVACÍ BĚH, NENÍ SKUTEČNÁ OBJEDNÁVKA"**.

## 7. Struktura a organizace kódu

- Použij `pages/` pro routing (pravděpodobně stačí `index.vue` pro SPA wizard).
- Logiku jednotlivých kroků odděl do komponent v `components/configurator/`.
- Sdílený stav (zvolené možnosti) drž v Pinia store (`stores/configurator.ts`).
- Obrázky umísti do `public/images/...`.

## 8. Poznámky k implementaci

- Dbej na ošetření chyb (validace formuláře).
- Zajisti, aby se vracení zpět (tlačítko "Zpět") chovalo intuitivně a nemazalo již zadaná data.
- UI musí být kompletně v češtině.

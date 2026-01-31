Jsi expert na vytváření softwarových specifikací a promptů pro webové aplikace především konfigurátory. 

Potřebuju vytvořit šikovný prompt specifikaci pro webovou aplikaci v prostředí nuxt s pinia store. Stylování udělej pomocí Tailwind. Design moderní, minimalistický, Glassmorphism efekty. Jemné stíny a animace přechodů. Bude to multistep konfigurační agent pro konfiguraci košile. 

Vše musí být v českém jazyce taže cizí nesrozumitelné výrazy které se běžně nepoužívají v prostředí nákupu košil překládej.

Uživatel si nejdřív vybere materiál a pak střih. 

Materiál může být :
1. 60%bavlna/40% polyester 
2. 100% bavlna easy

Střih může být :
1. REGULAR 
2. SLIM
3. SLIM FIT

V konfigurátoru se zobrazí příslušný obrázek košile pro daný střih. Ve složce /images/cuts jsou příslušné střihy REGULAR = regular.png, SLIM = slim.png, SLIM FIT = extra-slim.png

Pak si uživatel nakonfiguruje límec. Tady jsou tyto možnosti:
1. Stojáček
2. Propnutý (Button Down)
3. Kent

V konfigurátoru se zobrazí příslušný obrázek košile pro daný límec. Ve složce /images/collars jsou příslušné límce stojáček = stand_up.png, propnutý = button_down.png, kent = kent.png

Pak si uživatel nakonfiguruje manžetu. Tady jsou tyto možnosti:
1. Kulatá
2. Hranatá
3. Ohrnovací na manžetový knoflík

V konfigurátoru se zobrazí příslušný obrázek košile pro danou manžetu. Ve složce /images/cuffs jsou příslušné manžety kulatá = rounded.png, hranatá = mitered.png, ohrnovací = french.png

Pak si uživatel nakonfiguruje rukáv. Tady jsou tyto možnosti:
1. Dlouhý
2. Krátký
3. Ohrnovací

V konfigurátoru se zobrazí příslušný obrázek košile pro daný rukáv. Ve složce /images/sleeves jsou příslušné rukávy dlouhý = long.png, krátký = short.png, ohrnovací = roll-up.png

Pak si uživatel nakonfiguruje barvu košile. Tady jsou tyto možnosti:
1. Bílá
2. Černá
3. Královská modrá
4. Světle šedá
5. Světle modrá

V konfigurátoru se zobrazí příslušný obrázek košile pro danou barvu. Tady budeš muset zobrazit bílou košili a pomocí css tu košili nějak obarvit. Základ je bílý a musíš zobrazit tu košili která byla vybraná v prvním kroku jak byl střih.

Pak si uživatel nakonfiguruje barvu knoflíčků. Tady jsou tyto možnosti: bílý, černý, modrý, šedý.
Tady si uživatel musí nějak vybrat barvu. Nemám pro to obrázky takže se asi musí zobrazit jenom ta košile.

Pak si člověk vybere velikost. Buď se to vybere tak že si vybere konfeční velikost S - 5XL nebo číselnou velikost podle obvodu krku tedy 37/38, 39/40, 41/42, 43/44, 45/46, 47/48, 49/50, 51/52, 53/54, 55/56
U těch konfečních velikostí udej přibližnou velikost obvodu krku podle následující tabulky :


Písmeno    Obvod krku (cm)
S          37/38
M          39/40
L          41/42
XL         43/44
XXL        45/46
3XL        47/48
4XL        49/50
5XL        51/52


Po té co se košile nakonfiguruje  zobrazí se shrnutí údajů a rekapitulace objednávky. Pak může uživatel zadat Jméno a příjmení povinné, telefon , email povinný a nepovině poznámku
a po té to odešle email s konfigurací na mnou nakonfigurovanou adresu. 

Musí zde být konfigurační možnost v programu, kdy v textu emailu bude jasně vidět že se jedná o testovací běh programu aby to uživatel nepovažoval za skutečnou objednávku. V konfiguračním souboru budu mít možnost to přempnou




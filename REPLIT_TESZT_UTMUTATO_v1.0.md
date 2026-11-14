# Everflame v1.0.0 – egyetlen teljes Replit-tesztmenet

Ez a forgatókönyv úgy készült, hogy egy importálással és egy tesztalkalommal ellenőrizhető legyen az új app. A teszt teljes egészében elvégezhető telefonon; a Shell parancsok a Replit mobilos Shell felületén futnak.

## A. Import és indítás
1. Importáld az `Everflame_App_v1_0_0_Testable.zip` csomagot új projektként. A korábbi verziókat ne töröld.
2. Nyisd meg a Replit Shellt.
3. Futtasd:
   - `npm install`
   - `npm test`
   - `npm run build`
4. Mindkét teszt/build parancsnak sikeres kimenetet kell adnia. A `npm test` legalább 18 tesztet futtat.
5. Nyomd meg a Run gombot. A `.replit` fájl automatikusan a Vite fejlesztői szervert indítja a 0.0.0.0 címen.

## B. Kezdőlap és telefonos elrendezés
- A kezdőlapon 4 zónának és 64 logikai pixelnek kell szerepelnie.
- Görgesd végig a képernyőt; a navigáció és a főkapcsoló nem lóghat ki a nézetből.
- Nyisd meg Chrome-ban a publikált HTTPS címet. Ne a Replit beágyazott előnézetében próbáld a PWA telepítését.

## C. LED-festő
1. Válts a négy zóna között.
2. Fess különböző színeket LED-enként.
3. Próbáld az ecsetméreteket, a színátmenetet és a teljes sávos kitöltést.
4. Kapcsold be a W festést, állíts eltérő fehérértékeket egyes pixeleken.
5. Törölj egy zónát, és ellenőrizd, hogy csak az változik.
6. Ments el legalább két különböző RGBW mintát külön névvel.
7. Exportálj JSON-t, majd importáld vissza.

## D. Minták és régi adatok
- Alkalmazz egy kész hangulatmintát.
- Tölts be egy mentett mintát.
- Frissítsd az oldalt: a legutóbbi kézi festésnek és a mintalistának meg kell maradnia.
- Régi, 192 elemes fizikai LED-mintából a 64 logikai pixeles megjelenítés három szín átlagolásával áll elő.

## E. Időzítések és fényjelenetek
1. Nyisd meg az Időzítés oldalt.
2. Módosítsd a két alapértelmezett rutin nevét, idejét, napjait és műveletét.
3. Adj meg külön fényerőt és effektet.
4. Válassz egy korábban mentett fényfestést mindkét rutinhoz, de különbözőt.
5. Adj hozzá új rutint, majd töröld.
6. Próbálj 8 rutint létrehozni; a 9. rutin hozzáadása legyen letiltva.
7. Próbálj hibás adatot (például 25:70 időpontot vagy nulla kiválasztott napot) beállítani; a mentésnek vissza kell utasítania.
8. Mentsd el, frissítsd az oldalt, és ellenőrizd, hogy a rutinok megmaradtak.

## F. Virtuális ESP32 és alkalmazás-önteszt
1. Beállítások > ESP32-szimuláció indítása.
2. Várd meg, amíg az RGBW adatcsomag ellenőrzése megtörténik.
3. Ugyanitt az Alkalmazás-önteszt panelen nyomd meg az `Önteszt futtatása` gombot.
4. Minden diagnosztikai sor mellett `SIKERES` szerepeljen.
5. A teszt az alkalmazás adatlogikáját teszteli. Nem helyettesíti az RTC, ESP32 vagy fizikai LED próbáját.

## G. PWA – csak production preview vagy publikálás után
A service worker szándékosan csak production módban regisztrálódik. A sima Vite fejlesztői előnézetben a PWA-telepítés nem feltétlenül jelenik meg.
- Előbb legyen sikeres a `npm run build`.
- Indíts production preview-t `npm run preview` paranccsal, vagy publikáld a Replit projektet a buildelt appal.
- A publikált HTTPS címet Chrome-ban nyisd meg.
- Chrome menü > Alkalmazás telepítése / Hozzáadás a kezdőképernyőhöz.
- Offline ellenőrzést csak az első teljes online betöltés után végezz.
- Ha ezt a lépést most kihagyod, a többi alkalmazásfunkciót még teljeskörűen tesztelheted.

## H. Mit küldj vissza
Egyetlen tesztalkalom után küldd el:
1. a `npm test` összefoglaló kimenetét;
2. a `npm run build` sikeres/hibás végét;
3. képernyőképet a telefonos alkalmazás-önteszt eredményéről;
4. minden olyan hibát vagy képernyőképet, ahol nem a leírt eredmény jelent meg.

## Biztonsági korlátozás – valódi hardver
- Az ESP32-re még ne tölts firmware-t.
- Ne csatlakoztasd a 12 V-os LED-szalagot.
- A firmware `EVERFLAME_LED_DRIVER 0` módban van; LED-kimenetet nem ad.
- A pontos SK6812 cikkszám, CI/DI jelölés, adatprotokoll, RGBW byte sorrend és elektromos bekötés továbbra sincs beszállítói adatlappal igazolva.

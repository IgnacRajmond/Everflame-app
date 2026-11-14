# Everflame App v1.0.0

A React + Vite PWA prototípus az Everflame háromkönyves, RGBW LED-es könyvtartóhoz. Az alkalmazás és az ESP32 firmware közös WebSocket protokollja a 4-es verzió.

## Aktuális munkamodell
- 12 V SK6812RGBW, 60 fizikai LED/m, IP30.
- Feltételezett logikai leképezés: 20 címezhető pixel/m; három fizikai LED/logikai pixel.
- Négy zóna: 14 / 18 / 16 / 16 logikai pixel, összesen 64 logikai pixel és 192 fizikai LED-csomag.
- A 3 fizikai LED/pixel arány a konkrét eladói SKU-val még nincs megerősítve.
- A firmware LED-kimenete `EVERFLAME_LED_DRIVER 0` biztonsági módban van.

## v1.0.0 funkciók
- LED-enkénti RGB-festés és független W fehércsatorna.
- Ecset, színátmenet, teljes zónakitöltés, mentett minták és JSON import/export.
- Régi 192 elemű színminták átlagolásos migrációja a 64 logikai pixelhez.
- Heti időzítés legfeljebb 8 rutinnal: név, időpont, napok, be/ki, fényerő, effekt és opcionális mentett fényjelenet.
- ESP32 oldali DS3231 RTC, NVS állapotmentés, két nyomógomb és három TTP223 touch bemenet.
- WebSocket reconnect/heartbeat és eszközazonosítás.
- Beépített mobilos alkalmazás-önteszt (RGBW, pixelkiosztás, migráció, időzítések és csomagméret).

## Replit indítás és tesztelés
A `.replit` fájl a Vite fejlesztői szervert indítja a Run gombbal.

Replit Shell:
```bash
npm install
npm test
npm run build
```

A telefonos, egyalkalmas tesztforgatókönyv: `REPLIT_TESZT_UTMUTATO_v1.0.md`.

## ESP32 firmware
A `firmware/` mappa tartalmazza a PlatformIO projektet, protokollt, magyar bekötési és tesztelési dokumentációt.

A firmware AP-hálózata alapértelmezetten `Everflame-Setup`, IP-címe `192.168.4.1`, WebSocket címe `ws://192.168.4.1:81/`. Az alapértelmezett jelszót feltöltés előtt meg kell változtatni.

A firmware fő részei:
- Protocol v4: teljes RGBW állapotok, DS3231 időbeállítás, heti rutinok és mentett fényjelenetek.
- DS3231 I2C: SDA GPIO21, SCL GPIO22.
- Nyomógombok: GPIO25 és GPIO26, aktív LOW.
- TTP223: GPIO27/32/33, aktív HIGH, 3,3 V táp.
- NVS: a fényállapot és a heti rutinok újraindítás utáni visszaállítása.

## Biztonság és ismert korlátok
- 5 V vagy 12 V soha nem kerülhet közvetlenül ESP32 GPIO-ra.
- A 12 V LED-szalag külön tápegységágról kap tápot; az ESP32 nem táplálja a LED-szalagot.
- A 74AHCT125 és a végleges jelszintillesztés csak a pontos strip-adatprotokoll igazolása után aktiválható.
- A LED-kimenet biztonságosan le van tiltva, amíg a pontos szalagcikkszám, a CI/DI jelölés, az adatprotokoll, a RGBW byte sorrend és a tápelosztás nincs ellenőrizve.
- Az időzítések a DS3231 helyi falióra-idejét használják; időzóna- vagy nyári időszámítás-váltás után újra kell szinkronizálni.
- A firmware PlatformIO fordítása és fizikai hardverteszt még nem igazolt.

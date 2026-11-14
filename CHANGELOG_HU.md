# Everflame – változásnapló

## v0.7.0 – kommunikációs integráció
- ESP32 helyi szimulátor a Beállítások oldalon, hardver nélküli adatcsomag-ellenőrzéshez.
- Valódi eszközazonosítás protokoll-, zónaszám- és fizikai/logikai LED-arány ellenőrzéssel.
- Kézfogási időkorlát és alkalmazásszintű ping/pong kapcsolatfigyelés.
- Szinkronizációs állapot és utolsó sikeres átvitel kijelzése.
- Virtuális ESP32-szimulátor és helyi RGBW adatcsomag-validálás.
- Manifest, Android ikonok és offline app-shell service worker.
- Firmware oldali szigorú adattípus- és tartományellenőrzés.
- Eszközállapot válasz kibővítése pixelmodellel, zónaszámokkal, csatornaszámmal és keretlimittel.
- LED-kimenet továbbra is letiltva, amíg a konkrét szalag és az elektronika fizikai tesztje nem történik meg.

## v0.6.0
- RGBW csatornánkénti pixelmodell, 64/192 pixeles konfigurációs cél.
- WebSocket protokoll v2.


## v0.8.0
- Heti RTC-időzítés szerkesztő: legfeljebb 8 rutin, napválasztás, időpont és be/ki művelet.
- App–ESP32 protokoll v3: `setClock` és `setSchedule` üzenetek, ACK válaszok.
- DS3231 RTC integráció I2C-n, helyi falióra-idő beállítással.
- Két fizikai gomb firmware-kezelése: főkapcsoló és effektváltó.
- A 64 pixeles RGBW modell és a biztonságosan letiltott LED-meghajtó változatlan.
- Fordítás és hardveres ellenőrzés még szükséges.

## v0.8.0 – RTC és fizikai vezérlés
- Időzítés oldal heti rutinokkal: időpont, napok, be/ki, max. 8 rutin.
- WebSocket protokoll v3: setClock, setSchedule, clockAck és scheduleAck.
- DS3231 RTC I2C integráció és helyi idő beállítása az alkalmazásból.
- ESP32 oldali heti időzítések, internet nélkül.
- GPIO25 főkapcsoló és GPIO26 effektváltó gomb kezelése.
- A LED kimenet továbbra is SAFE disabled.
- Build és PlatformIO fordítás nem igazolt.


## v0.9.0 – intelligens fényvezérlés
- Heti időzítésekhez külön fényerő, effekt és választható mentett RGBW-fényfestés.
- ESP32 oldali jelenetvalidálás és jelenetalkalmazás.
- NVS perzisztencia: időzítések és aktuális fényállapot/pixelpufferek.
- TTP223 érintésvezérlés három bemenettel: GPIO27, GPIO32, GPIO33.
- Megnövelt WebSocket keretméret a több jelenetet tartalmazó ütemezési csomaghoz (32 KB).
- A LED-meghajtó SAFE módban marad.


## v1.0.0 – tesztelhető integrációs kiadás
- App/ESP32 protokoll v4.
- Core logika külön modulban; 10 Node.js egységteszt és firmware szerződés teszt.
- Beépített mobilos önteszt.
- Időzített RGBW fényjelenetek: egyedi fényerő, effekt, mentett scene.
- ESP32 NVS rutin- és fényállapot-mentés.
- DS3231 heti időzítés, gombok és TTP223 érintésvezérlés.
- LED fizikai kimenet továbbra is letiltva, amíg az exact SKU/protokoll és bekötés nincs igazolva.

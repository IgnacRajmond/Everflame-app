# Everflame v1.0.0 – fejlesztői tesztjegyzőkönyv

Dátum: 2026-11-14

## Lefuttatott tesztek
- Node.js `npm test`: 18/18 teszt sikeres (RGBW adatmodell, régi minták migrációja, időzítés-validálás, jelenetcsomagok, app/firmware szerződés).
- Python firmware-protokoll teszt: 64 és 192 logikai pixel adatmodellje, csatornák és csomagméret sikeres.
- Python statikus integrációs teszt: app/firmware konfiguráció, protokoll 4, 64 pixeles zónák, RTC/NVS és SAFE LED-kimenet sikeres.
- Python schedule teszt: 8 RGBW-jelenetet tartalmazó időzítési csomag 9333 bájt, 32768 bájtos keretkorlát alatt.
- TypeScript transpile parser: `src/main.jsx`, `src/core.js`, `vite.config.js` JSX/JS szintaktikai feldolgozása sikeres.

## Nem lefuttatható ebben a környezetben
- `npm run build`: nem sikerült; a Vite függőség nem állt rendelkezésre a munkakörnyezetben. Az npm registry DNS-elérése sem működött, ezért a Vite csomag telepítését itt nem tudtam befejezni.
- PlatformIO/ESP32 tényleges fordítás: a PlatformIO nincs telepítve, a csomagtelepítés DNS-elérési hiba miatt nem sikerült. A firmware C++ forrása külön `g++ -fsyntax-only` ellenőrzésen átment ideiglenes Arduino/ESP32 mock headerekkel; ez nem igazolja a valódi ESP32 toolchain és könyvtárak kompatibilitását.
- Replit böngészős teszt: a felhasználó Replit fiókjában nem tudtam elindítani.
- ESP32/RTC/TTP223/LED fizikai teszt: nincs még meg a hardver.

## Fontos teszt-határok
A Node és Python tesztek az adatmodellt, validációt és a statikus app/firmware szerződést ellenőrzik. Nem jelentenek sikeres Vite buildet, C++ firmware-fordítást vagy fizikai eszköztesztet.

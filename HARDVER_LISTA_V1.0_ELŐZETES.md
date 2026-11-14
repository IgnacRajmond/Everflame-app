# Everflame – előzetes hardverlista v1.0

**Ez még nem rendelési lista és nem végleges villamos terv.** A pontos LED-szalag SKU, adatprotokoll és csatlakozók nincsenek megerősítve. Ne rendeld meg az összes alkatrészt, amíg a szalag gyártója/eladója nem erősíti meg az alábbi adatokat.

## LED-szalag munkamodell
A felhasználó által megadott kép felirata: `IP30-SK6812-12V-60LED/m`; látható méretek: 10 mm szélesség, 16,5 mm osztás, 1,95 mm vastagság. A jelenlegi tervezési munkamodell 20 címezhető pixel/m, 3 fizikai LED/pixel, azaz 3,2 m-en 64 logikai RGBW pixel és 192 fizikai LED-csomag. A 3 LED/pixel arányt továbbra is meg kell erősíteni a konkrét termék adatlapjából.

## Előzetes teljesítmény
18 W/m felső értékkel, 3,2 m teljes szalaghosszon:
- 57,6 W teljesítmény;
- 4,8 A áram 12 V-on;
- a 12 V / 8 A tápegység csak előzetes jelölt, nem végleges döntés.

| Zóna | Hossz | Max. becsült áram 12 V-on |
|---|---:|---:|
| Bal ív | 0,7 m | 1,05 A |
| Középső ív | 0,9 m | 1,35 A |
| Jobb ív | 0,8 m | 1,20 A |
| Talp | 0,8 m | 1,20 A |
| Összesen | 3,2 m | 4,80 A |

## Tervezett alkatrészek
| Alkatrész | Mennyiség | Megjegyzés |
|---|---:|---|
| ESP32-WROOM-32 DevKit | 1 | Ne WROVER/PSRAM modellt válasszunk, amíg nincs szükség rá |
| 12 V SK6812 RGBW/RGBNW IP30 60 LED/m szalag | kb. 5 m | 3,2 m beépítés + tartalék; pontos SKU függő |
| 12 V DC tápegység | 1 | Előzetes jelölt: 8 A körüli, minősített külső tápegység |
| 12 V → 5 V DC/DC buck | 1 | Stabil 5 V, legalább 2 A; vezérlő és 74AHCT125 számára |
| 74AHCT125 | 1 | 4 adatcsatornás jelszintillesztő; 5 V táplálás |
| 330–470 Ω soros ellenállás | 4 | Csak a végleges egyvezetékes adatprotokoll igazolása után |
| 1000 µF / 25 V kondenzátor | 1–4 | 12 V tápbetáplálásnál, polaritás betartásával |
| 100 nF kondenzátor | 1–2 | Jelszintillesztő leválasztására |
| DS3231 RTC modul | 1 | CR2032-hez ne legyen nem megfelelő töltőáramköre |
| TTP223 touch modul | 3 | 3,3 V tápellátás, digitális kimenet |
| Pillanatkapcsoló | 2 | GPIO25 és GPIO26 |
| Biztosítéktartó/elosztó | 1 készlet | Főág és 4 LED-zóna külön védelme; értékek kábelméret alapján |
| 12 V nagyáramú csatlakozó | 1 pár | A tényleges áramra méretezve; kis barrel jack nem megfelelő |
| 3 eres zónacsatlakozó | 4 készlet | 12 V / DATA / GND, ha a szalag igazoltan ilyen jelű |

## Előzetes GPIO-kiosztás
- GPIO16/17/18/19: négy LED-zóna adatvonal (csak igazolt protokoll után).
- GPIO21/22: DS3231 SDA/SCL.
- GPIO25: főkapcsoló pillanatgomb, aktív LOW, GND-re húzva.
- GPIO26: effektváltó pillanatgomb, aktív LOW, GND-re húzva.
- GPIO27: TTP223 főkapcsoló touch.
- GPIO32: TTP223 effekt touch.
- GPIO33: TTP223 fényerő touch.

**Minden ESP32 GPIO 3,3 V logikai szintű. 5 V vagy 12 V közvetlenül nem kerülhet GPIO-ra.** A TTP223 modulokat 3,3 V-ról tápláljuk és közös GND-t használunk.

## Vásárlás előtt kötelezően visszaigazolandó
1. A pontos SKU és gyártói adatlap.
2. 12 V, 60 fizikai LED/m és 20 címezhető pixel/m ténylegesen igaz-e.
3. A képen szereplő `CI` vagy `C1` felirat jelentése: clock bemenet, tartalék adatvonal vagy más.
4. A strip adatprotokollja: egyvezetékes SK6812-kompatibilis vagy clock+data.
5. RGBW byte sorrend és a fehér csatorna típusa/színhőmérséklete.
6. Maximális fogyasztás, tápbetáplálási követelmény és vágási pont.

A firmware LED-kimenete biztonsági okból `EVERFLAME_LED_DRIVER 0` állásban marad, amíg ezeket nem igazoltuk.

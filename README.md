Guitar pedal resources / Gitarrpedal-resurs

EN: Documentation for a modular analog guitar pedalboard (18 V DC, SELV): module standard, power distribution, wiring, BOMs and a reference library of pedal circuits. Work in progress, unreviewed. Read disclaimer.md and the known issues below before building or ordering anything.

SV: Dokumentation för ett modulärt analogt pedalbord (18 V DC, SELV): modulstandard, matning, kablage, stycklistor och ett referensbibliotek med pedalkretsar. Pågående arbete, ogranskat. Läs disclaimer.md och de kända felen nedan innan du bygger eller beställer något.

Status

Allt är ogranskat tills en modul uttryckligen är markerad som verifierad mot datablad eller byggd och mätt. Det finns än så länge inga KiCad-filer i repot, bara dokumentationen och planerad struktur.

Kända fel (hittade i granskning, ännu inte rättade i dokumentet)

Beställ inga kretskort efter dokumentet förrän dessa är åtgärdade. Detaljer finns i docs/granskning_v9_dokumentet.md.

MN3207-pinouten i Bilaga C verkar vara fel (VDD och GND på fel stift, VGG-kopplingen från MN3102 stämmer inte). Påverkar Chorus och Flanger. Kontrollera mot tillverkarens datablad.
TL072/TL074 (CP-varianter) används utanför databladets matningsområde vid 8,5–9,7 V. Välj H-varianter eller dokumentera avvikelsen. Samma sak gäller LM741 (Distortion+).
Bypass för modulerna i rackläge är inte definierad. 3PDT finns bara i "fristående" tillvalet.
Limiterns LED-stapel saknar drivare (komparatorer eller LM3915) och fungerar inte som ritad.
VREF är inkonsekvent (4,75 / 4,5 / 4,35 V) och delas av alla moduler utan lokalt filter.
Jordtopologin (signal- och strömkablar med GND) kan ge slingor, och det finns ingen regel för skärmens jordning.
Alternativ 2 (nio basvärden för alla motstånd) ändrar flera klassiska kretsar. Pedalnamn som TS9, RAT och Big Muff bör läsas som "inspirerad av".
Kap. 12B (23 referensmoduler), inklusive den aktiva DI:n med phantom (48 V), är ogranskade.
Struktur
Mapp	Innehåll
docs/	Dokumentation, granskningar och ritregler
standard/	Rutnät, kontakter, pinning och spänningsregler (kommer)
modules/	En mapp per modul: module.toml, README.md, bom.csv, kicad/
kicad-template/, kicad-libs/	Projektmall och gemensamma bibliotek (kommer)
tools/	Skript, bl.a. build_index.py som bygger export/oversikt.md
export/	Genererade filer
Modulstatus
ogranskad: skriven men inte kontrollerad
verifierad: IC-pinouts och gränsvärden kontrollerade mot datablad (revision angiven)
byggd och matt: byggd och uppmätt
Bidra

Fel och rättelser tas emot som issues. Ange komponent, vad som är fel, källa (datablad med revision) och förslag. Ändringar loggas med datum och vem som hittade felet.

Licens

Ingen licens vald än. Förslag: CERN-OHL för hårdvara, CC BY-SA 4.0 för dokumentation, MIT för skript. Tills en licens är vald gäller alla rättigheter.

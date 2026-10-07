---
name: Vass Gergő Dániel
neptun: DYRKAU
id: 2026-SD-03
github: https://github.com/Vassgergo5/project-course
---
# Tananyaghoz kötött feladatgeneráló és gyakorlóalkalmazás

A projekt egy webalkalmazás, amely szöveges tananyagok tanulását és gyakorlását segíti. A felhasználó feltölti a jegyzetét, amelyet a rendszer egységes belső formátumra konvertál és részekre bont. A tananyag privát maradhat, vagy a tulajdonosa nyilvánosan megoszthatja, így mások is tanulhatnak belőle, használhatják a kérdéseit, vagy saját kérdéseket generálhatnak hozzá. A kérdéseket AI generálja feleletválasztós és rövid szöveges formában. Minden kérdés egy verziózott tananyagrészletre hivatkozik, amelyből kiderül, hogy a kérdés a tananyag ismeretével megválaszolható, és a felhasználó ez alapján hagyja jóvá. A tananyag változásakor az érintett kérdések felülvizsgálandó állapotba kerülnek. A kutatási rész összehasonlítja a teljes dokumentumra és a visszakeresett részletekre (RAG) épülő generálást, valamint a véletlenszerű és a feltételes feladatsor-összeállítást. A tervezett megoldás SvelteKit, PostgreSQL, Prisma és Zod alapú, az AI-integráció a DeepSeek Harness keretrendszerrel, kizárólag szerveroldalon készül. A konkrét nyelvi modell kiválasztása a későbbiekben történik.

## Célok

- **Elsődleges cél:** Működő tanuló- és gyakorlóalkalmazás, amelyben az AI által generált kérdések visszakövethetően a tananyaghoz kötődnek, emberi jóváhagyáson mennek át, és a tananyagok megoszthatók. Emellett a generálási és a feladatsor-összeállítási módszerek mérhető összehasonlítása.
- **Célfelhasználók / érintettek:** Elsősorban diákok és hallgatók, akik saját vagy megosztott jegyzetekből szeretnének megbízhatóan, a tananyaggal összeegyeztethetően tanulni, gyakorolni. Másodsorban oktatók, akik megoszthatják a tananyagaikat. Érintett még a témavezető és az értékelők.
- **Mérhető sikerkritériumok:**
  - Minden kérdés hivatkozik egy tananyagrészletre (azonosító, verzió, tartalom-hash), amelyből kiderül, hogy a kérdés a tananyag ismeretével megválaszolható.
  - Egy részlet módosítása után a hozzá kötött kérdések 100%-a felülvizsgálandó lesz minden ráépülő kérdésbankban, a többi kérdés változatlan marad.
  - Más kérdésbankja nem módosítható, és egy gyakorlósor mindig egyetlen tananyagból áll.
  - Azonos seed, paraméterek és kérdésbank-állapot mellett a gyakorlósor azonos.
  - Minden LLM-kimenet sémavalidáción esik át, érvénytelen kimenet nem mentődik.
  - A két generálási mód és a két összeállítási módszer tesztkészleten össze van hasonlítva a briefben előírt mérőszámok szerint.
  - A rövid válaszok AI-értékelése a kézi pontozással legalább 70%-ban egyezik (legfeljebb egypontos eltérés), a célérték az első mérések után pontosítható.
  - A tartományi logika adatbázis és LLM nélkül futtatható, és automatizált tesztek fedik le.
- **Korlátok:** TypeScript és SvelteKit, PostgreSQL és Prisma, Zod-validáció az LLM-kimenettől az adatbázisig. AI-hívás csak szerveroldalon. Az első változat .txt bemenetet és két feladattípust kezel. Az AI hibája nem okozhat adatvesztést, titkos kulcs és személyes adat nem kerülhet a repóba.

## Hatókör

### Benne van a hatókörben

- Egyetlen fióktípus, a szerep a tananyaghoz és a kérdésbankhoz fűződő viszonytól függ.
- Tananyag feltöltése bővíthető konverterekkel (először .txt), verziózás, darabolás és a darabolás kézi ellenőrzése.
- Privát vagy nyilvános tananyag. Nyilvános tananyagnál a tulajdonos kérdésbankja is nyilvános, a tanulók utólag generált új kérdései a saját privát bankjukba kerülnek.
- Megosztott tananyag bővítése saját jegyzetekkel, az eredeti módosítása nélkül. A bővített tananyag nem osztható tovább.
- AI-alapú kérdésgenerálás részlethivatkozással, jóváhagyás, szerkesztés, nehézségi kategóriák és duplikátumszűrés.
- Érvénytelenítés tananyagváltozáskor minden ráépülő kérdésbankban, újrageneráláskor a kézi javítással összevethető tervezettel.
- Tanulási mód több tananyag párhuzamos tanulásával, és gyakorlósor egy tananyag több fejezetéből, témalefedettség, feladatszám és korábbi próbálkozások alapján, reprodukálhatóan, a kérdésbank elégtelenségének kezelésével.
- Determinisztikus feleletválasztós és rubric-alapú AI-értékelés felülvizsgálati jelzéssel.
- RAG-alapú generálás, jelentés hibás tartalomról, haladáskövetés, reszponzív felület.
- Reprodukálható értékelési eljárás, automatizált tesztek, futtatási útmutató és mintaadatok.

### Nincs benne a hatókörben

- Hivatalos vizsgáztatás, osztályzás.
- Kép-, hang- és videóalapú tananyag (OCR, átírás).
- Kettőnél több feladattípus és esszéjellegű válaszok.
- Különböző tananyagok keverése egy gyakorlósorban.
- Külön oktatói fióktípus, saját modell tanítása, valós idejű közös szerkesztés.

## Jegyzetek

Az első változat egy tantárgy néhány fejezetét használja. Ezek egy részén fejlesztek és hangolom a promptokat, a többi a kiértékelés tesztkészlete. A rendszer azt garantálja, hogy a kérdés a tananyaghoz hű, azt nem, hogy a tananyag helyes, és a kérdésminőségből nem következtet tanulási eredményességre.

Lehetséges bővítés az ellenőrzött oktatói jelölés, a tananyag linken keresztüli megosztása, további konverterek (.md, .docx, szöveges PDF, .pptx), az ismétlési ütemezés és a natív mobilalkalmazás Capacitorral. Ezek csak az alapfunkciók megbízható működése után kerülnek sorra.

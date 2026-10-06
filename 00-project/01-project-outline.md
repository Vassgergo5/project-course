---
name: Vass Gergő Dániel
neptun: DYRKAU
id: 2026-SD-03
github: https://github.com/Vassgergo5/project-course
---
# Tananyaghoz kötött feladatgeneráló és gyakorlóalkalmazás

A projekt egy webalkalmazás, amely a felhasználó saját szöveges tananyagából AI segítségével feleletválasztós és rövid szöveges választ igénylő gyakorlókérdéseket generál. A központi feladat az, hogy a generált tartalom megbízható és visszakövethető legyen. Ezért minden kérdés a tananyag egy verziózott, jóváhagyott részletéhez kötődik, csak a felhasználó jóváhagyása után kerül a feladatbankba, és a tananyag változásakor a rendszer felülvizsgálandóként jelöli meg. A felhasználó a jóváhagyott kérdésekből seed alapján reprodukálható gyakorlósorokat old meg. A feleletválasztós válaszokat a rendszer determinisztikusan, a rövid válaszokat előre rögzített szempontrendszer alapján AI-val értékeli, bizonytalan esetben felülvizsgálati jelzéssel. A kutatási rész összehasonlítja a teljes dokumentumra és a visszakeresett részletekre épülő generálást, valamint a véletlenszerű és a feltételeket kezelő feladatsor-összeállítást. A megoldás a Next.js (TypeScript), a PostgreSQL, a Prisma és a Zod technológiákra épül, az LLM-hívások kizárólag szerveroldalon futnak. A projekt végére a felhasználó a saját jegyzetéből készült, ellenőrzött kérdésekkel gyakorolhat, és követheti a haladását.

## Célok

- **Elsődleges cél:** Működő, verziókezelt gyakorlóalkalmazás elkészítése, amelyben az AI által generált kérdések visszakövethetően a felhasználó tananyagához kötődnek, emberi jóváhagyáson mennek át, és a tananyag változásakor automatikusan felülvizsgálandóvá válnak. Emellett cél a generálási és a feladatsor-összeállítási módszerek mérhető összehasonlítása.
- **Célfelhasználók / érintettek:** Diákok és hallgatók, akik a saját jegyzetükből szeretnének megbízható, a tananyaggal összeegyeztethető gyakorlófeladatokon keresztül gyakorolni vagy a számonkéréseikre felkészülni. Érintett még a témavezető és az értékelők.
- **Mérhető sikerkritériumok:**
  - A feladatbankban lévő minden kérdés hivatkozik egy jóváhagyott tananyagrészletre (részletazonosító, verzió, tartalom-hash), és a kérdés forrásidézete szó szerint megtalálható a hivatkozott részletben.
  - Egy tananyagrészlet módosítása után a hozzá kötött kérdések 100%-a felülvizsgálandó állapotba kerül, a nem érintett részletek kérdései változatlanok maradnak.
  - Ugyanazzal a seeddel, paraméterekkel és feladatbank-állapottal összeállított gyakorlósor azonos kérdéseket ad azonos sorrendben.
  - Minden LLM-kimenet sémavalidáción esik át, mielőtt adatbázisba kerül, és a sémának nem megfelelő kimenetet a rendszer nem menti el.
  - A teljes dokumentumra és a visszakeresett részletekre épülő generálás minősége, késleltetése és költsége tananyagonként elkülönített tesztkészleten össze van hasonlítva.
  - A véletlenszerű és a feltételes feladatsor-összeállítás témalefedettsége, kérdésismétlődése, teljesíthetősége és összeállítási ideje össze van hasonlítva.
  - A rövid válaszok AI-értékelésének egyezése a kézzel ellenőrzött mintákkal össze van hasonlítva.
  - A tartományi logika (darabolás, a kérdések állapotátmenetei és érvénytelenítése, duplikátumszűrés, gyakorlósor-összeállítás, feleletválasztós értékelés) adatbázis és LLM nélkül is futtatható, és automatizált tesztek fedik le.
- **Korlátok:** Az alkalmazás TypeScriptben, Next.js App Routerrel készül, a szerveroldali logika Server Actionökben és API route-okban fut. Az adatokat a PostgreSQL tárolja, az elérés a Prismán keresztül történik. A Zod-sémák az LLM-kimenettől egészen az adatbázisig ellenőrzik az adatokat. LLM-hívás csak szerveroldalon történhet. A felületnek mobilon és asztali gépen is használhatónak kell lennie. Az első változat szöveges tananyagra és két feladattípusra korlátozódik. Az AI hibája vagy elérhetetlensége nem okozhat adatvesztést. API-kulcs, más hitelesítő adat, valamint személyes vagy éles adat nem kerülhet a repóba vagy a kliensoldalra.

## Hatókör

### Benne van a hatókörben

- Szöveges tananyag feltöltése, verziózása, részletekre bontása (chunking) és a tananyagegységek jóváhagyása.
- Feleletválasztós és rövid szöveges válaszos kérdések AI-alapú generálása, forrásrészlethez és forrásidézethez kötve.
- Kérdések manuális ellenőrzése, szerkesztése, jóváhagyása vagy elutasítása, szerkeszthető nehézségi kategóriákkal.
- Közel azonos kérdések felismerése és kezelése.
- A tananyagváltozás észlelése és az érintett kérdések érvénytelenítése (függőségi modell), újrageneráláskor a kézi javításokkal összevethető tervezettel.
- Gyakorlósor összeállítása témalefedettség, feladatszám, nehézség és korábbi próbálkozások alapján, seed segítségével reprodukálhatóan, a feladatbank elégtelenségének kezelésével.
- Determinisztikus értékelés a feleletválasztós kérdéseknél, szempontrendszer-alapú (rubric) AI-értékelés és felülvizsgálati jelzés a rövid válaszos kérdések esetén.
- Hibás kérdés vagy értékelés jelentése.
- Felhasználói haladáskövetés témánként.
- Reszponzív, mobilon is használható webes felület.
- A generálási módok és a feladatsor-összeállítási módszerek összehasonlítása, valamint a kérdésminőség és az AI-értékelés mérése reprodukálható értékelési eljárással.
- Automatizált tesztek a tartományi logikához, futtatási útmutató és mintaadatok.

### Nincs benne a hatókörben

- Hivatalos vizsgáztatás, osztályzás.
- Kép-, hang- vagy videóalapú tananyag feldolgozása (OCR, átírás).
- Kettőnél több feladattípus, valamint hosszú, esszé jellegű válaszok értékelése.
- Oktatói feladatmegosztás és ismétlési ütemezés (lehetséges későbbi bővítések).
- Saját nyelvi modell tanítása vagy finomhangolása.
- Valós idejű közös szerkesztés, közösségi funkciók, ranglisták.
- Natív mobilalkalmazás.

## Jegyzetek

Az első változat egyetlen, előre kiválasztott tantárgy néhány fejezetét használja. Ezek egy részén történik a fejlesztés és a promptok hangolása, a többi fejezetet pedig a kiértékelés tesztadatkészleteként tartom fenn. A kérdések jóváhagyása a forrásrészlettel való összevetésen alapul, nem a felhasználó előzetes tudásán. A rendszer ezért azt garantálja, hogy a kérdés a feltöltött tananyaghoz hű, azt nem, hogy maga a tananyag helyes. A jó kérdésminőségből a projekt nem következtet tanulási eredményességre. A hatókörön kívüli bővítések csak akkor merülhetnek fel, ha a forráskötés, az érvénytelenítés, a jóváhagyási folyamat és az értékelés megbízhatóan működik. A darabolás pontos szabályai, a visszakeresés módja, a bizonytalanság mérése és az LLM-szolgáltató kiválasztása a specifikációban és a kezdeti technikai javaslatban dől el.
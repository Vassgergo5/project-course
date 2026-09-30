---
name: Vass Gergő Dániel
neptun: DYRKAU
id: 2026-SD-03
---
# Tananyaghoz kötött feladatgeneráló és gyakorlóalkalmazás

## A brief értelmezése

A projekt célja egy olyan mobilon, weben vagy akár kombináltan is használható alkalmazás kidolgozása, amely strukturált szöveges tananyagokból AI segítségével generál forráshoz köthető, ellenőrizhető gyakorlófeladatokat. A megbízhatóság és a hitelesség érdekében a generált kérdések (feleletválasztós és rövid szöveges típusok) a forrásszöveghez kötve, kizárólag kézi ellenőrzést és jóváhagyást követően kerülnek a feladatbankba. A tananyag módosítása esetén a függőségi modell alapján az érintett kérdések érvénytelenítésre kerülnek. A gyakorlás során a feleletválasztós válaszok értékelése determinisztikus, míg a rövid szöveges válaszokat az AI előre rögzített szempontok szerint pontozza, bizonytalan esetben felülvizsgálati jelzéssel. A rendszer méri az előrehaladást, és megadott témalefedettség, nehézség, valamint korábbi próbálkozások alapján állít össze reprodukálható feladatsorokat.

## Miért én lennék alkalmas erre a projektre?

Érdekelnek a modern, interaktív webes alkalmazások és a nyelvi modellek gyakorlati, megbízható integrációja. Hallgatóként különösen motivál egy olyan alkalmazás megvalósítása, amely valóban hatékonyabbá és célzottabbá teszi a tananyagok feldolgozását a diákok és hallgatók számára. Ez a projekt remek lehetőség arra, hogy a reszponzív felülettől a stabil háttérlogikáig bemutassam és elmélyítsem a full-stack fejlesztési tudásomat egy hasznos, valós problémát megoldó alkalmazáson keresztül.

## Releváns tapasztalat és előzmények

Saját és tanulmányi projektek keretében webes és mobilalkalmazások fejlesztésével egyaránt foglalkoztam. Ennek köszönhetően magabiztos Git-ismeretekkel, valamint full-stack alapokkal rendelkezem. Kliensoldalon React és TypeScript, a backend terén Java és Spring Boot technológiákat is használtam. Ismerem a relációs adatmodellezést, a modern webes felületek felépítését és az adatáramlás típusbiztos rétegzését.

## Tervezett megközelítés

A feladathoz reszponzív, kliens-szerver alapú webes struktúrát választanék Next.js (TypeScript) alapon. Ezzel egyszerre biztosítanám az AI-modulok, az üzleti logika és a felület tiszta funkcionális szétválasztását, valamint a platformfüggetlen, azonnali kipróbálhatóságot mobilról és asztali gépről egyaránt. A kulcskérdések a tananyag és a kérdések közötti függőségek precíz kezelése, a determinisztikus sémavalidáció, valamint a feltételes feladatsor-generálás kidolgozása lenne.

A backend (Next.js Server Actions / API Routes) felelne az üzleti logikáért, a relációs adatkezelésért (PostgreSQL és Prisma ORM) és a külső nyelvi modell védett, szerveroldali meghívásáért, kizárva a hitelesítő adatok szivárgását. A kliensoldalt React komponensekre építeném, biztosítva a jóváhagyási munkafolyamat és a gyakorlófelület letisztult kezelhetőségét mobilon is. Az LLM-válaszok validálásától az adatbázis-kezelésig egységesen Zod sémákra támaszkodnék, biztosítva az adatáramlás determinisztikus és típusbiztos felépítését.

## Kezdeti terv

1. A tananyag- és kérdésmodellek, a jóváhagyási folyamat és az adatformátumok meghatározása. 
2. A specifikáció és a kezdeti technikai architektúra elkészítése. 
3. A szövegdarabolás, a kérdésgenerálás és a sémavalidáció prototipizálása.
4. A reszponzív kliens elkészítése a kérdésszerkesztéshez, jóváhagyáshoz és gyakorláshoz.
5. Prisma-perzisztencia, forrásérvénytelenítés és a feladatsor-összeállító logika integrálása.
6. A kérdésminőség és feladatsor-összeállítás mérése tesztkészleten, valamint a használhatóság értékelése.

## További információ

A munkát Git-verziókövetéssel vezetem, a feladatokat issue-kra bontva. 
Kiemelt figyelmet fordítok az API-kulcsok szerveroldali védelmére és az AI-logika tiszta elválasztására.
A projektben végig TypeScriptet használok, a frontendhez és API route-okhoz Next.js-t, az adatbázis-eléréshez Prismát.

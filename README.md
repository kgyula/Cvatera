# Online Aukciós Platform (Catawiki-jellegű) – Projekt Összefoglaló

## 1. Projekt célja

Egy magyar nyelvű, online aukciós piactér létrehozása, ahol különleges, gyűjtői vagy prémium tárgyakat lehet értékesíteni és vásárolni, időalapú aukciós logikával.  
A platform célja a felhasználók közötti bizalom kiépítése, egyszerű kezelhetőség, korszerű licitmechanika (pl. automatikus licit, anti-sniping), és biztonságos, letéti (escrow) fizetés. A szakértői ellenőrzés opcionális, a minőségi kínálat támogatása mellett a belépési küszöb alacsonyan tartása is fontos.

---

## 2. Főbb funkciók

- **Felhasználói fiókok:** regisztráció, bejelentkezés, email megerősítés.
- **Termékfeltöltés:** eladó egyszerűen tud új terméket aukcióra bocsátani, képekkel, leírással.
- **Szakértői értékelés (nem kötelező):** minden termékhez opcionális, kérhető szakértői vagy mesterséges intelligencia (AI) alapú értékelés/minősítés.
- **Aukciós logika:** időzített aukciók, manuális és automatikus (proxy) licit, dinamikus időhosszabbítás (anti-sniping).
- **Termékoldal:** minden terméknél részletes adatlap, képek, leírás, licittörténet.
- **Értesítések:** email és in-app értesítések (licit, aukció vége, túllicitálás, fizetés).
- **Fizetés és szállítás:** biztonságos fizetés (escrow), szállítási opciók, követés.
- **Adminisztráció:** termékek, felhasználók, aukciók kezelése, moderáció.

---

## 3. Új, specifikus üzleti szabályok

### 3.1. Szakértői értékelés rugalmassága
- **Nem kötelező szakértői értékelés**: A termékek feltöltésekor a szakértői értékelés csak opcionális, nem kötelező minden terméknél.
- **AI alapú értékelés lehetősége**: Az eladók (vagy a rendszer) mesterséges intelligencia alapú értékelést is kérhetnek, mely automatizáltan adhat becslést, minősítést vagy kategorizálást a termékről.
- **Külön jelölés**: A szakértő vagy AI által értékelt termékek külön jelölést kapnak a platformon.

### 3.2. Jutalék feltételekhez kötése
- **Időszakos jutalékmentesség**:  
  - Az új regisztrálók számára a platform használata és az értékesítés **6 hónapig jutalékmentes** lehet (pl. regisztrációtól számítva).
  - Lehetőség időszakos promóciókra is: **adott időablakban** minden termékre vagy bizonyos típusokra vonatkozó jutalékmentesség.
- **Részletes szabályozás**:  
  - A jutalékmentességhez tartozó feltételek (pl. csak első X termék, vagy összes termék) adminisztratív felületen állíthatók.

### 3.3. Kategória-alapú jutalékozás
- **Kategóriától függő jutalék**: A rendszerben a jutalék mértéke termékkategóriánként eltérő lehet (pl. műtárgy, ékszer, könyv, bélyeg, stb.).
- **Adminisztrációs beállítás**: Az admin felületen minden kategóriához külön-külön állítható a jutalék mértéke (akár 0% is).
- **Elszámolás**: A fizetendő jutalék minden értékesítésnél automatikusan a termék kategóriája alapján kerül meghatározásra.

---

## 4. Fő felhasználói szerepkörök

- **Eladó**: termékfeltöltés, aukciózás, értesítések, szállítás kezelése.
- **Vevő**: böngészés, licitálás, fizetés, értesítések.
- **Szakértő**: termékek szakmai értékelése, minősítés, javaslattétel (emberi vagy AI-alapú szakértői szerep).
- **Admin/Moderátor**: termékek, aukciók, felhasználók kezelése, jutalék szabályok és promóciók beállítása.

---

## 5. Fő folyamatok (röviden)

1. **Regisztráció:** felhasználó regisztrál, (jutalékmentes időszak admin által beállítható).
2. **Termékfeltöltés:** eladó feltölti a terméket, kérhet szakértői/AI értékelést (opcionális).
3. **Szakértői értékelés:** szakértő (emberi vagy AI) leírást, minősítést vagy ajánlást adhat a feltöltött termékhez.
4. **Aukció indítása:** termék aukcióra kerül, vevők licitálhatnak.
5. **Aukciózárás:** nyertes vevő fizet (escrow), eladó szállít.
6. **Elszámolás:** jutalék számítása a termék kategóriája és az aktuális szabályok alapján (jutalékmentesség figyelembevétele).
7. **Adminisztráció:** admin felületen kategória-jutalékok és promóciós időszakok menedzselése.

---

## 6. Monetizáció

- **Kategóriaalapú jutalék** (pl. 5–15%, kategóriánként eltérő, adminisztrálható)
- **Promóciós időszakok**: időszakos jutalékmentesség vagy csökkentett jutalék (pl. bevezetési kampány, új felhasználók)
- **Opcionális szakértői vagy AI értékelés díja** (külön választható szolgáltatás)

---

## 7. Prioritás és MVP fókusz

- Termékfeltöltés, aukció, licitálás, fizetés, szállítás, admin oldali jutalék és promóciós logika, opcionális szakértői/AI értékelés – ezek az MVP részét képezik.
- Később bővíthető reputációs rendszerrel, statisztikával, integrációkkal.

---

## 8. Kiemelt előnyök

- Alacsony belépési küszöb, gyors indulás
- Rugalmas, adminisztrálható jutalékstruktúra
- Szakértői vagy AI értékelés lehetősége, de nem kötelező
- Kategória-alapú díjazás, célzott promóciók

---

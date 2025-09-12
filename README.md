# Aukciós + Használtcikk (Hibrid) Piactér – Kibővített Projekt Összefoglaló

Ez a dokumentum a korábban meghatározott, Catawiki-szerű kurált aukciós platform vízióját bővíti egy általános “használt ad–vétel” (fix árú / apróhirdetés jellegű) funkcionális iránnyal. A cél: hibrid modell – prémium aukció + általános second‑hand piactér – egységes technológiai és bizalmi keretrendszerben.

---

## 1. Megújított Fő Cél

Létrehozni egy hibrid online piacteret, amely:
1. Kurált (szakértő által ellenőrzött) különleges tárgyak aukcióit kezeli (értéknövelő, bizalmi réteg).
2. Támogatja az általános “használt termék” (általános gyűjtői vagy hétköznapi) fix áras vagy alkuképes hirdetéseket, gyorsabb és alacsonyabb belépési súrlódással.
3. Közös felhasználói identitást, reputációt, fizetési és értesítési infrastruktúrát használ mindkét modellhez.
4. Képes a felhasználókat a “casual seller” → “trusted / curated seller” funnel mentén fejleszteni (verifikáció, minőségi szintlépések).

---

## 2. Bővített Értékajánlat Összevetés

| Pillér | Aukciós réteg | Használt (fix ár / apró) réteg |
|--------|---------------|--------------------------------|
| Céltárgy típusa | Ritkaságok, gyűjteményes, prémium | Általános gyűjtői / hobby / hétköznapi |
| Ármechanika | Licit + proxy + anti-sniping | Fix ár, vagy fix ár + ajánlat/alku |
| Minőség kontroll | Kurátor jóváhagyás (kötelező) | Alap önkiszolgáló; opcionális “verified” badge |
| Időfaktor | Időzített lezárás | Folyamatos elérhetőség (expire / megújítás) |
| Fizetés | Escrow kötelező | Escrow ajánlott; helyi átvételnél opcionális “offline” jelölés |
| Monetizáció | Jutalék eladási ár %-ból | Hirdetés kiemelés, tranzakciós díj, csomag előfizetés |
| Bizalom | Szakértői szűrés + reputáció | Reputáció + jelvények + KYC szintek |
| Likviditás | Alacsonyabb volumen, magasabb érték | Magas volumen, széles kategóriaspektrum |

---

## 3. Új / Kiegészített Szerepkörök

- Casual Seller – gyors fix árú hirdetést ad fel.
- Local Buyer – helyi térképes / távolság alapú keresés.
- Power Seller – nagy mennyiségű listázás, riport igény.
- Negotiator Buyer – alku / ajánlat funkciót használ.
- Trust & Safety Operátor – csalás és visszaélések felügyelete (apróhirdetés kockázat nő).
- Fulfillment Partner (opcionális jövőben) – integrált logisztikai aggregator.

---

## 4. Kiegészített Funkcionális Területek (Használt / Fix Ár)

| Modul | Leírás | Prioritás (Hibrid fázis) |
|-------|--------|---------------------------|
| Fix árú listázás | Azonnali megjelenés minimális mezőkkel | Fázis 1 |
| Opcionális moderált felülminősítés | “Curated” státusz kérés | Fázis 2 |
| Alku / Ajánlattétel (Offer) | Buyer ajánlatot tesz, eladó elfogad / counter | Fázis 2 |
| Chat / Biztonságos üzenet | Szűrt kulcsszavak (anti-scam) | Fázis 2–3 |
| Hely alapú keresés | Város + sugár / megyeszint | Fázis 2 |
| Hirdetés lejárat / megújítás | Expire + “bump” funkció | Fázis 1 |
| Kiemelés / promó | Lista teteje, színes keret, badge | Fázis 2 |
| Tömeges feltöltés | CSV / API nagy eladóknak | Fázis 3 |
| Kosár / Több tétel vásárlás | Fix ár több termék egyszerre | Fázis 3 |
| Részleges escrow opció | Opcionális biztonságos fizetés | Fázis 2 |
| Lokációs metaadat tárolás | Normalizált régió / geohash index | Fázis 1–2 |

---

## 5. Új Domain Entitások (Aukciós mag mellé)

- Listing (fix árú hirdetés)
  - id, seller_id, title, description, category_id, price, currency
  - status (active, paused, sold, expired)
  - condition, location (geo / city), shipping_options, promoted_flag
  - created_at, expires_at, renewed_count

- Offer
  - id, listing_id, buyer_id, offer_amount, status (pending, accepted, declined, expired, countered)
  - parent_offer_id (counter lánc), expires_at

- Order (fix ár tranzakció)
  - id, listing_id, buyer_id, seller_id, agreed_price
  - status (initiated, paid_escrow, shipped, completed, dispute, refunded)
  - escrow_flag (bool)

- Chat_Message
  - id, thread_id, sender_id, sanitized_body, classification (safe / flagged)

- Promotion
  - id, listing_id, type (highlight, top_slot, badge), start_time, end_time

- GeoIndex / Location
  - listing_id, geohash, region_code

Közös entitások új mezői:
- User: seller_tier, trust_score, strike_count
- Moderation_Log kiterjesztése listing típusra is.

---

## 6. Ár / Alku Folyamat – Rövid Sequence

1. Buyer Offer létrehoz → Offer.status=pending; Seller értesítve.
2. Seller: Accept → Order generálódik (escrow opció kérdés) → Fizetés.
   - Decline → Offer.status=declined
   - Counter → Új Offer parent_offer_id=eredeti
3. Fizetés (ha escrow választva) → Order.status=paid_escrow
4. Szállítás / átvétel → Buyer “complete” vagy automatikus release (timeout).
5. Release → payout pipeline → commission számítás (ha alkalmazandó).

---

## 7. Architektúra Kiegészítések

Új szolgáltatások / modulok:
- Listing Service (külön a curated Item + Auction logikától)
- Offer / Negotiation Service (state machine)
- Chat Sanitization (NLP / szabálymotor)
- Geo Search réteg (pl. PostgreSQL PostGIS vagy Elastic geo_point)
- Promotion Engine (időzített priorizálás, cache)
- Trust & Safety (flag detection, throttle szabályok)

Skálázási megfontolás:
- Aukciós bid motor továbbra is alacsony latency fókusz (Redis lock).
- Fix ár listing nagy mennyiség – szükség szerint külön read replica, caching layer (Redis sorted sets: category:last_update_time).
- Keresés evolúció: Postgres fulltext → Elastic/OpenSearch (aukció + listing index konvergált schema: type=auction|listing).

---

## 8. Új User Story Váz (Használt / Fix Ár)

EPIC: Fix Árú Listázás
- Must: Mint eladó minimális mezővel (cím, ár, kategória, állapot) szeretném azonnal közzétenni a hirdetést.
- Must: Mint eladó szeretném, ha 30 nap után a hirdetés inaktívvá válna (expire).
- Should: Mint eladó egy kattintással “megújíthatom” (bump) a hirdetésem.
- Could: Mint eladó kiemelhetem a hirdetésem 7 napra.

EPIC: Alku / Ajánlat
- Must: Mint vevő ajánlatot szeretnék tenni a fix ár alatt, hogy kedvezményt kapjak.
- Must: Mint eladó el akarom fogadni, elutasítani vagy ellenajánlatot tenni.
- Should: Mint vevő látni akarom az ajánlat lejárati idejét (pl. 24 óra).
- Could: Mint eladó automatikus szabályt állítok: “>= X összegű ajánlatot fogadd el”.

EPIC: Chat / Kommunikáció
- Should: Mint vevő kérdést intézhetek az eladóhoz a listázás alatt.
- Should: Mint rendszer érzékeny adatok (telefon, email) küldését jelöli / maszkolja.
- Could: Mint felhasználó spam / csalás gyanús üzenetet jelentek.

EPIC: Lokáció & Keresés
- Must: Mint vevő keresni szeretnék város + km sugárral.
- Should: Mint vevő szűrni akarok csak “személyes átvétel” opcióra.
- Could: Mint vevő térképes nézeten szeretném látni a találatokat.

EPIC: Reputáció Kiterjesztés
- Should: Mint buyer értékelni akarom a tranzakciót (1–5 + szöveg).
- Could: Mint rendszer trust_score-t növelem sorozatos pozitív értékelés után jelvénnyel.

EPIC: Promotion
- Should: Mint eladó vásárolhatok kiemelést (top list pozíció).
- Could: Mint rendszer dinamikus pricing-et alkalmazhat csúcsidőben.

---

## 9. Monetizáció – Hibrid Modell

| Csatorna | Aukció | Fix ár |
|----------|--------|--------|
| Eladási jutalék | Igen (alap) | Opcionális (ha escrow) |
| Listing fee | (Csak prémium kiemelt aukció) | Opció (ingyenes limit felett) |
| Promóció | Kiemelt aukció blokk | Kiemelés / bump |
| Szakértői díj | Igen | Opcionális upgrade |
| Előfizetés | “Pro Seller” dashboard | “Power Lister” (tömeges feltöltés) |
| Fizetési margin | Escrow kezelési díj | Escrow választás esetén |
| Partner integráció | Tematikus kampány | Logisztika, biztosítás |

---

## 10. Mérőszámok (Kiegészítve Fix Árra)

- Listing Activation Rate (% draft → active)
- Listing Renewal Ratio (% expiring → renewed)
- Offers per Listing átlag
- Offer Accept Ratio (% accepted / össz aj.)
- Time-to-First-Offer (átlag)
- Chat Abuse Flag Rate
- Escrow Adoption Rate (% tranzakció escrow-val)
- Promotion Conversion (kiemelés → eladás gyorsulás)
- GMV szegmentált: aukció vs fix ár
- Buyer 30/60/90 napos retention csatornánként

---

## 11. Kockázatok (Hibrid Kiterjesztés)

| Kockázat | Hatás | Mitigáció |
|----------|-------|-----------|
| Brand hígulás (prémium vs tömeg) | Aukciós exkluzivitás gyengülhet | UI szétválasztás, “Curated” badge, külön landing |
| Fraud növekedés fix árnál | Vevői bizalom esik | Escrow default ajánlás, chat szűrés, reputáció súlyozás |
| Technikai komplexitás nő | Fejlesztési sebesség csökken | Moduláris service boundary + fokozatos rollout |
| Moderáció túlterhelés | Backlog nő | Automata kép / kulcsszó előszűrés |
| Keresési teljesítmény romlik | Latencia | Index stratégia, dedikált search cluster |
| Ár arbitrázs (aukció vs fix ár átfedés) | Zavart okoz | Ajánlórendszer konzisztencia, duplikátum detektálás |

---

## 12. Fázisolt Bevezetési Terv a Hibridhez

| Fázis | Cél | Kulcselemek |
|-------|-----|-------------|
| 0 (Baseline) | Aukciós MVP stabil | Eddigi core funkciók |
| 1 | Egyszerű fix ár listázás + expire | Listing CRUD, expirer job |
| 2 | Alku + lokáció + “bump” | Offer engine, geo index, promotion alap |
| 3 | Chat + moderált filter | Üzenet sanitization, report flow |
| 4 | Escrow opció fix árnál + reputáció | Order + escrow flag, rating modul |
| 5 | Tömeges eszközök + advanced search | Elastic geo + power seller API |
| 6 | Dinamikus promó pricing + ML trust | Pricing engine, trust score ML pipeline |

Release guardrail: minden fázis végén mérőszám validáció (fraud rate, latency, support ticket volumetria).

---

## 13. Technikai Kiegészítés – Adatbázis Index / Skálázás

- Listing:
  - (status, category_id, updated_at DESC) composite index listaoldalhoz
  - (geohash_prefix, status) index lokációs kereséshez
  - fulltext (title, description) GIN
- Offer:
  - (listing_id, status)
  - (buyer_id, status)
- Order:
  - (seller_id, status, created_at)
  - (buyer_id, status)
- Promotion közelgő lejáratok: (end_time) ascending priority queue
- Caching:
  - “Top trending listings” → Redis sorted set (score = view_count + recent_offer_weight)

---

## 14. Biztonság / Trust & Safety Bővítés

- Chat NLP pipeline (kulcsszó / PHI / direct contact attempt detection) → maskolás + figyelmeztetés.
- Offer spam rate limiter (user_id dnev: X új offer per hour).
- Velocity check: több új account azonos IP / device hash → flagged.
- Listing image perceptual hash (duplikált / tiltott tartalom).
- Escrow ajánlás UI: “Biztonságosabb tranzakció – válassz escrowt”.

---

## 15. Egységes Reputációs Keret

Reputáció komponensei:
- Transakciós pontok (sikeres eladások / vásárlások)
- Időben teljesített szállítás arány
- Konfliktus / dispute arány
- Visszajelzés súlyozása (aukció > fix ár, verified buyer > új buyer)
- Fraud flag súly levonás

Badgek példák:
- “New Seller” (0–5 eladás)
- “Reliable Seller” (>=10, 0 dispute az utolsó 90 napban)
- “Curated Approved” (legalább 1 szakértői jóváhagyott aukció)
- “Fast Responder” (chat válaszidő < 2 óra median)

---

## 16. Konvergált UI Irányelvek

- Fő választó: Aukciók / Fix ár (tab / külön feed).
- Listing card jelölés:
  - Aukció: countdown, current bid.
  - Fix ár: price pill, “Make Offer” gomb.
- Curated jelvény: csak approved aukció + curated listing upgrade esetén.
- Szűrők: Kontextusfüggő (aukció: time left; fix ár: distance, only offers accepted, pickup available).

---

## 17. Egyszerű Példa Offer State Machine

States: pending → (accepted | declined | expired | countered)  
Rules:
- Counter létrehozása: eredeti pending → countered; új Offer state=pending.
- Expire: scheduler (cron) 24h után (ha nincs transition).
- Accept csak “latest active branch” offeren engedett (parent lánc validálás).

---

## 18. Integrációs Megfontolások

- Geo: OpenStreetMap + forward geocoding (Nominatim) → geohash.
- Fraud ML (később): Feature store (listing_age, offers_count, ip_risk_score).
- Image optimize pipeline: WebP + perceptual hash (pHash) táblázat.
- Pricing engine (promotion): CRON precompute + Redis ephemeral cache.

---

## 19. Teszt / QA Kiegészítések

- Property based test: Offer counter lánc konzisztencia.
- Load: 10k aktív listing + 200 parallel offer művelet.
- Geo keresés relevancia: bounding box vs sugár pontosság ±1 km tolerancia.
- Chat moderation: hamis pozitív < 3% target.
- AB teszt (később): Escrow konverzió uplift mérés.

---

## 20. Stratégiai Differenciáció a “Sima Apróhirdetésektől”

- Fokozatos “minőségi funnel”: self-serve → verified → curated.
- Egységes escrow + reputáció keretrendszer mindkét csatornára (bizalmi prémium).
- Aukciós feed-be cross-promoting releváns fix ár listing (kategória hibrid ajánlás).
- Oktató tartalom: “Mikor válassz aukciót vs fix árat?” – döntési segéd.
- Dinamikus javaslat: ha fix ár listázás 7 nap után inaktív → ajánlat: “Indíts aukciót (ajánlott kezdőár X)”.

---

## 21. Rövid Prioritizált “Hybrid Extension” Backlog (Első 3 Fázis)

Fázis 1 (Foundation – 3–4 sprint):
1. Listing entity + CRUD + indexelés
2. Kategória integráció reuse (auction + listing)
3. Expire job + renew endpoint
4. Alap feed API + sort (recent, price asc)
5. Minimal UI integráció (külön tab)
6. Alap geolocation mezők (város + manual)
7. Egyszerű riport adminnak (#active, #expired)

Fázis 2 (Interaction – 3 sprint):
8. Offer engine + accept/decline
9. Counter offer logika
10. Email értesítések offer eseményekre
11. Lokációs keresés (radius) – geohash index
12. Bump / promote (simple flag + weight sort)
13. Escrow opció fix ár tranzakcióra (Order skeleton)

Fázis 3 (Trust & Engagement – 3 sprint):
14. Chat (moderált) MVP
15. Rating modul integráció (order completion trigger)
16. Promotion időzítés + lejárat
17. Analytics metrikák (offer conversion, escrow adoption)
18. Reputáció kalkuláció első verzió

---

## 22. Összegzés – Hibrid Platform Elv

A bővítés nem egyszerű “apróhirdetés” hozzáadás: egy egységes bizalmi és monetizációs gépezet felépítése, amely:
- Maximálja a belépő küszöb alacsony súrlódását (self-serve listing),
- Felfelé szűri és pozicionálja a minőségi készletet (curated aukció),
- Visszacsatolt reputációs és escrow mechanizmusokkal csökkenti a kockázatot,
- Moduláris architektúrával kezeli a volumennövekedést és a differens sebességű fejlesztési pályákat.

---

## 23. Következő Javasolt Lépések

1. Listing vs Auction közös design rendszer komponens specifikálása.
2. Offer state machine részletes sequence diagram.
3. Geo modell (geohash precízió kiválasztása magyar piac lefedettséghez).
4. Escrow opciós döntési fa (mikor default ON?).
5. Reputáció scoring képlet első draft + normalizáció.
6. Promotion ranking formula (pl. score = base_weight + recency_decay + payment_weight).

Készen állok a fenti pontok bármelyikének részletes kibontására – jelezd, melyik terület legyen a következő fókusz.

---

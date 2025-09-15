# WordPress-alapú Aukciós Platform – Részletes Összefoglaló

Ez a dokumentum egy Catawiki-jellegű, magyar nyelvű online aukciós piactér gyors és költséghatékony bevezetését mutatja be WordPress és WooCommerce alapokon, ismertetve a fő komponenseket, ajánlott modulokat és testreszabási lehetőségeket.

---

## 1. Miért WordPress + WooCommerce?

- **Gyors bevezetés, alacsony induló költség:** Bővítményekkel és sablonokkal a legtöbb kulcsfunkció kódolás nélkül elérhető.
- **Rugalmas piactér- és aukciós motor:** Számos megbízható, nemzetközi és magyar fejlesztésű plugin támogatja az aukciós logikát, a piactér-modellt és a kategória-alapú jutalékozást.
- **Jó támogatás, folyamatos frissítések:** Nagy fejlesztői közösség, rendszeres biztonsági frissítés.
- **Magyar lokalizáció és fizetés:** Elérhető magyar nyelv, forint, Barion/OTP Simple/Stripe integrációk.
- **Bővíthetőség:** Egyedi fejlesztésű pluginokkal, API kapcsolatokkal később továbbfejleszthető (pl. AI értékelés).

---

## 2. Alapfunkciók – Megoldások WordPress/WooCommerce környezetben

### 2.1. Felhasználói fiókok, jogosultságok

- WooCommerce alapból kezeli a vásárló/eladó szerepköröket.
- Piactér plugin (pl. **Dokan**, **WCFM Marketplace**) kibővíti eladói funkciókkal, saját eladói adminisztrációval.
- Szakértői szerepkör: Egyedi user role vagy vendor role bővítmény, jogosultságkezeléssel (pl. User Role Editor).

### 2.2. Termékfeltöltés, aukciós logika

- Eladó frontendről (vagy adminból) tölthet fel terméket (leírás, kép, kategória, kezdőár, licitlépcső, zárás dátuma).
- **YITH WooCommerce Auctions** vagy **Ultimate WooCommerce Auction** plugin:
  - Automatikus licit (proxy), anti-sniping (időhosszabbítás), Buy Now opció, aukciózárás, értesítések.
  - Kategóriához kötött termékfeltöltés.
- Szakértői/AI értékelés: Külön űrlap (Gravity Forms, WPForms), ahol eladó kérhet értékelést, vagy automatikus workflow (pl. AI API bekötés).

### 2.3. Aukciós termékoldal

- Egyedi sablonnal részletes adatlap: képek, leírás, licittörténet, zárás ideje, szakértői/AI minősítés, kategória, eladó adatai, szállítási információk.
- Widgetek: ajánlott hasonló aukciók, kiemelt eladók.

### 2.4. Licitálás, fizetés, escrow

- Plugin oldja meg a licitlogikát, a végén automatikus értesítő a nyertesnek.
- WooCommerce Payment Gateway-k (Barion, Stripe, SimplePay, PayPal).
- Escrow logika:  
  - Egyszerű verzió: a fizetés a platformhoz érkezik, az eladó csak szállítás/jóváhagyás után kapja meg (admin manuális jóváhagyással).
  - Komplex verzióhoz speciális escrow plugin, vagy egyedi workflow/plugin fejlesztése szükséges.

### 2.5. Jutalék- és díjkezelés

- **WooCommerce Simple Auctions**, **Product Category Discount/Fee** pluginok:
  - Kategóriaalapú jutalékok, fix vagy százalékos díjak.
  - Promóciós időszakok: időszakosan 0% jutalék vagy kedvezményes díjszabás, akár regisztrációtól számított időintervallumra.
  - Ingyenes aukciózás új felhasználóknak (WooCommerce Memberships/Subscriptions + rules).

### 2.6. Piactér funkciók

- **Dokan** vagy **WCFM Marketplace**:
  - Több eladó, saját boltprofil, rendeléskezelés, statisztika.
  - Eladói értékelés, reputáció.
  - Admin visszaigazolás, moderáció.
- Felhasználók, eladók, szakértők, adminok szerepköre szabadon menedzselhető.

### 2.7. Értesítések, kommunikáció

- **Better Notifications for WP**, **WP Mail SMTP**:  
  - Aukciózárás, túllicitálás, fizetési emlékeztetők, szakértői értékelés visszajelzése.
- Vevő–eladó üzenetváltás:  
  - Dokan/WCFM chat modul, vagy külön plugin.

### 2.8. Szállítás, számlázás

- **Table Rate Shipping**: Szállítási díjak, opciók, ország/kategória alapú szabályok.
- **Számlázz.hu WooCommerce plugin**: Automatikus számlázás, NAV kompatibilis.

### 2.9. Adminisztráció

- WooCommerce és piactér plugin admin felülete:  
  - Termékek, aukciók, felhasználók, kifizetések, jutalékszabályok, promóciók, statisztikák, jelentések.
- Egyedi riportok, exportok (pl. Aukciós forgalom, jutalékbevétel).

---

## 3. Opcionális és jövőbeli fejlesztések

- **AI értékelő plugin integráció** (pl. OpenAI, Google Vision): képek, leírások automatikus értékelése, kategorizálása.
- **Egyedi workflow plugin**: összetett admin folyamatok, escrow automatizálás.
- **Mobil PWA vagy natív app**: reszponzív dizájn alapból, később dedikált app.
- **Duplikátum-, csalás- és spamvédelem**: WP Cerber, AntiSpam Bee.
- **Marketing automatizáció**: MailPoet, WooCommerce Follow-ups.
- **Reputációs rendszer bővítés**: vásárlói, eladói értékelések, jelvények, kiemelt eladók.

---

## 4. Főbb ajánlott modulok – összefoglaló táblázat

| Funkció                       | Ajánlott Plugin                                |
|-------------------------------|-----------------------------------------------|
| Aukciós piactér (core)        | YITH WooCommerce Auctions, Ultimate WC Auction|
| Piactér, eladói admin         | Dokan, WCFM Marketplace                       |
| Kategóriaalapú jutalék        | Product Category Discount/Fee, Dokan Pro      |
| Fizetés (HUF, escrow)         | Barion, Stripe, SimplePay, escrow: egyedi     |
| Szakértői/AI értékelés        | Gravity Forms, WPForms, OpenAI API integráció |
| Számlázás                     | Számlázz.hu WooCommerce plugin                |
| Szállítás                     | Table Rate Shipping, WooCommerce Shipping     |
| Értesítések                   | Better Notifications for WP, WP Mail SMTP     |
| Felhasználói szerepkörök      | User Role Editor, Dokan/WCFM role bővítés     |
| Promóciós időszakok, díjak    | WooCommerce Fees and Discounts, Subscriptions |
| Admin riportok, export        | WooCommerce Export, Dokan Reports             |

---

## 5. Előnyök és korlátok

### Előnyök

- Gyors MVP, alacsony fejlesztési és üzemeltetési költség
- Bármikor bővíthető, könnyen testreszabható
- Rengeteg kész plugin, fejlesztő és támogatás elérhető
- Magyar fizetés, számlázás, lokalizáció megoldott

### Korlátok

- Nagy terhelésnél, nagyon speciális aukciós logikánál skálázhatósági és egyediségi határok
- Komplex egyedi workflow (pl. AI workflow, többlépcsős escrow) fejlesztést igényel
- Pluginok között lehetnek inkompatibilitások, folyamatos karbantartás szükséges

---

## 6. Ajánlott lépések az induláshoz

1. WordPress, WooCommerce, piactér és aukciós plugin telepítése, magyarítás
2. Alap sablon kiválasztása, branding
3. Kategóriák, jutalék- és díjszabás, promóciós szabályok beállítása
4. Szakértői/AI értékelési workflow kialakítása
5. Tesztelés: regisztráció, termékfeltöltés, aukció, licit, fizetés, admin folyamatok
6. Folyamatos fejlesztés, visszacsatolás alapján plugin bővítés vagy egyedi fejlesztés

---

## 7. Példa induló roadmap (MVP)

1. Alaprendszer telepítés, magyar lokalizáció
2. Piactér, aukciós és jutalék modulok integrációja
3. Fizetési és számlázási modulok beállítása
4. Szakértői/AI értékelés lehetőségének kialakítása
5. Promóciós, időszakos díjszabás szabályok beállítása
6. Eladói és vevői oldali tesztfolyamatok
7. Indulás, marketing, visszamérés
8. Folyamatos továbbfejlesztés igény szerint

---

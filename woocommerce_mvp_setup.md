1. Áttekintés

A jelenlegi plugin-készlettel a rendszer már eljut oda, hogy
a Junk (apróhirdetéses) és a Gallery (védett piactér) logika külön kezelhető.
A cél most nem fejlesztés, hanem minden plugin teljes beállítása,
hogy a rendszer működjön, bemutatható legyen, és stabil alapot adjon a novemberi fejlesztésekhez.
átgondoltam, és ahogy átnéztem a felrakott bővítményeket, az látszik, hogy az alapváz nagyjából odáig tud most eljutni, hogy a rendszerben már elkülöníthető a két fő irány: a hirdetéses „junk” rész és a védett „gallery” piactér.
A Dokan és a WCFM együtt elviszik az eladói felületet, termékfeltöltést, rendeléskezelést, jutalékokat és a refund-folyamatokat. A WP Adverts és a Memberships Pro pedig lefedi a gyors listázásos, kontakt-hozzáféréses logikát, tehát a junk oldal már most el tud indulni vele – gyakorlatilag egy működő apróhirdetési modell lesz belőle.

A piactér rész (gallery) a buyer protection résszel együtt plugin alapon is összeáll. Az escrow és a kifizetések kezelése tesztkörnyezetben már működik, a pénz fogadható, visszatartható és manuálisan kiadható.
Ez bőven elég lesz arra, hogy a védett vásárlás logikája látszódjon, és az egész platform átláthatóan két irányban működjön: a gyors hirdetéses és a biztonságos piactér modellben.

A KYC-mezők is beállíthatók már most az eladói profilban, így megvan az alapja a DAC7-kompatibilis azonosításnak. A Metorik riportokkal pedig látjuk a forgalmat, refundokat és jutalékokat, vagyis a pénzügyi oldal is működőképes vázon lesz.

A szállítási résznél is eljutunk addig, hogy az alap tracking és címkegenerálás (GLS, Foxpost stb.) működjön, tehát a buyer protection ágon a kézbesítéshez kötött folyamat már demonstrálható.

Ami most még hiányzik, az a finomabb átmenet a két világ között.
Belenyúlni majd a buyer protection és a checkout folyamat közé kell, hogy az egész gördülékenyen váltson a hirdetéses és az escrow-alapú logika között. Ebben az Elementor Pro is sokat fog segíteni, mert ott tudjuk majd testre szabni a checkout mezőket, a buyer protection kapcsolót és az ehhez tartozó üzeneteket.

Ha minden plugin be van állítva, és a front-oldal is fel van húzva, akkor az MVP-váz gyakorlatilag állni fog.
Ezzel október 25-ig el tudunk jutni oda, hogy a rendszer működik, be lehet mutatni, látszik, mi mire szolgál, és onnantól csak bele kell fejleszteni a saját logikáinkat – a DAC7 jelentést, az escrow-automatizmust, a vitakezelést és a payout menedzsmentet.

A beállításokat nézve, a Dokan Pro-val kell kezdeni, mert az adja az egész eladói vázat. Ott az eladói regisztrációt, termékfeltöltést, rendeléskezelést és kifizetési folyamatokat kell bekapcsolni. Az eladók termékei csak admin jóváhagyással jelenjenek meg, így tudjuk kontroll alatt tartani a piacteret. A „Vendor Dashboard”-ot érdemes magyarosítani, elnevezni „Eladói felületnek”, és bekapcsolni a statisztikákat, hogy mindenki lássa a saját forgalmát és jutalékát.

A WCFM Marketplace-ben a refund és a vitakezelés modulokat kell bekapcsolni, hogy az eladók tudjanak visszatérítést kérni, és ezek bekerüljenek az admin oldalra is. A payout (withdrawal) modult is aktiválni kell, hogy látszódjon az eladói kifizetési felület, még ha az elején manuális is marad. A kettő együtt fogja adni a buyer protection pénzügyi részének demóját.

A WP Adverts oldalán a kategóriákat és a hirdetési űrlapot kell rendbe tenni. Legyen benne terméknév, ár, leírás, állapot és képfeltöltés. A hirdetés érvényességét állítsuk be 30 napra, és automatikus archiválás menjen a végén. Kapcsoljuk be az e-mail értesítéseket is, hogy a hirdető kapjon visszajelzést a feltöltésről.

A Paid Memberships Pro-nál hozzunk létre két szintet: egy ingyenes, ami csak hirdetni tud, és egy „Pro” csomagot, ami hozzáfér a kontaktadatokhoz. Ezt a Contact Access Addonnal kell összekötni, hogy a rendszer csak fizetés után adja ki a vevő adatait. Fizetéshez a Barion vagy Stripe tesztmódot kapcsoljátok be, hogy látszódjon a folyamat.

Az escrow résznél a Mangopay vagy Escrow plugin sandbox-kulcsait kell felvinni, és le kell futtatni egy próbarendelést, hogy a pénz escrow-ba kerüljön és csak manuálisan lehessen felszabadítani. Ezt az admin felületen kell majd figyelni, ott látszani fog a tranzakció státusza (on hold / released).

A checkout folyamatban a Woo Conditional Checkout Fields-szel tegyünk be egy Buyer Protection kapcsolót. Ha ezt a vevő bekapcsolja, akkor a Woo Fee Manager segítségével jelenjen meg két tétel: egy 5%-os Buyer’s Premium és egy fix 990 Ft-os Buyer Protection díj. Ezzel a checkout már külön tudja kezelni a védett és nem védett vásárlásokat.

A KYC Verification pluginnél három mezőt hozzatok létre az eladói profilban: teljes név, adóazonosító és bankszámlaszám. Ezek csak akkor legyenek kötelezők, ha valaki buyer protection eladást indít. Ez előkészíti a DAC7-et, de nem zavarja a sima hirdetőket.

A Data Exporter Pro-ban be kell állítani, hogy az eladók forgalma (név, termékszám, bevétel, jutalék, refund) exportálható legyen CSV és JSON formátumban. Ezzel már most lesz egy alap riport, amit az admin le tud menteni.

A logisztikai plugineknél elég, ha a GLS vagy Foxpost sandbox verziót bekapcsoljátok, generáltok egy címkét és megnézitek, hogy visszaadja-e a tracking ID-t. A buyer protection ágon ez lesz a kézbesítéshez kötött trigger.

Az Elementorban pedig a front-oldalt kell most felhúzni. Legyen egy Főoldal, ahol röviden elmagyarázzuk a két világot (Junk és Gallery), egy „Hogyan működik?” oldal, ami leírja a buyer protectiont, plusz a Kapcsolat, ÁSZF és Adatkezelés oldalak. A menüben a Junk és Gallery külön fülön szerepeljen, de egységes stílusban, hogy ne tűnjön szétválasztottnak.

Ha ezek beállnak, október 25-re gyakorlatilag egy teljes, működő váz lesz előttünk, ami fejlesztés nélkül is használható és bemutatható. Onnantól jövünk mi az egyedi részekkel – a DAC7 riport, az automatikus escrow-release, a vitakezelés és a payout menedzser, meg a saját buyer protection workflow.


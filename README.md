### 1. UVOD V NUMERIČNO RAČUNANJE

#### (1) Kaj je strojni epsilon? Kaj je osnovna zaokrožitvena napaka?

Strojni epsilon je najmanjša razlika med 1 in naslednjim večjim številom, ki ga lahko predstavi računalniški sistem. Osnovna zaokrožitvena napaka je napaka, ki nastane, ko se realna števila zaokrožijo na najbližje predstavljivo število v računalniškem formatu.

#### (2) Katere napake pri numeričnem računanju poznamo?

Poznamo več vrst napak, vključno z zaokrožitvenimi napakami, napakami zaradi omejene natančnosti predstavitve števil, in algoritemskimi napakami, ki nastanejo zaradi neoptimalnih numeričnih metod.

#### (3) Katere so osnovne računske operacije v IEEE in kateri dve operaciji sta problematični s stališča numerične matematike?

Osnovne računske operacije po standardu IEEE vključujejo seštevanje, odštevanje, množenje, deljenje in korenenje. Problematični operaciji sta deljenje in odštevanje, še posebej, ko se deli ali odšteva zelo majhne številke, kar lahko vodi v izgubo natančnosti.

#### (4) Kaj je relativno direktno stabilna metoda in kaj relativno obratno stabilna metoda?

Relativno direktno stabilna metoda zagotavlja, da majhne spremembe v vhodnih podatkih povzročijo le majhne spremembe v izhodnih podatkih. Relativno obratno stabilna metoda zagotavlja, da so izhodni podatki natančni rešitvi malo spremenjenih vhodnih podatkov.

**Primer stabilne metode:** Metoda, ki je hkrati relativno direktno in obratno stabilna, je Gaussova eliminacija.
**Primer nestabilne metode:** Metoda, ki je relativno obratno stabilna, a ni direktno stabilna, bi bila iterativna rešitev sistemov linearnih enačb, kjer lahko začetne napake hitro narastejo.

### 2. REŠEVANJE LINEARNIH SISTEMOV

#### (1) Zapišite splošen kvadraten sistem linearnih enačb in ga prepišite v matrično obliko.

Splošen kvadraten sistem linearnih enačb zapisujemo kot \( Ax = b \), kjer je:

- \( A \) matrika koeficientov velikosti \( n \times n \),
- \( x \) vektor neznank,
- \( b \) vektor konstant.

**Resljivost:**

- Sistem je **enolično rešljiv**, če je determinanta matrike \( A \) neničelna.
- Sistem ni rešljiv ali ima neskončno mnogo rešitev, če je determinanta matrike \( A \) enaka nič.

**Število operacij:**

- Produkt matrike z vektorjem zahteva \( n^2 \) operacij.
- Produkt dveh matrik \( n \times n \) zahteva \( n^3 \) operacij.

#### (2) Kaj je Gaussova eliminacija?

Gaussova eliminacija je metoda za reševanje sistemov linearnih enačb z reduciranjem matrike na zgornje trikotno obliko. Potrebno je približno \( \frac{2}{3}n^3 \) osnovnih računskih operacij za izvedbo.

#### (3) Opis elementarnih eliminacij

Elementarne eliminacije vključujejo vrstične operacije kot so zamenjava, množenje vrstice z skalarjem in dodajanje večkratnika ene vrstice k drugi, da se dosežejo ničle pod glavno diagonalo.

**Inverz in produkt eliminacij:**

- Inverz elementarne eliminacije dobimo z obratno operacijo.
- Produkt dveh elementarnih eliminacij se izračuna z zaporednim izvajanjem obeh operacij na enoto matriko.

#### (4) Kaj je LU razcep matrike A brez pivotiranja?

LU razcep brez pivotiranja razdeli matriko \( A \) na produkt spodnje trikotne matrike \( L \) in zgornje trikotne matrike \( U \). Izračun zahteva približno \( \frac{1}{3}n^3 \) operacij. Obstaja, če so vsi glavni minori matrike \( A \) neničelni.

**Primer, kjer LU razcep brez pivotiranja ni možen:**
Matrika:
\[ A = \begin{bmatrix}
0 & 1 \\
1 & 1 \\
\end{bmatrix} \]
ne omogoča LU razcepa brez pivotiranja zaradi ničelnega elementa na mestu \( a\_{11} \).

#### (5) Kaj je zgornjetrikoten sistem linearnih enačb?

Zgornjetrikoten sistem ima ničle pod glavno diagonalo matrike.

**Substitucija:**

- **Premo substitucija** se ne uporablja; relevantna je le za spodnjetrikotne sisteme.
- **Obratna substitucija** se uporablja za reševanje zgornjetrikotnega sistema, začenši z zadnjo enačbo.

Potrebno je \( \frac{n(n+1)}{2} \) operacij za reševanje zgornjetrikotnega sistema.

#### (6) Uporaba LU razcepa za reševanje linearnega sistema \(Ax = b\)

Za reševanje sistema \(Ax = b\) s pomočjo LU razcepa najprej razcepimo matriko \(A\) na produkt \(LU\), kjer je \(L\) spodnjetrikotna matrika, \(U\) pa zgornjetrikotna matrika. Reševanje sistema poteka v dveh korakih:

1. Rešimo \(Ly = b\) za \(y\) z uporabo premega vstavljanja.
2. Rešimo \(Ux = y\) za \(x\) z uporabo obratnega vstavljanja.

Za celoten postopek je potrebno \(n^2\) operacij za vsako substitucijo, skupaj torej \(2n^2\) operacij.

#### (7) LU razcep z delnim pivotiranjem

**Delni pivot** pri LU razcepu vključuje izbiro največjega elementa v stolpcu kot pivot, da se izogne težavam z numerično stabilnostjo. Postopek izračuna:

1. Izberemo največji element v stolpcu pod ali na diagonalni liniji.
2. Zamenjamo trenutno vrstico z vrstico, ki vsebuje največji element.
3. Nadaljujemo z razcepom kot pri standardnem LU razcepu.

Za reševanje \(Ax = b\) s to metodo najprej izračunamo \(Ly = Pb\) (kjer je \(P\) permutacijska matrika zaradi pivotiranja), nato rešimo \(Ux = y\). Skupaj potrebujemo približno \(2n^3/3\) operacij za razcep in \(2n^2\) za substituciji.

#### (8) LU razcep s kompletnim pivotiranjem

LU razcep s **kompletnim pivotiranjem** vključuje izbiro največjega elementa iz celotne preostale matrike (ne samo stolpca) za pivotiranje. Čeprav je ta metoda zelo stabilna, se redko uporablja zaradi visoke računske zahtevnosti, ki lahko bistveno upočasni postopek, še posebej pri velikih matrikah.

#### (9) Stabilnost reševanja zgornjetrikotnega sistema z obratno/premo substitucijo

Stabilnost reševanja zgornjetrikotnega sistema z **obratno substitucijo** je običajno visoka, saj postopek naravno preprečuje deljenje z zelo majhnimi števili, razen če je zgornjetrikotna matrika slabo pogojena. V primeru spodnjetrikotnih sistemov, kjer uporabimo premo substitucijo, je tudi stabilnost običajno dobra, razen v primerih slabo pogojenih matrik ali zelo majhnih diagonalnih elementov.

#### (10) Kaj je pivotna rast?

Pivotna rast je merilo za povečanje elementov matrike med LU razcepom s pivotiranjem. Pove nam, kako se največja absolutna vrednost elementov matrike spreminja med izvajanjem eliminacijskega procesa. Pri delnem pivotiranju je pivotna rast omejena, kar pomeni, da razcep ne poveča vrednosti elementov preko določene meje, zagotavljajoč numerično stabilnost.

#### (11) Stabilnost računanja LU razcepa

- **Brez pivotiranja:** Lahko je nestabilno, če v matriki obstajajo zelo majhni diagonalni elementi.
- **Z delnim pivotiranjem:** Večja stabilnost, saj izbor največjega elementa v stolpcu kot pivot zmanjša problem majhnih pivotov.
- **S kompletnim pivotiranjem:** Največja stabilnost, vendar zahtevnejša zaradi iskanja največjega elementa v celotni preostali matriki.

#### (12) Razcep Choleskega matrike

Razcep Choleskega se uporablja za simetrične, pozitivno definitne matrike, kjer matriko \(A\) razdelimo na \(A = LL^T\), kjer je \(L\) spodnjetrikotna matrika. Ta razcep je običajno bolj stabilen in manj računsko zahteven v primerjavi z LU razcepom.

#### (13) Kaj je vektorska norma?

Vektorska norma meri velikost ali dolžino vektorja. Primeri:

- Evklidska norma \( \|x\|\_2 \)
- Maksimalna norma \( \|x\|\_\infty \)
- Manhattan norma \( \|x\|\_1 \)
  Uporabljajo se za oceno velikosti napak, konvergenco algoritmov in stabilnost sistemov.

#### (14) Kaj je matrična norma?

Matrična norma, izpeljana iz vektorskih norm, ocenjuje velikost matrik. Primeri matričnih norm:

- Frobeniusova norma
- Spektralna norma
  Matrične norme so ključne pri analizi numerične stabilnosti algoritmov in ocenjevanju občutljivosti rešitev.

#### (15) Kaj je pogojenostno število matrike?

Pogojenostno število matrike meri, kako vhodne napake vplivajo na izhodne rezultate. Visoko pogojenostno število pomeni, da majhne vhodne napake lahko povzročijo velike izhodne napake, kar lahko pokaže na numerično nestabilnost algoritma.

#### (16) Iterativne metode za reševanje linearnih sistemov

Primer iterativne metode je **metoda konjugiranih gradientov**, ki se uporablja predvsem za reševanje velikih, redkih sistemov simetričnih, pozitivno definitnih matrik. Metoda izračuna rešitev z minimizacijo funkcije v obliki kvadratnega polinoma, pri čemer koristi lastnosti ortogonalnosti.

### 3. PREDOLOČENI SISTEMI

#### (1) Kaj je predoločen sistem enačb? Napišite primer. Kaj je rešitev predoločenega sistema po metodi najmanjših kvadratov?

Predoločen sistem enačb ima več enačb kot neznank. Primer takšnega sistema:
\[ 2x + 3y = 5 \]
\[ x - y = 2 \]
\[ 4x + y = 7 \]
Rešitev predoločenega sistema z metodo najmanjših kvadratov je tista, ki minimizira vsoto kvadratov razlik med dejanskimi izidi in napovedmi modela (minimizacija \( \|Ax - b\|^2 \)).

#### (2) Zapišite predoločen sistem enačb, ki določa regresijsko premico za podatke (xi, yi), i = 1, 2, ..., m.

Sistem za linearno regresijo:
\[ a x_1 + b = y_1 \]
\[ a x_2 + b = y_2 \]
\[ \vdots \]
\[ a x_m + b = y_m \]
Rešitev tega sistema daje koeficiente \(a\) (naklon) in \(b\) (presek z osjo y) regresijske premice, ki najbolje ustreza danim točkam v smislu metode najmanjših kvadratov.

#### (3) Kako izračunamo rešitev predoločenega sistema preko normalnega sistema?

Rešitev predoločenega sistema preko normalnega sistema se izračuna z:
\[ A^T Ax = A^T b \]
kjer \( A^T \) je transponirana matrika \( A \), in \( x \) je vektor neznank. Rešujemo za \( x \), ki minimizira kvadrat napake.

#### (4) Kaj je Moore-Penroseov inverz matrike in kako se z njim izraža rešitev predoločenega sistema po metodi najmanjših kvadratov?

Moore-Penroseov inverz, označen z \( A^+ \), je splošnitev inverza na matrike, ki niso kvadratne ali so singularne. Uporablja se za izračun rešitve najmanjših kvadratov predoločenega sistema z:
\[ x = A^+ b \]
kjer \( A^+ \) minimizira \( \|Ax - b\| \).

#### (5) Kaj lahko poveste o stabilnosti rešitve predoločenega sistema?

Stabilnost rešitve predoločenega sistema je odvisna od pogojenosti matrike \( A \). Če je matrika slabo pogojena (visoko pogojenostno število), so lahko rešitve nestabilne in močno občutljive na majhne spremembe v podatkih ali napake v izračunu.

#### (6) QR razcep matrike A in njegova uporaba

QR razcep je razgradnja matrike \( A \) na produkt dveh matrik \( Q \) in \( R \), kjer je \( Q \) ortogonalna matrika in \( R \) zgornje trikotna matrika. Za rešitev predoločenega sistema \( Ax = b \) po metodi najmanjših kvadratov uporabimo:
\[ R x = Q^T b \]
Najprej izračunamo \( Q^T b \), nato pa rešimo sistem \( Rx = Q^T b \) z obratno substitucijo.

#### (7) Klasična in modificirana Gram-Schmidtova ortogonalizacija

**Klasična Gram-Schmidtova ortogonalizacija** je proces, pri katerem iz danega sistema vektorjev ustvarimo ortogonalni sistem s projekcijami vektorjev na ortogonalni komplement predhodno obravnavanih vektorjev. **Modificirana Gram-Schmidtova ortogonalizacija** izboljša numerično stabilnost klasične metode tako, da ortogonalizira vsak vektor z vsemi že ortogonaliziranimi vektorji takoj, ko je ta generiran, kar zmanjšuje akumulacijo numeričnih napak.

#### (8) Householderjeva zrcaljenja za izračun QR razcepa

Householderjeva zrcaljenja so transformacije, ki se uporabljajo za postopno pretvorbo matrike v zgornje trikotno obliko \( R \) z uporabo ortogonalnih transformacij, ki odražajo vektorje okoli izbrane hiperravnine. Postopek začne z levo stranjo matrike in progresivno ustvarja zgornje trikotne elemente, pri čemer vsako zrcaljenje izniči elemente pod diagonalno.

#### (9) Givensove rotacije za izračun QR razcepa

Givensove rotacije so krožne transformacije, ki se uporabljajo za postopno uvajanje ničel v matriko z rotacijo vrstic ali stolpcev. Givensove rotacije so posebej ugodne pri redkih matrikah, kjer Householderjeva zrcaljenja lahko povzročijo povečanje gostote ničel, kar poveča računsko zahtevnost. Pri Givensovih rotacijah se vsaka rotacija nanaša lokalno, zato je izogibanje širjenju ničel učinkovitejše in ohranja redkost matrike.

### 4. ISKANJE LASTNIH VREDNOSTI MATRIK

#### (1) Kaj je dominantna lastna vrednost? Kako numerično iščemo dominantno lastno vrednost? Kako iščemo drugo dominantno lastno vrednost?

Dominantna lastna vrednost je tista lastna vrednost matrike, ki ima največjo absolutno vrednost. Numerično jo iščemo z **potenčno metodo**, kjer večkrat množimo matriko z začetnim vektorjem in normaliziramo rezultat, dokler ne konvergira k lastnemu vektorju, povezanemu z dominantno lastno vrednostjo. Za iskanje druge dominantne lastne vrednosti uporabimo deflacijo, ki odstrani vpliv že najdene dominantne lastne vrednosti iz matrike, in ponovno uporabimo potenčno metodo.

#### (2) Kaj je inverzna iteracija in zakaj se uporablja?

Inverzna iteracija je metoda za iskanje lastnih vrednosti blizu predhodno določene vrednosti \( \mu \). Ta metoda temelji na iteraciji z inverzom \( (A - \mu I)^{-1} \) in se uporablja za iskanje lastnih vrednosti, ki so natančno določene ali blizu specifične ciljne vrednosti, saj konvergira hitreje za lastne vrednosti blizu \( \mu \).

#### (3) Kaj je ortogonalna iteracija? Katero formo matrike izračunamo z ortogonalno iteracijo in kako iz nje razberemo lastne vrednosti?

Ortogonalna iteracija je postopek, kjer izvajamo množenje matrike z blokom vektorjev, sledi QR razcep rezultata. Izračunamo formo \( Q_k \) (ortogonalna matrika) in \( R_k \) (zgornje trikotna matrika). Z iterativnim izvajanjem postopka \( Q \) konvergira k matriki, katere stolpci so lastni vektorji izhodiščne matrike, lastne vrednosti pa lahko ocenimo iz diagonalnih elementov \( R \).

#### (4) Kaj je QR–iteracija z enojnim premikom? Kaj je cilj premika?

QR-iteracija z enojnim premikom je varianta QR-iteracije, kjer pred vsakim korakom odštejemo premik \( \mu \) od matrike \( A \), torej delamo z \( A - \mu I \). Premik je zasnovan tako, da pospeši konvergenco metode proti želeni lastni vrednosti, še posebej tistim, ki so bližje \( \mu \).

#### (5) Kako učinkovito numerično izračunamo vse lastne vrednosti matrike? Kakšna je cena?

Vse lastne vrednosti matrike lahko izračunamo s kombinacijo tehnik, kot so QR-iteracija, spektralna dekompozicija ali singularna vrednostna dekompozicija. Učinkovitost teh metod je odvisna od velikosti in lastnosti matrike, kot so redkost ali simetrija. Računska zahtevnost raste s povečevanjem velikosti matrike in želene natančnosti rezultatov.

### 5. REŠEVANJE NELINEARNIH ENAČB

#### (1) Opis bisekcije in število potrebnih korakov za natančnost \(10^{-10}\)

Bisekcija je metoda za iskanje ničle funkcije, ki deluje tako, da iterativno polovi interval \([a, b\]), kjer funkcija spreminja predznak. Število korakov, potrebnih za dosego natančnosti \(10^{-10}\), izračunamo s formulom:
\[ n = \lceil \log_2\left(\frac{b-a}{\epsilon}\right) \rceil \]
kjer je \( \epsilon = 10^{-10} \).

#### (2) Zaustavitveni kriteriji za bisekcijo

Ko je odvod funkcije na intervalu blizu 0, je smiselno uporabiti zaustavitveni kriterij, ki temelji na majhni spremembi intervala \([a, b]\), saj funkcija ničlo prečka počasi. Pri velikem odvodu je učinkoviteje uporabiti kriterij, ki temelji na majhnih spremembah vrednosti funkcije \(f(x)\), ker funkcija hitro spreminja vrednosti.

#### (3) Red konvergence

Red konvergence opisuje, kako hitro se približki izbrane metode približujejo dejanski rešitvi. Visok red konvergence pomeni, da se napaka z vsako iteracijo znatno zmanjšuje. V praksi to pomeni hitrejše doseganje natančnejših rešitev z manj koraki.

#### (4) Tangentna metoda in njen red konvergence

Tangentna metoda (Newtonova metoda) izračuna ničle z iteracijo:
\[ x\_{n+1} = x_n - \frac{f(x_n)}{f'(x_n)} \]
Red konvergence te metode je kvadratičen (\(O(h^2)\)), kar pomeni, da se natančnost rešitve z vsako iteracijo kvadratično povečuje, če je začetni približek dovolj blizu prave ničle.

#### (5) Sekantna metoda in njen red konvergence

Sekantna metoda je podobna tangentni metodi, vendar ne zahteva odvoda funkcije. Namesto tega uporablja dve začetni točki in izračuna:
\[ x*{n+1} = x_n - f(x_n) \frac{x_n - x*{n-1}}{f(x*n) - f(x*{n-1})} \]
Red konvergence sekantne metode je superlinearen, približno \(1.618\) (zlato razmerje), kar je hitrejše od linearne konvergence, vendar počasnejše od kvadratične.

#### (6) Izpeljava in opis metode regula falsi

Metoda regula falsi (metoda lažne pozicije) je iterativna tehnika za iskanje ničel funkcije, ki se podobno kot bisekcija osredotoča na interval, kjer funkcija spreminja predznak. Metoda uporablja linearno interpolacijo med končnima točkama intervala in izbere ničlo linearne interpolacije kot naslednji približek. Iteracija poteka po formuli:
\[ x*{n+1} = x_n - f(x_n) \frac{x*{n} - x*{n-1}}{f(x_n) - f(x*{n-1})} \]
kjer \( x*n \) in \( x*{n-1} \) sta zadnji dve oceni ničle.

#### (7) Fiksne točke iteracijske funkcije \( g \)

Fiksna točka funkcije \( g \) je vrednost \( x \), za katero velja \( g(x) = x \). Fiksne točke so **privlačne**, če je absolutna vrednost odvoda \( g' \) pri \( x \) manjša od 1 (\(|g'(x)| < 1\)), saj približki konvergirajo k fiksni točki. So **odbojne**, če je \( |g'(x)| > 1 \), kar povzroči divergenco od fiksne točke.

#### (8) Navadna iteracija za iskanje ničel funkcije \( f \)

Navadna iteracija za iskanje ničle funkcije \( f \) lahko poteka s transformacijo \( x\_{n+1} = g(x_n) \), kjer je \( g(x) \) neka funkcija, izpeljana iz \( f \). Hitrost konvergence je:

- **Linearna**, če je \( |g'(x)| \) konstanta manjša od 1.
- **Kvadratična**, če je \( g'(x) = 0 \) pri fiksni točki.
- **Kubična**, če so izpolnjeni pogoji višjih odvodov.

#### (9) Iteracijske metode za reševanje nelinearnih enačb

Ena od priljubljenih metod je **Newtonova metoda** za reševanje nelinearnih enačb, ki iterativno izboljšuje približke z uporabo tangent k funkciji \( f \), izračunanih z odvodom \( f \). Formula za iteracijo je:
\[ x\_{n+1} = x_n - \frac{f(x_n)}{f'(x_n)} \]

#### (10) Kvazi-Newtonove metode

Kvazi-Newtonove metode so razred metod za reševanje nelinearnih enačb, ki poskušajo ohraniti prednosti Newtonove metode, vendar brez potrebe po natančnem izračunu drugega odvoda (Hessejeve matrike). **Metoda BFGS** je ena izmed teh, ki uporablja približke za inverz Hessejeve matrike za pospešitev konvergence.

#### (11) Povezava med reševanjem enačb in optimizacijo

Reševanje sistemov enačb je tesno povezano z optimizacijo, saj iskanje ničel gradienta optimizacijske funkcije neposredno ustreza reševanju nelinearnih enačb. Tehnike, kot so Newtonova in kvazi-Newtonova metoda, se pogosto uporabljajo tako za iskanje ničel enačb kot za iskanje ekstremov funkcij.

### 6. POLINOMSKA INTERPOLACIJA IN APROKSIMACIJA

#### (1) Sistem enačb za interpolacijski polinom in stabilnost sistema

Za interpolacijo 5 točk \( (x_i, y_i) \), i = 0, 1, ..., 4, potrebujemo polinom četrte stopnje (stopnja \( n = 4 \)), saj je stopnja polinoma enaka številu točk minus ena. Sistem enačb, ki določa koeficiente polinoma, lahko postane nestabilen, še posebej pri visokih stopnjah in če so točke umeščene zelo blizu skupaj ali zelo enakomerno (npr. če opazimo Rungejev pojav).

#### (2) Lagrangeova oblika interpolacijskega polinoma in njene pomanjkljivosti

Lagrangeov interpolacijski polinom je definiran kot:
\[ P(x) = \sum*{i=0}^n y_i \prod*{\substack{j=0 \\ j \neq i}}^n \frac{x - x_j}{x_i - x_j} \]
**Pomanjkljivosti:** Metoda je računsko zahtevna, saj za vsako spremembo točk ali dodajanje nove točke zahteva ponovno izračunavanje celotnega polinoma. Prav tako je občutljiva na numerične napake pri velikem številu točk.

#### (3) Newtonova oblika interpolacijskega polinoma in deljene diference

Newtonov interpolacijski polinom uporablja deljene diference in je zapisan kot:
\[ P(x) = f[x_0] + f[x_0, x_1](x - x*0) + \ldots + f[x_0, x_1, \ldots, x_n](x - x_0)\ldots(x - x*{n-1}) \]
Deljene diference se izračunajo rekurzivno in so uporabne za dodajanje novih točk brez ponovnega izračuna celotnega polinoma. **Prednosti:** Večja fleksibilnost in manjša občutljivost na dodajanje točk v primerjavi z Lagrangeovo metodo.

#### (4) Večkratne interpolacijske točke in njihov vpliv

Večkratne interpolacijske točke omogočajo, da se polinom ujema ne samo z vrednostmi funkcije, ampak tudi z njenimi odvodi v danih točkah. Deljene diference, kot so \( f[x_0, x_0] \), predstavljajo odvode funkcije v točki \( x_0 \).

#### (5) Povečanje stopnje interpolacijskega polinoma in prileganje funkciji

Višanje stopnje interpolacijskega polinoma ne zagotavlja vedno boljšega prileganja, zlasti za kompleksne funkcije ali na večjih intervalih, kjer lahko pride do oscilacij (Rungejev pojav).

#### (6) Ocena napake interpolacijskega polinoma

Napaka interpolacijskega polinoma \( P(x) \) za funkcijo \( f \) je določena z:
\[ E(x) = f(x) - P(x) \]
Napaka pri interpolaciji s polinomom stopnje \( n \) je odvisna od \( (n+1) \)-tega odvoda funkcije \( f \) in velikosti intervala, v katerem interpoliramo.

#### (7) Gaussove kvadraturne formule

Gaussove kvadraturne formule so napredne metode za numerično integracijo, ki uporabljajo optimalno izbrane točke in uteži za izračun integralov. Te točke (vozli) in uteži

### 7. NUMERIČNA INTEGRACIJA

#### (1) Osnovno trapezno in Simpsonovo pravilo ter njuni napaki

**Osnovno trapezno pravilo** aproksimira integral funkcije tako, da izračuna površino trapeza, ki ga oblikujeta graf funkcije in x-os med dvema točkama. Formula je:
\[ \int_a^b f(x) \, dx \approx \frac{b-a}{2} (f(a) + f(b)) \]
Napaka tega pravila je \(O(h^3)\) za en korak, kjer je \(h = b-a\).

**Osnovno Simpsonovo pravilo** uporablja parabolično interpolacijo skozi tri točke za izračun integrala in je natančnejše. Formula je:
\[ \int_a^b f(x) \, dx \approx \frac{b-a}{6} [f(a) + 4f\left(\frac{a+b}{2}\right) + f(b)] \]
Napaka je \(O(h^5)\), kjer je \(h = b-a\).

#### (2) Sestavljeno trapezno in Simpsonovo pravilo

**Sestavljeno trapezno pravilo** deli interval integracije na manjše segmente in uporablja osnovno trapezno pravilo na vsakem segmentu, kar zmanjšuje napako.
**Sestavljeno Simpsonovo pravilo** prav tako deli interval na segmente, vendar mora biti število segmentov sodo. Uporablja osnovno Simpsonovo pravilo na vsakem paru sosednjih segmentov za izboljšanje natančnosti.

#### (3) Red kvadraturne formule in metoda nedoločenih koeficientov

Red kvadraturne formule pomeni, da formula natančno izračuna integral polinomov do določene stopnje. Metoda nedoločenih koeficientov se uporablja za določanje uteži in vozlišč v kvadraturni formuli tako, da formula točno integrira polinome najvišje možne stopnje.

#### (4) Določanje pravega koraka v trapeznem pravilu

Pravi korak \(h\) v trapeznem pravilu določimo glede na želeno natančnost in lastnosti funkcije. Korak se lahko prilagodi na podlagi ocene napake, ki pove, kako hitro se spreminja funkcija \(f(x)\).

#### (5) Adaptivno trapezno pravilo

Adaptivno trapezno pravilo samodejno prilagaja korak \(h\) med izračunom integrala za doseganje želene natančnosti. Pravilo oceni napako v trenutnem koraku in, če je napaka prevelika, zmanjša korak, če pa je napaka majhna, poveča korak za naslednje segmente, s čimer optimizira celotno računsko delo.

#### (6) Rombergova metoda

Rombergova metoda je tehnika za izboljšanje natančnosti numeričnih integracij, ki izhaja iz trapeznega pravila. **Osnovni princip** je uporaba Richardsonove ekstrapolacije za zaporedne približke integrala, ki so izračunani z vedno manjšimi koraki. Začnemo s trapeznim pravilom za grob korak, nato korak postopoma polovimo in izračunamo nove približke. Ti približki se nato kombinirajo za izboljšanje natančnosti.

**Primer uporabe:**

1. Izračunaj integral z osnovnim trapeznim pravilom za korak \( h \).
2. Polovi korak in ponovi izračun.
3. Uporabi Richardsonovo ekstrapolacijo za izboljšanje ocene integrala.

#### (7) Vozli in uteži v kvadraturnem pravilu; prednosti Gaussove kvadrature

Vozli v kvadraturnem pravilu so točke, v katerih funkcijo ovrednotimo, uteži pa so koeficienti, s katerimi pomnožimo vrednosti funkcije za izračun integrala. **Gaussova kvadraturna pravila** so učinkovitejša od Newton-Cottesovih pravil, ker izbirajo optimalne vozle in uteži, ki maksimizirajo stopnjo točnosti za dane vozle. To pomeni, da lahko Gaussova pravila z manjšim številom vozlov dosežejo višjo natančnost kot ekvivalentna Newton-Cottesova pravila.

#### (8) Numerični izračun dvojnega integrala na pravokotniku

Dvojni integral na pravokotniku se običajno izračuna z iteriranjem enodimenzionalnega integracijskega pravila (npr. trapeznega ali Simpsonovega) najprej v eni smeri in nato v drugi. Izračunamo:
\[ \int*{a}^{b} \int*{c}^{d} f(x,y) \, dx \, dy \]
kjer najprej integriramo po \( x \) za fiksni \( y \), nato rezultate integriramo po \( y \).

#### (9) Numerični izračun večkratnih integralov na poljubnem območju

Za večkratne integrale na kompleksnih območjih se pogosto uporabljajo metode, kot so Monte Carlo ali adaptivne kvadraturne metode, ki se prilagajajo obliki območja. Napaka pri teh metodah je odvisna od števila uporabljenih točk in metode integracije. Računska zahtevnost za doseganje napake \( \epsilon \) narašča s kompleksnostjo območja in dimenzijo integrala.

### 8. REŠEVANJE DIFERENCIALNIH ENAČB

#### (1) Eulerjeva metoda za reševanje začetnega problema

Eulerjeva metoda je osnovna numerična metoda za reševanje diferencialnih enačb oblike \( y' = f(x, y) \) s začetnim pogojem \( y(a) = y*a \). Metoda napreduje z iterativnim izračunom:
\[ y*{n+1} = y_n + h f(x_n, y_n) \]
kjer \( h \) predstavlja korak, \( x_n \) je trenutna točka, in \( y_n \) trenutna vrednost rešitve.

#### (2) Ideja Runge-Kutta metod in napaka

Runge-Kutta metode izboljšajo Eulerjevo metodo s točnejšim izračunom sprememb \( y \) z uporabo več vmesnih korakov. Napaka metode reda \( k \) je \( O(h^{k+1}) \), kjer \( k \) predstavlja število stopenj metode (npr. pri RK4 je \( k = 4 \), zato napaka znaša \( O(h^5) \)).

#### (3) Adaptivna metoda in DOPRI5

Adaptivne metode prilagajajo velikost koraka \( h \) glede na lokalno napako rešitve. **DOPRI5** je priljubljena adaptivna Runge-Kutta metoda petega reda, ki dinamično prilagaja korak, da optimizira natančnost in učinkovitost. Ima vgrajen nadzor napake, ki omogoča natančnejše reševanje.

#### (4) Adams-Bashforthova metoda in napaka

Adams-Bashforthove metode so eksplicitne večkorakne metode, ki uporabljajo pretekle vrednosti \( f(x, y) \) za napovedovanje novih vrednosti. Napaka metode reda \( k \) je \( O(h^k) \), kar pomeni, da več korakov vodi do večje natančnosti.

#### (5) Adams-Moultonova metoda in napaka

Adams-Moultonove metode so implicitne večkorakne metode, ki vključujejo trenutno in pretekle vrednosti \( f(x, y) \) za izračun \( y*{n+1} \). Napaka metode reda \( k \) je \( O(h^{k+1}) \). Metoda je implicitna, ker zahteva rešitev algebrske enačbe za \( y*{n+1} \) na vsakem koraku.

#### (6) ABM prediktor-korektor metoda in napaka

ABM (Adams-Bashforth-Moulton) metoda kombinira prediktor (Adams-Bashforth) za inicialno oceno in korektor (Adams-Moulton) za končno prilagoditev. Napaka te kombinirane metode reda \( k \) je \( O(h^{k+1}) \).

#### (7) Strelska metoda za reševanje robnih problemov

Strelska metoda pretvori robni problem v začetni problem z ugibanjem začetnih pogojev. Metoda iterativno prilagaja začetne pogoje, dokler rešitev ne ustreza robnim pogojem. Primerna je za linearni ali nelinearni robni problem.

### 1. UVOD V NUMERIČNO RAČUNANJE

#### (1) Kaj je strojni epsilon? Kaj je osnovna zaokrožitvena napaka?

Strojni epsilon je najmanjša razlika med 1 in naslednjim večjim številom. Osnovna zaokrožitvena napaka je napaka, ki nastane, ko se realna števila zaokrožijo na najbližje število.

#### (2) Katere napake pri numeričnem računanju poznamo?

Poznamo več vrst napak, vključno z:
- zaokrožitvena napaka (računanje s približki in zaokroževanje), 
- neodstranljiva napaka (nenatančni začetni podatki), 
- napaka metode (npr. če neskončni proces aproksimiramo s končnim).

#### (3) Katere so osnovne računske operacije v IEEE in kateri dve operaciji sta problematični s stališča numerične matematike?

Osnovne računske operacije po standardu IEEE vključujejo seštevanje, odštevanje, množenje, deljenje in korenenje. Problematični operaciji sta deljenje in odštevanje, še posebej, ko se deli ali odšteva zelo majhne številke, kar lahko vodi v izgubo natančnosti.

#### (4) Kaj je relativno direktno stabilna metoda in kaj relativno obratno stabilna metoda? Navedite primer metode, ki je relativno direktno in obratno stabilna.

**Relativno direktno stabilna metoda** zagotavlja, da majhne spremembe v vhodnih podatkih povzročijo le majhne spremembe v izhodnih podatkih.

**Relativno obratno stabilna metoda** zagotavlja, da so izhodni podatki natančni rešitvi malo spremenjenih vhodnih podatkov.

### Primer metode, ki je relativno direktno in obratno stabilna:

Gaussova eliminacija brez pivotiranja je primer metode, ki je tako relativno direktno kot obratno stabilna za diagonalo dominantne matrike.

**Dokaz:**

1. **Relativno direktno stabilna:**
   Gaussova eliminacija brez pivotiranja za diagonalo dominantne matrike zagotavlja, da majhne spremembe v vhodnih podatkih povzročijo le majhne spremembe v izhodnih podatkih.

2. **Relativno obratno stabilna:**
   Rešitev, ki jo dobimo z Gaussovo eliminacijo brez pivotiranja, je natančna za malo spremenjene vhodne podatke. To pomeni, da rešitev natančno ustreza sistemu, ki je malo spremenjen v primerjavi s prvotnim sistemom.

### 2. REŠEVANJE LINEARNIH SISTEMOV

#### (1) Zapisite splosen kvadraten sistem linearnih enacb in ga prepisite v matricno obliko. Kdaj  je tak sistem resljiv/enolicno resljiv/ni resljiv? Koliko operacij je potrebnih za izracun produkta matrike z vektorjem? Kaj pa za produkt dveh matrik?

Splošen kvadraten sistem linearnih enačb zapisujemo kot $Ax = b$, kjer je:

- $A$ matrika koeficientov velikosti $n \times n$,
- $x$ vektor neznank,
- $b$ vektor konstant.

Matrično obliko lahko zapišemo kot:

```math
\begin{bmatrix}
a_{11} & a_{12} & \cdots & a_{1n} \\
a_{21} & a_{22} & \cdots & a_{2n} \\
\vdots & \vdots & \ddots & \vdots \\
a_{n1} & a_{n2} & \cdots & a_{nn}
\end{bmatrix}
\begin{bmatrix}
x_1 \\
x_2 \\
\vdots \\
x_n
\end{bmatrix}
=
\begin{bmatrix}
b_1 \\
b_2 \\
\vdots \\
b_n
\end{bmatrix}
```

**Resljivost:**

- Sistem je **enolično rešljiv**, če je determinanta matrike $A$ neničelna.
- Sistem ni rešljiv ali ima neskončno mnogo rešitev, če je determinanta matrike $A$ enaka nič.

**Število operacij:**

- Produkt matrike z vektorjem zahteva $n^2$ operacij.
- Produkt dveh matrik $n \times n$ zahteva $n^3$ operacij.

#### (2) Kaj je Gaussova eliminacija in koliko osnovnih računskih operacij je potrebnih za njeno izvedbo?

Gaussova eliminacija je metoda za reševanje sistemov linearnih enačb z reduciranjem matrike na zgornje trikotno obliko. Potrebno je $O(n^3)$ osnovnih računskih operacij za izvedbo.

#### (3) Opisite elementarne eliminacije in razlozite, kako z njihovo pomocjo unicimo elemente v danem vektorju x. Kako izracunamo inverz elementarne eliminacije in kako izracunamo produkt dveh elementarnih eliminacij?

Elementarne eliminacije vključujejo vrstične operacije kot so zamenjava, množenje vrstice z skalarjem in dodajanje večkratnika ene vrstice k drugi, da se dosežejo ničle pod glavno diagonalo.

**Inverz in produkt eliminacij:**

- Inverz elementarne eliminacije dobimo z obratno operacijo.
- Produkt dveh elementarnih eliminacij se izračuna z zaporednim izvajanjem obeh operacij na enoto matriko.

#### (4) Kaj je LU razcep matrike A (brez pivotiranja) in kako ga izracunamo? Koliko operacij je potrebnih za njegov izracun? Kdaj LU razcep brez pivotiranja obstaja? Napisite primer matrike, pri kateri se ne da izracunati LU razcepa brez pivotiranja.

LU razcep brez pivotiranja razdeli matriko $A$ na produkt spodnje trikotne matrike $L$ in zgornje trikotne matrike $U$. Izračun zahteva približno $O(n^3)$ operacij. Obstaja, če so vsi glavni minori matrike $A$ neničelni.

Primer, kjer LU razcep brez pivotiranja ni možen: Matrika:
```math
\begin{bmatrix}
0 & 1 \\
1 & 1 \
\end{bmatrix}
```
ne omogoča LU razcepa brez pivotiranja zaradi ničelnega elementa na mestu $a_{11}$.

#### (5) Kaj je zgornjetrikoten sistem linearnih enacb? Kaj je prema in kaj obratna substitucija za zgornjetrikoten sistem? Koliko operacij zahtevata?

Zgornjetrikoten sistem ima ničle pod glavno diagonalo matrike.

**Substitucija:**

- **Premo substitucija** se ne uporablja; relevantna je le za spodnjetrikotne sisteme.
- **Obratna substitucija** se uporablja za reševanje zgornjetrikotnega sistema. Začne se z zadnjo enačbo.

Potrebno je $O(n^2)$ operacij za reševanje zgornjetrikotnega sistema.

#### (6) Kako s pomocjo LU razcepa matrike A izracunamo resitev linearnega sistema enacb $Ax = b$ ? Koliko operacij zahteva?

Za reševanje sistema $Ax = b$ s pomočjo LU razcepa najprej razcepimo matriko $A$ na produkt $LU$, kjer je $L$ spodnjetrikotna matrika, $U$ pa zgornjetrikotna matrika. Reševanje sistema poteka v dveh korakih:

1. Rešimo $Ly = b$ za $y$ z uporabo premega vstavljanja.
2. Rešimo $Ux = y$ za $x$ z uporabo obratnega vstavljanja.

$O(n^3)$ operacij za LU razcep. $O(n^2)$ operacij za rešitev sistemov $Ly = b$ in $Ux = y$. 

#### (7) Kaj je LU razcep matrike A z delnim pivotiranjem? Zakaj ga uvedemo? Opisite postopek za njegov izracun. Kako s pomocjo tega razcepa izracunamo resitev linearnega sistema enacb $Ax = b$ ? Koliko operacij zahteva resevanje sistema $Ax = b$ prek LU razcepa z delnim pivotiranjem?

**Delni pivot** pri LU razcepu vključuje izbiro največjega elementa v stolpcu kot pivot, da se izogne težavam z numerično stabilnostjo. Postopek izračuna:

1. Izberemo največji element v stolpcu pod ali na diagonalni liniji.
2. Zamenjamo trenutno vrstico z vrstico, ki vsebuje največji element.
3. Nadaljujemo z razcepom kot pri standardnem LU razcepu.

Za reševanje $Ax = b$ s to metodo najprej izračunamo $Ly = Pb$ (kjer je $P$ permutacijska matrika zaradi pivotiranja), nato rešimo $Ux = y$. Delno pivotiranje prinese dodatnih $O(n^2)$ operacij, ampak to bistveno ne vpliva na asimptotično časovno kompleksnost LU razcepa - $O(n^3)$

#### (8) Kaj je LU razcep s kompletnim pivotiranjem in zakaj se v praksi ne uporablja?

LU razcep s **kompletnim pivotiranjem** vključuje izbiro največjega elementa iz celotne preostale matrike (ne samo stolpca) za pivotiranje. Čeprav je ta metoda zelo stabilna, se redko uporablja zaradi visoke računske zahtevnosti, ki lahko bistveno upočasni postopek, še posebej pri velikih matrikah.

#### (9) Kaj lahko poves o stabilnosti resevanja zgornjetrikotnega sistema prek obratne/preme substitucije?

Stabilnost reševanja zgornjetrikotnega sistema z **obratno substitucijo** je običajno visoka, saj postopek naravno preprečuje deljenje z zelo majhnimi števili, razen če je zgornjetrikotna matrika slabo pogojena. V primeru spodnjetrikotnih sistemov, kjer uporabimo premo substitucijo, je tudi stabilnost običajno dobra, razen v primerih slabo pogojenih matrik ali zelo majhnih diagonalnih elementov.

#### (10) Kaj je pivotna rast? Kaj nam pivotna rast pove? Ali je pivotna rast pri delnem pivotiranju omejena? Če da, skiciraj dokaz tega dejstva.

**Pivotna rast** meri, kako se elementi matrike povečajo med LU razcepom s pivotiranjem. Visoka pivotna rast lahko pomeni nestabilnost metode.

Pri delnem pivotiranju je pivotna rast omejena, saj vedno izberemo največji element v stolpcu za pivot, kar omeji vrednosti v zgornji trikotni matriki $U$.

**Dokaz:**
- **Delno pivotiranje**: Vedno zamenjamo vrstico z največjim elementom v trenutnem stolpcu, kar omeji rast elementov.
- **Omejitev**: Elementi v $U$ ne postanejo večji od elementov v izvirni matriki $A$, kar zagotavlja stabilnost.

Zaključek: Delno pivotiranje omeji pivotno rast, kar pomeni, da LU razcep ostane stabilen.

#### (11) Kaj lahko poves o stabilnosti racunanja LU razcepa brez pivotiranja/z delnim pivotiranjem/s kompletnim pivotiranjem?

- **Brez pivotiranja:** Lahko je nestabilno, če v matriki obstajajo zelo majhni diagonalni elementi.
- **Z delnim pivotiranjem:** Večja stabilnost, saj izbor največjega elementa v stolpcu kot pivot zmanjša problem majhnih pivotov.
- **S kompletnim pivotiranjem:** Največja stabilnost, vendar zahtevnejša zaradi iskanja največjega elementa v celotni preostali matriki.

#### (12) Kaj je razcep Choleskega matrike in za katere matrike se razcep izvede? Kaksna je racunska zahtevnost in kaksna je stabilnost v primerjavi z LU razcepom.

Razcep Choleskega se uporablja za simetrične, pozitivno definitne matrike, kjer matriko $A$ razdelimo na $A = LL^T$, kjer je $L$ spodnjetrikotna matrika. Računska zahtevnost Choleskega razcepa je $O(n^3)$ . Ta razcep je običajno bolj stabilen in manj računsko zahteven v primerjavi z LU razcepom.


#### (13) Kaj je vektorska norma? Navedite nekaj primerov vektorskih norm? Kaj je uporaba vektorskih norm v numericni matematiki?

Vektorska norma je preslikava iz vektorja v množico realnih/kompleksnih števil. Primeri:

- Evklidska norma $\|x\|_2$
- Maksimalna norma $\|x\|_\infty$
- Manhattan norma $\|x\|_1$

Uporabljajo se za oceno velikosti napak, konvergenco algoritmov in stabilnost sistemov.

#### (14) Kaj je matricna norma? Na kaksen nacin vsaka vektorska norma porodi pripadajoco matricno normo? Navedite nekaj primerov matricnih norm. Kje jih uporabljamo v numericni matematiki?

Matrična norma, izpeljana iz vektorskih norm, ocenjuje velikost matrik. Primeri matričnih norm:

- 1-norma
- Frobeniusova norma
- Spektralna norma

Matrične norme so ključne pri analizi numerične stabilnosti algoritmov in ocenjevanju občutljivosti rešitev.

#### (15) Kaj je pogojenostno stevilo matrike? Kako je pogojenostno stevilo povezano s stabilnostjo resevanja sistemov z eno od direktnih metod?

Pogojenostno število matrike meri, kako vhodne napake vplivajo na izhodne rezultate. Visoko pogojenostno število pomeni, da majhne vhodne napake lahko povzročijo velike izhodne napake, kar lahko pokaže na numerično nestabilnost algoritma.

#### (16) Katere iterativne metode za resevanje linearnih sistemov poznas? Eno od njih podrobno opisi.

- Jacobi
- Gauss-Seidel
- SOR
- SSOR
- konjugirani gradienti

Primer iterativne metode je **metoda konjugiranih gradientov**, ki se uporablja predvsem za reševanje velikih, redkih sistemov simetričnih, pozitivno definitnih matrik. Metoda izračuna rešitev z minimizacijo funkcije v obliki kvadratnega polinoma, pri čemer koristi lastnosti ortogonalnosti.

### 3. PREDOLOČENI SISTEMI

#### (1) Kaj je predoločen sistem enačb? Napišite primer. Kaj je rešitev predoločenega sistema po metodi najmanjših kvadratov?

Predoločen sistem enačb ima več enačb kot neznank. Primer takšnega sistema:
- $2x + 3y = 5$
- $x - y = 2$
- $4x + y = 7$

Rešitev predoločenega sistema z metodo najmanjših kvadratov je tista, ki minimizira vsoto kvadratov razlik med dejanskimi izidi in napovedmi modela (minimizacija $\|Ax - b\|^2$).

#### (2) Zapišite predoločen sistem enačb, ki določa regresijsko premico za podatke $(x_i, y_i)$ , i = 1, 2, ..., m.

Sistem za linearno regresijo:
- $ax_1 + b = y_1$
- $ax_2 + b = y_2$
- $\vdots$
- $ax_m + b = y_m$

Rešitev tega sistema daje koeficiente $a$ (naklon) in $b$ (presek z osjo y) regresijske premice, ki najbolje ustreza danim točkam v smislu metode najmanjših kvadratov.

#### (3) Kako izračunamo rešitev predoločenega sistema preko normalnega sistema?

Rešitev predoločenega sistema preko normalnega sistema se izračuna z:
$A^T Ax = A^T b$
kjer $A^T$ je transponirana matrika $A$, in $x$ je vektor neznank. Rešujemo za $x$, ki minimizira kvadrat napake.

#### (4) Kaj je Moore-Penroseov inverz matrike in kako se z njim izraža rešitev predoločenega sistema po metodi najmanjših kvadratov?

Moore-Penroseov inverz, označen z $A^+$, je splošnitev inverza na matrike, ki niso kvadratne ali so singularne. Uporablja se za izračun rešitve najmanjših kvadratov predoločenega sistema z:
$x = A^+ b$
kjer $A^+$ minimizira $\|Ax - b\|$.

#### (5) Kaj lahko poveste o stabilnosti rešitve predoločenega sistema?

Stabilnost rešitve predoločenega sistema je odvisna od pogojenosti matrike $A$. Če je matrika slabo pogojena (visoko pogojenostno število), so lahko rešitve nestabilne in močno občutljive na majhne spremembe v podatkih ali napake v izračunu.

#### (6) Kaj je QR razcep matrike A in kako z njegovo pomocjo pridemo do resitve predolocenega sistema po metodi najmanjsih kvadratov?

QR razcep je razgradnja matrike $A$ na produkt dveh matrik $Q$ in $R$, kjer je $Q$ ortogonalna matrika in $R$ zgornje trikotna matrika. Za rešitev predoločenega sistema $Ax = b$ po metodi najmanjših kvadratov uporabimo:
$R x = Q^T b$
Najprej izračunamo $Q^T b$, nato pa rešimo sistem $Rx = Q^T b$ z obratno substitucijo.

#### (7) Kaj je klasična Gram-Schmidtova ortogonalizacija in kaj je razlika med klasično in modificirano Gram-Schmidtovo ortogonalizacijo?

Postopek, ki naredi stolpce matrike pravokotne drug na drugega. Začnemo s prvim stolpcem. Drugega dobimo tako, da odštejemo pravokotno projekcijo na prvega. Tretjega dobimo tako, da odštejemo pravokotni projekciji na prva dva... 
Tako dobljene vektorje na koncu še normiramo. 
Modificirana varianta je bolj numerično stabilna

#### (8) Kaj so Householderjeva zrcaljenja in kako s pomocjo njih izracunamo QR razcep matrike?

Householderjeva zrcaljenja so transformacije, ki se uporabljajo za postopno pretvorbo matrike v zgornje trikotno obliko \( R \) z uporabo ortogonalnih transformacij, ki odražajo vektorje okoli izbrane hiperravnine. Postopek začne z levo stranjo matrike in progresivno ustvarja zgornje trikotne elemente, pri čemer vsako zrcaljenje izniči elemente pod diagonalno.

#### (9) Kaj so Givensove rotacije in kako jih uporabimo za izracun QR razcepa matrike? Kdaj je to ugodnejse od uporabe Houselderjevih zrcaljenj? 

Givensove rotacije so krožne transformacije, ki se uporabljajo za postopno uvajanje ničel v matriko z rotacijo vrstic ali stolpcev. Givensove rotacije so posebej ugodne pri redkih matrikah, kjer Householderjeva zrcaljenja lahko povzročijo povečanje gostote ničel, kar poveča računsko zahtevnost. Pri Givensovih rotacijah se vsaka rotacija nanaša lokalno, zato je izogibanje širjenju ničel učinkovitejše in ohranja redkost matrike.

### 4. ISKANJE LASTNIH VREDNOSTI MATRIK

#### (1) Kaj je dominantna lastna vrednost? Kako numerino iscemo dominantno lastno vrednost? Kako iscemo drugo dominantno lastno vrednost? 

Dominantna lastna vrednost je tista lastna vrednost matrike, ki ima največjo absolutno vrednost. Numerično jo iščemo z **potenčno metodo**, kjer večkrat množimo matriko z začetnim vektorjem in normaliziramo rezultat, dokler ne konvergira k lastnemu vektorju, povezanemu z dominantno lastno vrednostjo. Za iskanje druge dominantne lastne vrednosti uporabimo deflacijo, ki odstrani vpliv že najdene dominantne lastne vrednosti iz matrike, in ponovno uporabimo potenčno metodo.

#### (2) Kaj je inverzna iteracija in zakaj se uporablja?

Inverzna iteracija je metoda za iskanje lastnih vrednosti blizu predhodno določene vrednosti $\mu$. Ta metoda temelji na iteraciji z inverzom $(A - \mu I)^{-1}$ in se uporablja za iskanje lastnih vrednosti, ki so natančno določene ali blizu specifične ciljne vrednosti, saj konvergira hitreje za lastne vrednosti blizu $\mu$.

#### (3) Kaj je ortogonalna iteracija? Katero formo matrike izračunamo z ortogonalno iteracijo in kako iz nje razberemo lastne vrednosti?

Ortogonalna iteracija je postopek, kjer izvajamo množenje matrike z blokom vektorjev, sledi QR razcep rezultata. Izračunamo formo $Q_k$ (ortogonalna matrika) in $R_k$ (zgornje trikotna matrika). Z iterativnim izvajanjem postopka $Q$ konvergira k matriki, katere stolpci so lastni vektorji izhodiščne matrike, lastne vrednosti pa lahko ocenimo iz diagonalnih elementov $R$.

#### (4) Kaj je QR–iteracija z enojnim premikom? Kaj je cilj premika?

QR-iteracija z enojnim premikom je varianta QR-iteracije, kjer pred vsakim korakom odštejemo premik $\mu$ od matrike $A$, torej delamo z $A - \mu I$. Premik je zasnovan tako, da pospeši konvergenco metode proti želeni lastni vrednosti, še posebej tistim, ki so bližje $\mu$.

#### (5) Kako učinkovito numerično izračunamo vse lastne vrednosti matrike? Kakšna je cena?

Vse lastne vrednosti matrike lahko izračunamo s kombinacijo tehnik, kot so QR-iteracija, spektralna dekompozicija ali singularna vrednostna dekompozicija. Učinkovitost teh metod je odvisna od velikosti in lastnosti matrike, kot so redkost ali simetrija. Računska zahtevnost raste s povečevanjem velikosti matrike in želene natančnosti rezultatov.

### 5. REŠEVANJE NELINEARNIH ENAČB

#### (1) Opis bisekcije in število potrebnih korakov za natančnost $10^{-10}$

Bisekcija je metoda za iskanje ničle funkcije, ki deluje tako, da iterativno polovi interval $[a, b]$, kjer funkcija spreminja predznak. Število korakov, potrebnih za dosego natančnosti $10^{-10}$, izračunamo s formulo:
$n = \lceil \log_2\left(\frac{b-a}{\epsilon}\right) \rceil$ kjer je $\epsilon = 10^{-10}$.

#### (2) Kaj je dobro vzeti za zaustavitveni kriterij bisekciji v primeru, ko je odvod funkcije na danem intervalu blizu 0? Kaj pa, ko je odvod relativno velik?

Ko je odvod funkcije na intervalu blizu 0, je smiselno uporabiti zaustavitveni kriterij, ki temelji na majhni spremembi intervala $[a, b]$, saj funkcija ničlo prečka počasi. Pri velikem odvodu je učinkoviteje uporabiti kriterij, ki temelji na majhnih spremembah vrednosti funkcije $f(x)$, ker funkcija hitro spreminja vrednosti.


#### (3)  Kaj pomeni red konvergence? Kako se red konvergence pozna pri dejanski uporabi metode?

Red konvergence opisuje, kako hitro se približki izbrane metode približujejo dejanski rešitvi. Visok red konvergence pomeni, da se napaka z vsako iteracijo znatno zmanjšuje. V praksi to pomeni hitrejše doseganje natančnejših rešitev z manj koraki.

#### (4) Izpeljite in opisite tangentno metodo ter dolocite red konvergence.

Tangentna metoda (Newtonova metoda) izračuna ničle z iteracijo:
$x_{n+1} = x_n - \frac{f(x_n)}{f'(x_n)}$
Red konvergence te metode je kvadratičen $O(h^2)$, kar pomeni, da se natančnost rešitve z vsako iteracijo kvadratično povečuje, če je začetni približek dovolj blizu prave ničle.

#### (5) Izpeljite in opisite sekantno metodo ter dolocite red konvergence. 

Sekantna metoda je podobna tangentni metodi, vendar ne zahteva odvoda funkcije. Namesto tega uporablja dve začetni točki in izračuna:
$x_{n+1} = x_n - f(x_n) \frac{x_n - x_{n-1}}{f(x_n) - f(x_{n-1})}$
Red konvergence sekantne metode je superlinearen, približno $1.618$ (zlato razmerje), kar je hitrejše od linearne konvergence, vendar počasnejše od kvadratične.

#### (6) Izpeljava in opis metode regula-falsi

Metoda regula falsi (metoda lažne pozicije) je iterativna tehnika za iskanje ničel funkcije, ki se podobno kot bisekcija osredotoča na interval, kjer funkcija spreminja predznak. Metoda uporablja linearno interpolacijo med končnima točkama intervala in izbere ničlo linearne interpolacije kot naslednji približek. Iteracija poteka po formuli:
$x_{n+1} = x_n - f(x_n) \frac{x_{n} - x_{n-1}}{f(x_n) - f(x_{n-1})}$
kjer $x_{n}$ in $x_{n-1}$ sta zadnji dve oceni ničle.

#### (7) Naj bo $g$ iteracijska funkcija. Kaj so fiksne tocke za $g$? Kdaj so privlacne, kdaj odbojne? 

Fiksna točka funkcije $g$ je vrednost $x$, za katero velja $g(x) = x$. Fiksne točke so **privlačne**, če je absolutna vrednost odvoda $g'$ pri $x$ manjša od 1 $|g'(x)| < 1$, saj približki konvergirajo k fiksni točki. So **odbojne**, če je $|g'(x)| > 1$, kar povzroči divergenco od fiksne točke.

#### (8) Kako s postopkom navadne iteracije izracunamo nicle neke nelinearne funkcije $f$ ? Kdaj je hitrost konvergence linearna, kvadraticna in kdaj kubicna? 

Navadna iteracija za iskanje ničle funkcije $f$ lahko poteka s transformacijo  $x_{n+1} = g(x_n)$ , kjer je $g(x)$ neka funkcija, izpeljana iz $f$ . Hitrost konvergence je:

- **Linearna**, če je $|g'(x)|$ konstanta manjša od 1.
- **Kvadratična**, če je $g'(x) = 0$ pri fiksni točki.
- **Kubična**, če so izpolnjeni pogoji višjih odvodov.

#### (9) Kateri iteracijski metodi za resevanje sistema nelinearnih enacb poznas? Eno od njiju opisi.

Jacobijeva iteracija in Newtonova metoda. 

Ena od priljubljenih metod je **Newtonova metoda** za reševanje nelinearnih enačb, ki iterativno izboljšuje približke z uporabo tangent k funkciji $f$ , izračunanih z odvodom $f$ . Formula za iteracijo je:
$x_{n+1} = x_n - \frac{f(x_n)}{f'(x_n)}$

#### (10) Kaj je ideja kvazi-Newtonovih metod za resevanje sistemov nelinearnih enacb? Eno od njih natancneje opisi. 

Pri velikem številu enačb je Newtonova metoda zelo zahtevna zaradi računanja veliko odvodov. Pri kvazi-Newtonovih metodah se izognemo računanju parcialnih odvodov. Najbolj znana je Broydenova metoda. 

#### (11) Opisi povezavo med resevanjem sistemov enacb in optimizacijo.

Reševanje sistemov enačb je tesno povezano z optimizacijo, saj iskanje ničel gradienta optimizacijske funkcije neposredno ustreza reševanju nelinearnih enačb. Tehnike, kot so Newtonova in kvazi-Newtonova metoda, se pogosto uporabljajo tako za iskanje ničel enačb kot za iskanje ekstremov funkcij.

### 6. POLINOMSKA INTERPOLACIJA IN APROKSIMACIJA

#### (1) Zapisite sistem enacb, ki doloca interpolacijski polinom skozi paroma razlicne tocke $(x_i, y_i)$, i = 0, 1, . . . , n. Kaksno stopnjo polinoma moramo vzeti, ce hocemo interpolirati 5 tock? Ali je resevanje tega sistema vedno stabilno? 

```math
\begin{bmatrix}
1 & x_0 & x_0^2 & x_0^3 & x_0^4 \\
1 & x_1 & x_1^2 & x_1^3 & x_1^4 \\
1 & x_2 & x_2^2 & x_2^3 & x_2^4 \\
1 & x_3 & x_3^2 & x_3^3 & x_3^4 \\
1 & x_4 & x_4^2 & x_4^3 & x_4^4
\end{bmatrix}
\begin{bmatrix}
a_0 \\
a_1 \\
a_2 \\
a_3 \\
a_4
\end{bmatrix}
=
\begin{bmatrix}
y_0 \\
y_1 \\
y_2 \\
y_3 \\
y_4
\end{bmatrix}
```

Za interpolacijo 5 točk $(x_i, y_i)$, i = 0, 1, ..., 4, potrebujemo polinom četrte stopnje (stopnja $n = 4$), saj je stopnja polinoma enaka številu točk minus ena. Sistem enačb, ki določa koeficiente polinoma, lahko postane nestabilen, še posebej pri visokih stopnjah in če so točke umeščene zelo blizu skupaj ali zelo enakomerno (npr. če opazimo Rungejev pojav).

#### (2) Lagrangeova oblika interpolacijskega polinoma in njene pomanjkljivosti

**Pomanjkljivosti:** Metoda je računsko zahtevna, saj za vsako spremembo točk ali dodajanje nove točke zahteva ponovno izračunavanje celotnega polinoma. Prav tako je občutljiva na numerične napake pri velikem številu točk.

#### (3) Opisite Newtonovo obliko interpolacijskega polinoma. Kaj so to deljene diference in kako jih racunamo? Kaksne so prednosti Newtonove oblike interpolacijskega polinoma v primerjavi z Lagrangeovo?

Newtonov interpolacijski polinom uporablja deljene diference in je zapisan kot:
$P(x) = f[x_0] + f[x_0, x_1](x - x_0) + \ldots + f[x_0, x_1, \ldots, x_n](x - x_0)\ldots(x - x_{n-1})$
Deljene diference se izračunajo rekurzivno in so uporabne za dodajanje novih točk brez ponovnega izračuna celotnega polinoma. **Prednosti:** Večja fleksibilnost in manjša občutljivost na dodajanje točk v primerjavi z Lagrangeovo metodo.

#### (4) Kaj s stalisca interpolacije pomenijo veckratne interpolacijske tocke? Cemu so enake deljene diference $f[x_0, x_0]$ , $f[x_0, x_0, x_0]$ , $f[x_0, x_0, x_0, x_0]$ ? Zapisite interpolacijski polinom, ki se s funkcijo f ujema v tocki $x_0$ stirikratno, to je v vrednosti in v prvih treh odvodih.

Večkratne interpolacijske točke omogočajo, da se polinom ujema ne samo z vrednostmi funkcije, ampak tudi z njenimi odvodi v danih točkah. Deljene diference, kot so $f[x_0, x_0]$, predstavljajo odvode funkcije v točki $x_0$.

#### (5) Povečanje stopnje interpolacijskega polinoma in prileganje funkciji? Utemelji s primerom?

Višanje stopnje interpolacijskega polinoma ne zagotavlja vedno boljšega prileganja, zlasti za kompleksne funkcije ali na večjih intervalih, kjer lahko pride do oscilacij (Rungejev pojav).

#### (6)  Kako lahko ocenimo napako interpolacijskega polinoma za funkcijo $f$ ? Kaksna je napaka interpolacije s polinomom stopnje $n$ .

Napaka interpolacijskega polinoma $P(x)$ za funkcijo $f$ je določena z:
$E(x) = f(x) - P(x)$
Napaka pri interpolaciji s polinomom stopnje $n$ je odvisna od $(n+1)$ - tega odvoda funkcije $f$ in velikosti intervala, v katerem interpoliramo.

#### (7) Kaj so Gaussove kvadraturne formule za izračun integrala $\int_a^b f(x) \ dx$ funkcije \( f \) in kako jih učinkovito določimo?

Gaussove kvadraturne formule so napredne metode za numerično integracijo, ki uporabljajo optimalno izbrane točke in uteži za izračun integralov. Te točke (vozli) in uteži

### 7. NUMERIČNA INTEGRACIJA

#### (1) Opisite osnovno trapezno in osnovno Simpsonovo pravilo. Kako pridemo do teh dveh pravil in kaksni sta napaki? 

**Osnovno trapezno pravilo** aproksimira integral funkcije tako, da izračuna površino trapeza, ki ga oblikujeta graf funkcije in x-os med dvema točkama. Formula je:
$\int_a^b f(x) \, dx \approx \frac{b-a}{2} (f(a) + f(b))$
Napaka tega pravila je $O(h^3)$ za en korak, kjer je $h = b-a$.

**Osnovno Simpsonovo pravilo** uporablja parabolično interpolacijo skozi tri točke za izračun integrala in je natančnejše. Formula je:
$\int_a^b f(x) \, dx \approx \frac{b-a}{6} [f(a) + 4f\left(\frac{a+b}{2}\right) + f(b)]$
Napaka je $O(h^5)$, kjer je $h = b-a$.

#### (2) Opisite sestavljeno trapezno in sestavljeno Simpsonovo pravilo.

**Sestavljeno trapezno pravilo** deli interval integracije na manjše segmente in uporablja osnovno trapezno pravilo na vsakem segmentu, kar zmanjšuje napako.
**Sestavljeno Simpsonovo pravilo** prav tako deli interval na segmente, vendar mora biti število segmentov sodo. Uporablja osnovno Simpsonovo pravilo na vsakem paru sosednjih segmentov za izboljšanje natančnosti.

#### (3) Kako je red kvadraturne formule? Kako je to metoda nedolocenih koeficientov? 

Red kvadraturne formule pomeni, da formula natančno izračuna integral polinomov do določene stopnje. Metoda nedoločenih koeficientov se uporablja za določanje uteži in vozlišč v kvadraturni formuli tako, da formula točno integrira polinome najvišje možne stopnje.

#### (4) Kako lahko dolocimo pravi korak v trapeznem pravilu?

Pravi korak $h$ v trapeznem pravilu določimo glede na želeno natančnost in lastnosti funkcije. Korak se lahko prilagodi na podlagi ocene napake, ki pove, kako hitro se spreminja funkcija $f(x)$.

#### (5) Kako deluje adaptivno trapezno pravilo?

Adaptivno trapezno pravilo samodejno prilagaja korak $h$ med izračunom integrala za doseganje želene natančnosti. Pravilo oceni napako v trenutnem koraku in, če je napaka prevelika, zmanjša korak, če pa je napaka majhna, poveča korak za naslednje segmente, s čimer optimizira celotno računsko delo.

#### (6) Kaj je Rombergova metoda? Opisi osnovni princip in ga prikazi na primeru trapeznega pravila

Rombergova metoda je tehnika za izboljšanje natančnosti numeričnih integracij, ki izhaja iz trapeznega pravila. **Osnovni princip** je uporaba Richardsonove ekstrapolacije za zaporedne približke integrala, ki so izračunani z vedno manjšimi koraki. Začnemo s trapeznim pravilom za grob korak, nato korak postopoma polovimo in izračunamo nove približke. Ti približki se nato kombinirajo za izboljšanje natančnosti.

**Primer uporabe:**

1. Izračunaj integral z osnovnim trapeznim pravilom za korak $h$.
2. Polovi korak in ponovi izračun.
3. Uporabi Richardsonovo ekstrapolacijo za izboljšanje ocene integrala.

#### (7) Kaj so vozli in kaj utezi v kvadraturnem pravilu? V cem so Gaussova kvadraturna pravila boljsa od Newton-Cottesovih? 

Vozli v kvadraturnem pravilu so točke, v katerih funkcijo ovrednotimo, uteži pa so koeficienti, s katerimi pomnožimo vrednosti funkcije za izračun integrala. **Gaussova kvadraturna pravila** so učinkovitejša od Newton-Cottesovih pravil, ker izbirajo optimalne vozle in uteži, ki maksimizirajo stopnjo točnosti za dane vozle. To pomeni, da lahko Gaussova pravila z manjšim številom vozlov dosežejo višjo natančnost kot ekvivalentna Newton-Cottesova pravila.

#### (8) Kako se numericno racuna dvojni integral na pravokotniku? 

Dvojni integral na pravokotniku se običajno izračuna z iteriranjem enodimenzionalnega integracijskega pravila (npr. trapeznega ali Simpsonovega) najprej v eni smeri in nato v drugi. Izračunamo:
$\int_{a}^{b} \int_{c}^{d} f(x,y) \, dx \, dy$
kjer najprej integriramo po $x$ za fiksni $y$, nato rezultate integriramo po $y$.

#### (9) Kako se numericno racuna veckratni integral na poljubnem obmocju? Kaksna je napaka? Koliksna je racunska zahtevnost za napako ϵ?

Za večkratne integrale na kompleksnih območjih se pogosto uporabljajo metode, kot so Monte Carlo ali adaptivne kvadraturne metode, ki se prilagajajo obliki območja. Napaka pri teh metodah je odvisna od števila uporabljenih točk in metode integracije. Računska zahtevnost za doseganje napake $( \epsilon \)$ narašča s kompleksnostjo območja in dimenzijo integrala.

### 8. REŠEVANJE DIFERENCIALNIH ENAČB

#### (1)  Opisite Eulerjevo metodo za resevanje zacetnega problema $y_0 = f(x, y)$ pri pogoju $y(a) = y_a$ .

Eulerjeva metoda je osnovna numerična metoda za reševanje diferencialnih enačb oblike $y' = f(x, y)$ s začetnim pogojem 
$y(a) = y_a$. Metoda napreduje z iterativnim izračunom:
$y_{n+1} = y_n + h f(x_n, y_n)$
kjer $h$ predstavlja korak, $x_n$ je trenutna točka, in $y_n$ trenutna vrednost rešitve.

#### (2) Opisite idejo Runge-Kutta metod za resevanje diferencialnih enacb. Koliko je napaka metode reda $k$ ?

Runge-Kutta metode izboljšajo Eulerjevo metodo s točnejšim izračunom sprememb $y$ z uporabo več vmesnih korakov. Napaka metode reda $k$ je $O(h^{k+1})$, kjer $k$ predstavlja število stopenj metode (npr. pri RK4 je $k = 4$, zato napaka znaša $O(h^5)$ ).

#### (3) Kaj je adaptivna metoda za resevanje zacetnega problema  $y_0 = f(x, y)$ pri pogoju $y(a) = y_a$ in kaj je DOPRI5?

Adaptivne metode prilagajajo velikost koraka $h$ glede na lokalno napako rešitve. **DOPRI5** je priljubljena adaptivna Runge-Kutta metoda petega reda, ki dinamično prilagaja korak, da optimizira natančnost in učinkovitost. Ima vgrajen nadzor napake, ki omogoča natančnejše reševanje.

#### (4) Opisite idejo Adams-Bashforthove metode za resevanje diferencialnih enacb. Koliko je napaka metode reda $k$ ?

Adams-Bashforthove metode so eksplicitne večkorakne metode, ki uporabljajo pretekle vrednosti $f(x, y)$ za napovedovanje novih vrednosti. Napaka metode reda $k$ je $O(h^k)$, kar pomeni, da več korakov vodi do večje natančnosti.

#### (5)  Opisite idejo Adams-Moultonove (AM) metode za resevanje diferencialnih enacb. Koliko je napaka metode reda $k$ ? V kaksnem smislu je AM metoda implicitna metoda?

Adams-Moultonove metode so implicitne večkorakne metode, ki vključujejo trenutno in pretekle vrednosti $f(x, y)$ za izračun $y_{n+1}$. Napaka metode reda $k$ je $O(h^{k+1})$. Metoda je implicitna, ker zahteva rešitev algebrske enačbe za $y_{n+1}$ na vsakem koraku.

#### (6) Opisite idejo ABM prediktor-koretkor metode za resevanje diferencialnih enacb. Koliko je napaka metode reda $k$?

ABM (Adams-Bashforth-Moulton) metoda kombinira prediktor (Adams-Bashforth) za inicialno oceno in korektor (Adams-Moulton) za končno prilagoditev. Napaka te kombinirane metode reda $k$ je $O(h^{k+1})$.

#### (7) Opisite idejo strelske metode za resevanje robnih problemov DE.

Strelska metoda pretvori robni problem v začetni problem z ugibanjem začetnih pogojev. Metoda iterativno prilagaja začetne pogoje, dokler rešitev ne ustreza robnim pogojem. Primerna je za linearni ali nelinearni robni problem.

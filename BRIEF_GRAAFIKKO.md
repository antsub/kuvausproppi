# Kuvausproppi — brief graafikolle

**Kohtaus:** Mike, peligraafikko, yövuorossa kello kolmelta aamuyöllä. Tietokoneen
ruutu on kohtauksen toinen näyttelijä: sovellukset vilisevät, ilmoitukset piippaavat,
bugilista kasvaa 3 → 13 → 31 samalla kun kello kääntyy 3:31:een.

**Proppi on toiminnassa.** Se on yksi HTML-tiedosto (`proppi.html`), joka ajetaan
Miken PC:llä selaimessa kokoruudulla. Se on oikeasti klikattava — näyttelijä voi
vastata viesteihin, valita objekteja pelimoottorista ja käyttää ohjelmia niin että
ne reagoivat. Operaattori ohjaa kohtausta näppäimistöltä otto kerrallaan.

---

## 1. Lue tämä ensin — työn luonne muuttui

Aiemmassa versiossa graafikko olisi tehnyt 12 koko ruudun PNG:tä, jotka olisivat
korvanneet käyttöliittymät. **Se ei enää käy.** Kuva sovelluksen päällä estäisi
klikkaukset: näyttelijä ei voisi kirjoittaa viestiä eikä valita mitään.

Työ jakautuu nyt kahteen osaan:

| | |
|---|---|
| **A. Kuvatiedostot** | Renderit, tekstuurit ja ikonit. Pudotetaan `assets/`-kansioon, ei koodimuutoksia. Alle listattu 11 tiedostoa |
| **B. Ulkoasusuunnittelu** | Käyttöliittymien värit, typografia, tila ja rytmi. Toimitat suunnitelman (kuvina tai määrittelynä), se ajetaan koodiin CSS:ään |

Osa B on pienempi työ kuin miltä kuulostaa: kaikki tyylit ovat yhdessä paikassa
`proppi.html`:n alussa, ja käyttöliittymä on rakennettu muutamasta toistuvasta
palikasta (paneeli, rivi, ominaisuusrivi, työkalupalkki). Kun ne on ratkaistu,
kaikki kahdeksan sovellusta muuttuvat kerralla.

---

## 2. Kuvatiedostot

Kaikki PNG, sRGB, 8-bit. Läpinäkyvyys sallittu.

| Tiedosto | Koko | Sisältö | Prio |
|---|---|---|---|
| `engine_viewport_wasteroom.png` | **1280×720** | **Jätehuone-render** — pelin sisältö | **1** |
| `patina_wall.png` | 910×810 | Seinäpinta lähikuvassa, Patinan esikatselu | 2 |
| `desktop.png` | 1920×1080 | Työpöydän taustakuva | 4 |
| `icon_klatter.png` | 68×68 | Tehtäväpalkin ikoni — chat | 3 |
| `icon_posthaus.png` | 68×68 | sähköposti | 3 |
| `icon_engine.png` | 68×68 | pelimoottori | 3 |
| `icon_chisel.png` | 68×68 | 3D-mallinnus | 3 |
| `icon_patina.png` | 68×68 | materiaalimaalaus | 3 |
| `icon_depot.png` | 68×68 | versionhallinta | 3 |
| `icon_tickr.png` | 68×68 | tuntikirjaus | 3 |
| `icon_backloggr.png` | 68×68 | tiketit | 3 |
| `thumb_<nimi>.png` | 86×66 | Valinnaisia assettikuvakkeita, ks. kohta 4 | 5 |

**Jätehuoneen renderin paikka lavalla on x 290, y 130 (1280×720).** Se on ainoa
kuva, jota kohtauksessa katsotaan pitkään ja lähellä. Käytä siihen leijonanosa
ajasta.

Viewportin päälle jää koodattuna kaksi kerrosta, jotka ovat voimassa renderin
kanssa: **välkkyvä loisteputkivalo ja lika-/naarmutekstuuri**. Tee pohja siis
hieman tasaisemmaksi kuin lopputuloksen pitää olla.

Vaihtoehto: **`.mp4`-looppi** samalla nimellä toimii myös, jos haluat liikettä
(savu, valon värähtely). Kerro etukäteen, niin vaihdan img-tagin video-tagiksi.

---

## 3. Kahdeksan sovellusta

Nämä ovat keksittyjä ohjelmia, jotka on rakennettu oikeiden peliteollisuuden
työkalujen logiikalla. Sukulaisuus riittää — **kopio ei käy** (ks. kohta 6).

| Sovellus | Vastine todellisuudessa | Rooli kohtauksessa |
|---|---|---|
| **VESSEL ENGINE 9.4** | pelimoottori | Miken päätyökalu. Jätehuone on tässä auki |
| **CHISEL 4.2** | 3D-mallinnusohjelma | Roskasäiliön mallinnus, wireframe näkyvissä |
| **PATINA 8** | materiaalimaalausohjelma | Tästä lika tulee. Tasoina: valumat, ruoste, home |
| **DEPOT** | versionhallinta | Kollega on lukinnut tiedoston. Mike ei pääse eteenpäin |
| **KLATTER** | chat | Kaikki huutavat yhtä aikaa. Näyttelijä voi vastata |
| **BACKLOGGR** | tikettijärjestelmä | Bugilista. Kasvaa 3 → 31 kohtauksen aikana |
| **POSTHAUS** | sähköposti | 2 431 lukematonta, ylimpänä automaattiset build-virheet |
| **TICKR** | tuntikirjaus | 71 h viikossa, ylityötä +31 h |

Vilinässä (cue 1) kukin on ruudulla 0,34–1,1 sekuntia. Ne luetaan **siluettina ja
värinä**, eivät sisältönä. Siksi jokaisella on oma tunnusvärinsä ja oma
paneelirytminsä — ne ovat tärkeämpiä kuin yksityiskohdat.

Nykyiset tunnusvärit:

| Sovellus | Hex | |
|---|---|---|
| Klatter | `#7C5CD6` | violetti |
| Posthaus | `#3A6BD8` | sininen |
| Vessel Engine | `#8A9099` | harmaa |
| Chisel | `#6E9E4F` | oliivi |
| Patina | `#3E9E92` | verdigris |
| Depot | `#8C6FA8` | luumu |
| Tickr | `#D8862A` | amber |
| Backloggr | `#2FA8C7` | syaani |

---

## 4. Peruspaletti ja kamerasäännöt

| Käyttö | Hex |
|---|---|
| Taustan pohja | `#0E1116` |
| Paneeli | `#151A21` |
| Paneeli, korostettu | `#1A2029` |
| Paneeli, kohotettu | `#202834` |
| Viivat | `#232B36` / `#2E3846` |
| Teksti | `#C8D0D8` |
| Himmeä teksti | `#6C7885` / `#4E5866` |
| Valinta | `#2A4058` |
| Urgent / virhe | `#C4402F` |
| Varoitus | `#C79A3A` |
| OK | `#5E9E6B` |

### Säännöt, jotka eivät ole makuasioita

- **Ei puhdasta valkoista.** Kirkkain sallittu `#C8D0D8`. `#FFFFFF` palaa puhki.
- **Ei puhdasta mustaa.** Tummin `#0E1116`. Täysmusta ei valaise Miken kasvoja.
- **Ohuin viiva 2 px.** 1 px katoaa tai kihelmöi skaalatessa.
- **Pienin teksti 13 px** (1920-mittakaavassa).
- **Vältä laajoja hienovaraisia liukuvärejä** — 8-bit + videopakkaus tuottaa raitoja.
- **Vältä täyskylläisiä värejä.** Ne clippaavat värikanavassa ennen kirkkausrajaa.

### Typografia

Nyt käytössä IBM Plex Sans (käyttöliittymä) ja IBM Plex Mono (kaikki numerot,
tiedostonimet, lokit, kellonajat). Numerot ovat tabulaarisia, jotta ne eivät
hyppi päivittyessään. Jos vaihdat kirjasimet, mono-kirjasin on pakollinen
numeroille — se on iso osa siitä, miksi ruutu lukeutuu työkaluna.

### Valinnaiset assettikuvakkeet

Vessel Enginen Project-välilehdellä on 12 assettia. Jokaiselle voi tehdä oman
86×66 pikkukuvan nimellä `thumb_<assetin nimi>.png`, esim. `thumb_M_grime_04.png`.
Ilman kuvaa ne näkyvät värillisinä paikkamerkkeinä, mikä on täysin riittävää.
Nimet: `SM_bin_rusted_01`, `SM_bin_rusted_02`, `SM_bag_pile_03`, `SM_wall_stain_a`,
`M_grime_04`, `MI_metal_rust_02`, `T_wall_stain_a_BC`, `T_wall_stain_a_N`,
`T_wall_stain_a_ORM`, `T_rust_fine_BC`, `BP_door_waste`, `waste_room_01`.

---

## 5. Maailman kaanoni

| | |
|---|---|
| Studio | Grimeshift Studios |
| Projekti | GRIME-4, sprint 31, tiketit `GRIME-44xx` |
| Kohtaus | `waste_room_01.scene` |
| Build | #4471, epäonnistunut |
| Henkilöt | Mike (käyttäjä), T. Rautio, Producer, QA Bot |

Nimeämiskäytäntö on peliteollisuuden oikea: `SM_` static mesh, `M_` materiaali,
`MI_` materiaali-instanssi, `T_` tekstuuri, `BP_` blueprint, ja tekstuurien
päätteet `_BC` (base color), `_N` (normal), `_ORM` (occlusion/roughness/metallic).
Pidä nämä, jos teet omia nimiä.

**Luku 331 ja sen johdannaiset ovat tarkoituksellisia**: 331 known issues,
kello 3:31, 31 urgent requests, virhekoodi `0x0000331F`, tiling 3.31, bake 31 %,
ylityö +31 h, revisio #331. Älä siisti niitä pois.

---

## 6. Tavaramerkit

Sovellusnimet ovat keksittyjä juuri siksi, ettei Slackin, Googlen, Unityn,
Blenderin, Adoben tai Perforcen ilmettä tarvitse klaarata.

**Älä jäljittele tunnistettavasti.** Ei Slackin ruudukkologoa, ei Gmailin
M-kirjainta, ei Unityn kuutiota, ei Blenderin oranssia pyörrettä, ei Substancen
ikonia. Ammattikäyttäjä saa tunnistaa ohjelman *tyypin* sekunnissa — mutta ei
tuotetta.

---

## Liite A: Missä mikäkin grafiikka näkyy

| Cue | Näkyvä | Tapahtuma |
|---|---|---|
| 0 | `desktop.png` | Perustila, kello 3:28 |
| 1 | kaikki 8 sovellusta | **Vilinä** — 1,1 s → 0,34 s, kiihtyen |
| 2 | Klatter | Ilmoitus: "3 NEW URGENT REQUESTS" |
| 3 | Vessel Engine + jätehuone | Mike työstää kohtausta |
| 4 | sama | Mike herää mikrounesta → "13 NEW URGENT REQUESTS" |
| 5 | sama | Kello **3:31** (välähtää) |
| 6 | Backloggr | "31 URGENT REQUESTS", lista kasvaa 3 → 31 |

## Liite B: Mitä näyttelijä voi tehdä ruudulla

Nämä toimivat oikeasti. Hyvä tietää, koska ne vaikuttavat siihen, mitä ruudulla
pitää olla luettavaa.

- **Klatter:** vaihtaa kanavaa, kirjoittaa viestin ja lähettää sen. Viesti ilmestyy
  ketjuun oikealla kellonajalla, ja vastapuoli alkaa "kirjoittaa…" ja vastaa
  parin sekunnin päästä
- **Vessel Engine:** valitsee objektin hierarkiasta tai suoraan näkymästä
  (inspector päivittyy), vaihtaa työkalua, painaa Play, vaihtaa alalaidan
  välilehteä
- **Patina:** sytyttää ja sammuttaa materiaalitasoja — likakerrokset katoavat
  ja palaavat esikatselusta
- **Chisel:** vaihtaa varjostustilan (rautalanka / kiinteä / materiaali)
- **Depot:** valitsee tiedoston ja yrittää checkoutia — lukittu tiedosto antaa
  virheilmoituksen
- **Posthaus:** avaa viestin, lukemattomien määrä vähenee
- **Backloggr:** avaa tiketin, yksityiskohdat aukeavat oikealle
- **Tickr:** pysäyttää ja jatkaa ajastinta
- **Tehtäväpalkki:** vaihtaa sovellusta
- **Ilmoituskortti:** klikkaus kuittaa sen pois

## Liite C: Näppäimet kuvauspaikalla

Ohjauspalkki on ruudun yläreunassa. **Piilota se `H`:lla ennen ottoa.**

```
VÄLILYÖNTI  seuraava cue        A  viritä hiirilaukaisu (cue 4)
0–6         hyppää cueen        B  musta ruutu (ottojen väli)
←/→         vilinän nopeus      C  kursori piiloon / näkyviin
[  ]        ruudun kirkkaus     K  kello +1 min (3:31 → 3:26)
R           alkuun              G X Y Z  glitchit  (⇧ = jatkuva)
H           piilota palkki      V  chatin autovastaus pois
                                M  ilmoitusääni pois
                                F  koko ruutu
```

**Kello lähtee 3:28 ja pysähtyy 3:31:een**, jonka jälkeen se ei liiku — se on
jatkuvuuden takia pakollista. `K` vie minuutin eteenpäin, ja 3:31:ssä se
palauttaa kellon 3:26:een. Tickrin työaika on kiinni lukemassa 13 h 12 min,
vain sekunnit kiertävät.

**Kun näyttelijä kirjoittaa chattiin, operaattorin näppäimet ovat pois käytöstä**
— muuten "b" mustaisi ruudun kesken repliikin. Ohjauspalkkiin syttyy tällöin
oranssi varoitus. **Esc** palauttaa näppäimet operaattorille.

`A` virittää cuen 4 laukeamaan Miken **hiiren liikkeestä**: hän herää, heiluttaa
hiirtä, ruutu vastaa. Operaattorin ei tarvitse osua painallusta millisekunnilleen.

`[` ja `]` säätävät ruudun kirkkautta 50–140 %. Käytä tätä äläkä monitorin omaa
säätöä: monitorin himmennys on useimmiten PWM-pulssitusta, joka lyö kameran
sulkijaa vastaan. **Monitorin oma kirkkaus 100 %.**

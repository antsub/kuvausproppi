# Kuvausproppi — Miken työpöytä

Selaimessa ajettava kuvausproppi: peligraafikon työasema yövuorossa. Kahdeksan
keksittyä ohjelmaa, klikattava käyttöliittymä ja näppäimistöltä ajettava
seitsemän cuen kohtaus.

Ei asennuksia, ei nettiyhteyttä, ei palvelinta. Yksi HTML-tiedosto.

---

## Käyttöohje

### 1. Avaa

Avaa `proppi.html` selaimessa (Chrome, Edge tai Firefox). Paina **F** tai **F11**
kokoruututilaan.

### 2. Piilota ohjauspalkki

Ruudun yläreunassa on operaattorin ohjauspalkki. **Paina `H` ennen ottoa.**
Sama näppäin tuo sen takaisin.

### 3. Aja kohtaus

**Välilyönti** vie seuraavaan cueen. Numerot **0–6** hyppäävät suoraan.

| Cue | Mitä ruudulla tapahtuu |
|:---:|---|
| **0** | Työpöytä, kello 2:58 |
| **1** | Sovellusvilinä — 8 ohjelmaa vaihtuu kiihtyen 1,1 s → 0,34 s |
| **2** | Klatter + ilmoitus "3 NEW URGENT REQUESTS" |
| **3** | Vessel Engine, jätehuone auki |
| **4** | Ilmoitus "13 NEW URGENT REQUESTS" |
| **5** | Kello korostuu — **3:31** |
| **6** | Backloggr, lista kasvaa 3 → 31, "31 URGENT REQUESTS" |

### Kello on jäädytetty

Kello lukee **3:31 koko ajan** eikä kulje itsestään. Tämä on tarkoituksellista:
kellon pitää näyttää sama lukema joka otossa, tai jatkuvuus rikkoutuu
leikkauksessa. Sama koskee Tickrin ajastinta — tunnit ja minuutit ovat kiinni
lukemassa 11:47, vain sekunnit elävät.

Jos ohjaaja haluaa kuvata sen, että **kello vaihtuu** 3:31:een, paina **`K`**.
Silloin cuet 0–4 näyttävät 2:58 ja cue 5 kääntää sen 3:31:een. `K` uudestaan
palauttaa kiinteän 3:31:n. Voimassa oleva tila näkyy ohjauspalkissa.

### 4. Näppäimet

```
VÄLILYÖNTI  seuraava cue        A  viritä hiirilaukaisu (cue 4)
0–6         hyppää cueen        B  musta ruutu (ottojen väli)
←  →        vilinän nopeus      C  kursori piiloon / näkyviin
[  ]        ruudun kirkkaus     K  kello: 3:31 kiinteä / 2:58 → 3:31
R           alkuun              V  chatin autovastaus pois
H           piilota palkki      M  ilmoitusääni pois
                                F  koko ruutu
```

**`A`** virittää cuen 4 laukeamaan hiiren liikkeestä: näyttelijä herää, heiluttaa
hiirtä, ruutu vastaa. Operaattorin ei tarvitse osua painallusta millisekunnilleen.

**`[` ja `]`** säätävät ruudun kirkkautta 50–140 %. Käytä näitä äläkä monitorin
omaa säätöä — monitorin himmennys on useimmiten PWM-pulssitusta, joka lyö kameran
sulkijaa vastaan ja tuottaa vilkkuvan palkin. **Monitorin oma kirkkaus 100 %.**

### 5. Näyttelijä voi klikkailla

Sivu on oikeasti käytettävä. Näyttelijä voi mm. vaihtaa chat-kanavaa, kirjoittaa
ja lähettää viestin (vastapuoli alkaa "kirjoittaa…" ja vastaa), valita objekteja
pelimoottorista, sammuttaa likakerroksia materiaaliohjelmasta ja avata tikettejä.

> **Kun näyttelijä kirjoittaa chattiin, operaattorin näppäimet ovat pois käytöstä**
> — muuten "b" mustaisi ruudun kesken repliikin. Ohjauspalkkiin syttyy oranssi
> varoitus. **Esc** palauttaa näppäimet operaattorille.

---

## Ennen kuvauspäivää

- Windows: **Älä häiritse** päälle, päivitykset pois, näytönsäästäjä ja
  virransäästö pois
- Selain kokoruutuun, välilehtipalkki piiloon
- **Monitorin kirkkaus 100 %** (ks. yllä)
- Night light / sinisensuodatus pois
- Testikuvaus näytön kanssa: sulkijanopeutta säädetään kunnes rullaava palkki
  katoaa. Monitorin virkistystaajuus kannattaa asettaa kuvausnopeuden
  monikerraksi (50 Hz / 25 fps tai 60 Hz / 30 fps)

---

## Grafiikan lisääminen

Pudota kuvat `assets/`-kansioon, ne korvaavat paikkamerkit automaattisesti.
Ei koodimuutoksia. Täydet ohjeet: **[BRIEF_GRAAFIKKO.md](BRIEF_GRAAFIKKO.md)**

| Tiedosto | Koko |
|---|---|
| `engine_viewport_wasteroom.png` | 1280×720 — jätehuone-render |
| `patina_wall.png` | 910×810 |
| `desktop.png` | 1920×1080 |
| `icon_klatter.png` … `icon_backloggr.png` | 68×68, 8 kpl |

---

## Tiedostot

```
proppi.html          Koko proppi. Ainoa tiedosto, jota tarvitaan ajamiseen.
index.html           Aloitussivu (vain verkkoversiota varten)
BRIEF_GRAAFIKKO.md   Ohjeet graafikolle
assets/              Kuvat — pudota tänne
```

Sovellukset ovat keksittyjä (Klatter, Posthaus, Vessel Engine, Chisel, Patina,
Depot, Tickr, Backloggr), jotta oikeiden tuotteiden tavaramerkkejä ei tarvitse
klaarata.

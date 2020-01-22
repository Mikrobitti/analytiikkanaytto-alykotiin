# Analytiikkanäyttö Älykotiin - Mikrobitti 2/2020

Oheisesta repositoriosta löytyy vinkkejä helmikuun 2020 Mikrobitin *Analytiikkanäyttö älykotiin* taikapeilinrakennusosioon. Tee-se-itse kotiautomaatiota -artikkelisarjan 3. osa.


## MagicMirror -taikapeilin rakennusvaiheet

Kuvitetut ohjeet itse taikapeilin kasaamiseen löydät Mikrobitistä 2/2020. Tällä sivulla tarkemmin vinkkejä peilin ohjelmistopuolen käyttöönottoon sekä peilin ohjelmapuolen kustomointiin.


### Käyttöjärjestelmän asentaminen Raspberry Pi:lle

Mikäli kaivoit tuoreen Raspberry Pi:n suoraan naftaliinista, on siihen ensin asennettava käypä käyttöjärjestelmä. Tässä artikkelissa käytämme suosittua Raspbian -käyttöjärjestelmää. Oheisilla ohjeilla saat Raspin kehräämään! Alla olevat ohjeet mukailevat [tätä sivua](https://www.raspberrypi.org/documentation/installation/installing-images/).

1. Lataa `Raspbian Buster with desktop` -kuva osoitteesta [(https://www.raspberrypi.org/downloads/raspbian/](https://www.raspberrypi.org/downloads/raspbian/)

2. Lataa ja asenna balenaEtcher -ohjelma käyttöjärjestelmän muistikortille kirjoittamista varten osoitteesta [https://www.balena.io/etcher/](https://www.balena.io/etcher/)

3. Liitä micro-SD- muittikortti tietokoneeseen kiinni ja avaa balenaEtcher. Valitse .img -päätteinen Raspbian Buster -kuva latauskansiostasi (`Select image`) ja juuri kytkemäsi muistikortti (`Select drive`). Paina `Flash!` -nappia.

4. Siinäpä se! Laita muistikortti kiinni Raspberry Pihin. Kytke myös virtalähde, näyttö, näppäimistö ja hiiri, niin pääset alkuun!

5. Konfiguroi käyttöjärjestelmän asetukset mieluiseksesi Raspbianin käyttöönottovelhon (Setup Wizard) avulla. Sen pitäisi käynnistyä automaattisesti ensimmäisellä käynnistyskerralla.

Mikäli et ole aiemmin tutustunut Raspberry Pi:hin, suosittelen lämpimästi tutustumaan Raspberry Pi:n omaan, lempeään aloitussivuun: [Getting Started with Raspberry Pi](https://projects.raspberrypi.org/en/pathways/getting-started-with-raspberry-pi), ja selailemaan etenkin `Using your Raspberry Pi > Using the terminal` -osion läpi.

Varmistathan ennen MagicMirror2 -ohjelmiston asentamista, että internetyhteys toimii. Kytke siis joko verkkokaapeli Raspberry Pi:hin tai kliksuttele langattoman verkon asetukset kuntoon työpöydän oikeasta yläkulmasta.


### Näytön asetusten konfigurionti

Taikapeilinäytöstä voi olla enemmän hyötyä pystyasennossa. Näytön orientaation saa muutettua `/boot/config.txt` -tiedostosta. Avaa siis tiedosto rohkeasti tekstieditorissa kirjoittamalla komentoriville `sudo nano /boot/config.txt`. Kirjoita (tai muuta riviä) `display_rotate=1`. Tämä kiertää kuvaa 90 astetta. Vaihtoehtoisesti `display_rotate=3` voi toimia paremmin, mikäli kaikki näyttäisi olevan tyystin väärinpäin.

Tallenna asetustiedosto näppäinyhdistelmällä `Ctrl+x`. Käynnistä Raspberry Pi uudelleen komennolla `sudo reboot`.


### MagicMirror2 -ohjelmiston asentaminen Raspberry Pi:lle

MagicMirror -ohjelmisto kehittyy jatkuvasti, joten varmasti tuoreimmat asennus- ja konfigurointiohjeet löydät [docs.magicmirror.builders](https://docs.magicmirror.builders) -sivustolta.

---

**Vaihtoehto 1. asennusskripti**
Helpoimmalla pääset ajamalla sdteweil:in komentoriviasennusskriptin [täältä](https://github.com/sdetweil/MagicMirror_scripts).

Asennusskripti kysyy seuraavan kysymyksen asennuksen aikana: `Do you want use pm2 for auto starting of your MagicMirror (y/N)?`. YES.

Kirjoita vielä `pm2 save` tallentaaksesi asennusskriptin luomat MagicMirror -asetukset. Tätä en löytänyt tuoreimmasta skriptistä.
Käynnistä / sammuta ohjelmisto PM2:n kautta komentoriviltä komennoilla `pm2 start/restart/stop MagicMirror`.

**Vaihtoehto 2. manuaaliasennus**
Mikäli em. tapa aiheuttaa harmaita karvoja, kannattaa asennus suorittaa manuaalisesti magicmirror.buildersin [ohjeilla](https://docs.magicmirror.builders/getting-started/installation.html#manual-installation). Manuaaliasennus ei kuitenkaan ota kantaa automaattikäynnistykseen. Ohjeet sen käyttöönottoon [täällä](https://github.com/MichMich/MagicMirror/wiki/Auto-Starting-MagicMirror)

Käynnistä / sammuta ohjelmisto suoraan asennuskansiosta (`cd ~/MagicMirror`) komennolla `npm start`.
Mikäli seurasit automaattikäynnistyksen ohjeita, voit käyttää käynnistykseen suoraan työkalua PM2: `pm2 start/restart/stop MagicMirror`.

---

Lisäksi kannattaa seurata [näitä](https://github.com/MichMich/MagicMirror/wiki/Configuring-the-Raspberry-Pi) hyviksi havaittuja Raspberry Pi -spesifejä konfiguraatio-ohjeita ja niksejä muun muassa suoritinkäytön vähentämiseksi, näytön konfiguroimiseksi ja hiirenosoittimen piilottamiseksi.


### MagicMirror2 -ohjelmiston konfigurointi ja lisäosien asentaminen

MagicMirror2 -ohjelmisto on Node.js -pohjainen Electron -käyttöliittymäkehystä käyttävä web-ohjelma. Sen konfigurointi tapahtuu muokkaamalla `config.js` -tiedostoa, joka löytyy ohjelman asennuskansiosta (oletuksena `cd ~/MagicMirror/config/config.js`).

Listan asetuksista löydät [täältä](https://docs.magicmirror.builders/getting-started/configuration.html#general).


### Ulkoisten lisämoduulien asentaminen

MagicMirror2 -ohjelmisto on laajennettavissa lukuisin liitännäisin, eli moduulein. Jokainen taikapeilillä näkyvä kokonaisuus on todennäköisesti oma moduulinsa. Kaikki MagicMirro2 -ohjelmiston moduulita ovat erillisiä node.js -moduuleja, jotka asennetaan omaan kansioonsa `~/MagicMirror/modules/<moduuli>`. Moduulit otetaan käyttöön ja konfiguroidaan lisäämällä moduulikohtainen konfiguraatio-objekti `config.js`:n `modules` -listaan.

Kattavat ohjeet moduulien käyttämisestä löydät (docs.magicmirror.builders/modules)[https://docs.magicmirror.builders/modules/introduction.html] -sivuilta.


**Uusien moduulien käyttöönotto tapahtuu tyypillisesti kutakuinkin näin:**

1. Asenna moduuli, mikäli se on kolmannen osapuolen koodaama. Tarkemmat asennusohjeet tähän löytyy yleensä moduulin github-sivuilta, mutta useimmat noudattavat samaa kaavaa.
2. Navigoi moduulikansioon `cd ~/MagicMirror/modules`
3. Kloonaa moduulin koodi githubista `git clone git clone https://github.com/mymoduleauthor/MMM-mymodule.git`
4. Navigoin moduulin kansioon `cd MMM-mymodule`
5. Asenna riippuvuudet `npm install`
6. Konfiugroi ja ota moduuli käyttöön lisäämällä juuri asentamasi moduulin konfiguraatio-objekti `config.js`:n `modules` -listaan. Esimerkiksi Gedit-editorin avulla `gedit ~/MagicMirror/config/config.js`.

MagicMirror-tarjoaa helpohkon rajapinnan omien näyttömoduulien rakentamiseen, ja alan harrastajat ovatkin rakentaneet omiin peileihinsä aimo liudan erilaisia moduuleja ja integraatioita.

Muutaman manuaaliasennuksen jälkeen saatat haluta kokeilla [MagicMirror Package Manageria](https://github.com/Bee-Mar/mmpm) moduulien hallintaan.


### Automaattinen virransäästötila käyttöön

Ylläolevilla ohjeilla taikapeilinäyttö on aina päällä. Joissakin tilanteissa voi olla kätevää sammuttaa näyttö, esimerkiksi sähkön säästämiseksi, huoneen pimentämistä varten, tai vaikkapa taikapeilin tietojen vain tietyille henkilöille näyttämiseksi.

Tämän toiminnallisuuden voi toteuttaa monella tapaa. Yksinkertaisimmillaan näytön voi ajastaa menemään pois päältä tiettyyn vuorokaudenaikaan, esimnerkiksi `crontab`in avulla. Näyttöä voi ohjata myös esimerkiksi kameranliikkeen, kauko-ohjaime, painonapin tai muiden anturien avulla.

Alla ohjeet erillisen liikeanturin (PIR) käyttämiseen ruudun päälle ja pois kytkemiseksi.


#### Virtaa säästymään liikeanturin avulla

Geneerisen liikeanturin voit tilata esimerkiksi Aliexpressestä hakusanalla [PIR sensor module](https://www.aliexpress.com/af/pir-sensor-module.html?trafficChannel=af&d=y&CatId=0&SearchText=pir+sensor+module&ltype=affiliate&SortType=total_tranpro_desc&groupsort=1&page=1)

Kytke moduuli Raspberry Pihin muutamalla hyppylangalla seuraavalla tavalla.

```
 +-----------+       +----------+
 |    RPi    |       |   PIR    |
 +-----------+       +----------+
 |3V3      5V---------POWER     |
 |BCM2     5V|    +--|OUT       |
 |BCM3    GND-----|---GND       |
 |BCM4------------+  +----------+
 |...     ...|
 +-----------+
 
 5V -> POWER
 GND -> GND
 BCM4 -> OUT
```

1. Asenna MMM-PIR -moduuli [täältä](https://github.com/mboskamp/MMM-PIR).
2. Avaa `config.js` haluamassasi tekstieditorissa, esim. Gedit: `gedit ~/MagicMirror/config/config.js`
3. Lisää `modules` -listaan uusi `MMM-PIR` -konfiguraatio

```
{
    module: 'MMM-PIR',
    position: 'bottom_center',
    config: {
        sensorPin: 4,
        delay: 10000, // turn off the display after 10s of no movement
        turnOffDisplay: true
    }
}
```

(Huom! Mikäli olet vaihtanut Raspberry Pi:n käyttämään KMS OpenbGL -ajuria, joudut vaihtamaan vanhemman `tvservice -o` -komennon `vcgencmd display_power 0` ja `vcgencmd display_power 1` -komentoihin moduulin `displayON.sh` ja `displayOff.sh` skripteihin)


### Vinkkejä, linkkejä ja ideoita virittelijöille

**Ajastettu näytön sammuttaminen**

[MMM-Remote-Control](https://github.com/Jopyth/MMM-Remote-Control) on erinomainen yleismoduuli taikapeilin etäohjaukseen. Käteväni webkäyttöliittymän lisäksi se tarjoaa erinomaisen rajapinnan peiliin muille moduuleille. Saat esimerkiksi vallan mainion ajastetun virransäästötilan aikaiseksi lähettämällä MMM-Remote-Control -moduulille `MONITORON` ja `MONITOROFF` -signaaleja [MMM-ModuleSchedulerilla](https://github.com/ianperrin/MMM-ModuleScheduler).


**HSL-aikataulut peiliin**
[mm-hsl-timetable](https://github.com/ZakarFin/mm-hsl-timetable) ja [MMM-Hsl-stops](https://github.com/0EQUALIZERO/MMM-Hsl-stops) näyttävät lähipysäkin bussiaikataulut peilillä.


**Peili vain autorisoiduille käyttäjille**

Yhdistä [MMM-Face-Reco-DNN](https://github.com/nischi/MMM-Face-Reco-DNN) kasvojentunnistusmoduuli [MMM-Remote-Control](https://github.com/Jopyth/MMM-Remote-Control) -moduuliin, jolloin taikapeili näytetään vain tunnistetuille käyttäjille. Tämän saat toimimaan kaappaamalla `USERS_LOGIN` ja `USERS_LOGOUT` -notifikaatiot esimerkiksi [MMM-NotificationTrigger](https://github.com/eouia/MMM-NotificationTrigger) -moduulin avulla, ja välittämällä näistä signaaleista `MONITORON` ja `MONITORON` -notifikaatiot.

